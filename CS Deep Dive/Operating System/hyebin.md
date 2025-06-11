1. 프로세스(Process)와 스레드(Thread)의 차이는 무엇인가요?
- 프로세스: 실행 중인 프로그램 (ex. 아파트 한 세대)
- 스레드: 프로세스 내에서 실행되는 작업의 단위 (ex. 그 세대의 가족 구성원)

| 항목     | **프로세스(Process)**                           | **스레드(Thread)**                      |
| ------ | ------------------------------------------- | ------------------------------------ |
| 정의     | 실행 중인 프로그램                                  | 프로세스 내에서 실행되는 작업의 단위                 |
| 메모리 공간 | 독립적인 메모리 공간 사용                              | 같은 프로세스 내에서 메모리 공간(Heap, Code 등)을 공유 |
| 생성 비용  | 무겁고 비용이 큼 (Context Switching 비용 ↑)          | 가볍고 빠름                               |
| 안정성    | 하나가 죽어도 다른 프로세스에는 영향 없음                     | 하나의 스레드가 죽으면 전체 프로세스에 영향 줄 수 있음      |
| 통신 방식  | IPC(Inter-Process Communication) 등 별도 방식 필요 | 메모리 공유로 간단함                          |

2. 스레드를 사용하면 어떤 이점이 있나요? 단점은요?
- 장점 
    - 병렬 처리 가능: CPU 코어를 활용해 동시에 여러 작업 수행
    - 자원 절약: 같은 프로세스 내에서 메모리 공유 → 생성 비용 낮음
    - 반응성 향상: GUI 애플리케이션 등에서 사용자 응답성을 높일 수 있음 (ex. 백그라운드 처리)

- 단점
    - 동기화 문제: 여러 스레드가 같은 자원을 동시에 수정하면 문제가 발생 (→ race condition)
    - 디버깅 어려움: 흐름이 복잡해서 버그 추적이 힘듦
    - Deadlock 위험: 잘못된 자원 접근 순서로 인해 서로 대기 상태에 빠질 수 있음
    - Context Switching 비용: 너무 많은 스레드는 오히려 성능 저하 유발

3. 멀티스레딩 환경에서 주의해야 할 점은 무엇인가요? (예: race condition, deadlock)
- **Race Condition (경쟁 상태)**: 여러 스레드가 동시에 공유 자원을 읽고 쓰는 과정에서 순서가 뒤엉켜 예상치 못한 결과를 초래하는 문제 
    -  **해결:**  
        - `synchronized` 키워드 사용: 특정 메서드나 블록을 동기화하여, 동시에 한 스레드만 접근 가능하게 함
        ```java
        public class Counter {
            private int count = 0;

            public synchronized void increment() {
                count++; // 동기화된 메서드
            }
        }
        ```   

        - `Lock` 사용, 원자적 연산: 더 정교한 동기화 제어가 가능하며, timeout 설정 등 추가 기능 제공
        ```java
        Lock lock = new ReentrantLock();

        public void increment() {
            lock.lock();
            try {
                count++;
            } finally {
                lock.unlock(); // 반드시 해제
            }
        }
        ```   
- **Deadlock (교착 상태)**: 두 개 이상의 스레드가 서로가 가진 자원을 기다리며 무한 대기 상태에 빠짐.
    - **해결:** 
        - 자원 접근 순서를 명확히 고정: 모든 스레드가 동일한 순서로 자원에 접근하도록 설계
        ```java
        // 예: 항상 A -> B 순서로 Lock 획득
        synchronized(lockA) {
            synchronized(lockB) {
                // 작업
            }
        }
        ```   

        - `tryLock` 사용: 자원 획득 실패 시 타임아웃 또는 우회 가능     
        ```java
        if (lock1.tryLock(100, TimeUnit.MILLISECONDS)) {
            try {
                if (lock2.tryLock(100, TimeUnit.MILLISECONDS)) {
                    try {
                        // 작업 수행
                    } finally {
                        lock2.unlock();
                    }
                }
            } finally {
                lock1.unlock();
            }
        }
        ```   
- **Starvation (기아 상태)**: 낮은 우선순위의 스레드가 자원을 계속 획득하지 못해 실행되지 못하는 현상
    - **해결:** 
        - 공정한 락 정책 (`ReentrantLock` with fairness): ReentrantLock에서 공정성 설정 (fair = true)
        
        ```java
        Lock lock = new ReentrantLock(true); // FIFO 방식으로 lock 획득

        // true 설정 시 lock 요청 순서대로 접근 가능
        ```    
- **Context Switching 비용**: 스레드가 너무 많으면 CPU가 스레드를 자주 교체해야 하므로 오히려 성능이 저하 유발
    - **해결:** 
        - Thread Pool 사용 (Executors): 스레드 수를 제한하고 재사용 가능하게 하여 불필요한 생성/제거 방지

        ```java
        ExecutorService executor = Executors.newFixedThreadPool(10);

        for (int i = 0; i < 100; i++) {
            executor.submit(() -> {
                // 작업
            });
        }
        ``` 
        - 병렬성 수준 조정: 하드웨어(코어 수)에 따라 적절한 스레드 수 설정
        - 스레드 생성 대신 비동기 처리 고려: IO 중심 작업은 CompletableFuture, WebFlux, Project Reactor 등의 비동기 방식이 더 적합할 수 있음

## 📅 2025/05/28
### 4. 프로그램이 실행될 때 메모리 구조(스택, 힙, 데이터 영역, 코드 영역)를 설명해 주세요.
- 코드 영역: 실행할 프로그램의 기계어 코드
    - 읽기 전용으로 설정되는 경우가 많아 보안성 향상 (실행 중 수정 불가 → 바이러스 방지)
    - 실행 파일이 메모리에 올라올 때 이 영역에 로드됨
    - 메모리 관리는 운영체제가 로딩 시 자동으로 할당
        - 정적(Static): 실행 중에는 크기 변경 없음
- 데이터 영역: 전역 변수, 정적 변수 저장 
    - 초기값이 있는 전역/정적 변수 → 데이터 세그먼트
    - 초기값이 없는 전역/정적 변수 → BSS 세그먼트
    - 특징
        - 프로그램 시작 시 할당되고 종료 시 해제됨 (전역적 생명 주기)
        - 프로세스마다 독립적으로 존재 (다른 프로세스에 영향 없음)
    - 메모리 관리는 실행 시 OS가 한 번만 할당
        - JVM에서는 PermGen or Metaspace가 일부 역할
- 힙 영역: 동적 할당된 객체 (new 등)
    - 크기가 유동적 (사용자가 필요 시 할당, 명시적 해제 필요 – Java는 GC가 수행)
    - 속도가 느림 (할당/해제 비용 큼)
    - 참조 타입(객체, 배열 등)이 저장됨
    - 메모리 관리는 개발자가 직접 할당 (new)
- 스택 영역: 함수 호출, 지역 변수, 매개변수 등
    - Last In First Out (LIFO) 구조
    - 함수 호출 시 프레임이 쌓이고, 리턴되면 제거됨
    - 자동으로 할당 및 해제 → 빠름
    - 재귀 호출이 많거나 무한 루프 → Stack Overflow 발생 (크기가 제한되어 있음)
    - 메모리 관리는 호출 시 자동 할당, 함수 종료 시 자동 해제

### 5. Stack Overflow란 무엇인가요?
- 스택 영역이 넘쳐 함수 호출이 너무 깊거나 무한 재귀로 인해 발생하는 오류

### 6. Heap 메모리는 언제 사용하나요?
- 객체 생성 시 사용 (new 키워드)
- 크기가 가변적이고 수명이 동적인 데이터에 적합

## 📅 2025/06/12