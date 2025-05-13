# 📅 2025/05/13
# 프로세스(Process)와 스레드(Thread)의 차이는 무엇인가요?

## 프로세스(Process)
- **프로세스**는 운영체제에서 자원을 할당받는 **작업의 단위**로, 서로 메모리를 독립적으로 가진다.

## 스레드(Thread)
- **스레드**는 코드 **실행 흐름의 단위**로, 하나의 프로세스 안에 여러 스레드가 존재하며 같은 메모리를 공유한다.


| 항목 | 프로세스 (Process) | 스레드 (Thread) |
|------|----------------------|-------------------|
| 정의 | 실행 중인 프로그램의 인스턴스 | 프로세스 내에서 실행되는 작업의 흐름 |
| 메모리 공간 | 독립된 메모리 공간 사용 | 프로세스 내 자원을 공유 |
| 자원 공유 | 서로 자원 공유 불가 | 메모리, 파일, 자원 공유 |
| 생성 비용 | 상대적으로 큼 | 상대적으로 작음 |
| 안정성 | 하나의 프로세스가 종료되어도 다른 프로세스에는 영향 없음 | 하나의 스레드가 문제 생기면 전체 프로세스에 영향 줄 수 있음 |
| 예시 | Chrome 브라우저의 여러 창 | Chrome의 각 탭에서 작동하는 스레드 |


--- 

# 스레드를 사용하면 어떤 이점이 있나요? 단점은요?

## 스레드(Thread)의 장점
1. 응답성(성능) 향상 : 스레드 간의 작업 분할과 병렬 처리로 인해 사용자가 응용 프로그램을 원활하게 사용하는데 빠른 응답성(결과)를 제공할 수 있다
2. 자원 공유 효율성 향상 : 스레드는 하나의 프로세스 내에서 실행되기 때문에, 프로세스의 자원을 공유하여 접근할 수 있다. 그리고 스레드는 프로세스 내부에 있기 때문에 별도의 메모리 공간을 할당할 필요없이, 프로세스 내부에서 데이터를 관리하면 된다. (thread stack 공간에서 데이터 관리)
3. 동시성 : 여러 개의 스레드가 동시에 실행될 수 있어서, **작업 병렬 처리 가능**
4. 간결성 : 작업을 분리할 수 있어 코드가 간결해질 수 있다

## 스레드(Thread)의 단점
1. 스레드 간의 상호간섭 : 멀티 스레드(여러 스레드 사용)가 실행 중인 상황에, 스레드 간의 상호간섭 문제가 발생할 수 있다. 프로세스는 한 개가 다운되면, 그 프로세스만 작업이 멈추고 다른 프로세스에는 영향이 가지 않는다. 하지만 스레드는 다른 스레드가 작업을 방해하거나, 스레드간의 우선 순위 설정에 문제가 있을 경우 **서로에게 영향을 미치기 때문에** 예상치 못한 이슈 발생
2. 성능 저하 : 스레드를 많이 생성하면 성능 저하가 발생할 수 있다. 스레드들이 병렬로 실행되기 위해 컨텍스트 스위칭이 빈번하게 발생하기 때문
3. 동기화 이슈 : **여러 스레드가 공유 자원에 동시에 접근할 때, 동기화 문제 발생 가능**
4. 자원 소비 : 스레드는 개별적인 실행 흐름을 가지기 때문에, 스레드마다 stack 및 레지스터 등의 메모리 자원을 소비한다. 따라서 스레드의 수가 증가하면 메모리 사용량도 증가하게 되어 시스템 자원이 한계에 도달할 수 있다

# 멀티스레딩 환경에서 주의해야 할 점은 무엇인가요? (예: race condition, deadlock)

## Race Condition(경쟁 상태)
- 여러 스레드가 공유 자원에 동시에 접근하여 실행 결과가 접근 순서에 따라 달라지는 현상
- => 해결 방법 : Semaphore, Atomic 연산 활용, Lock 메커니즘 구현

```java
public class Counter {
    private int count = 0;
    
    // 동기화 없음 - Race Condition 발생 가능
    public void increment() {
        count++;
    }
    
    // 동기화 적용 - Race Condition 방지
    public synchronized void safeIncrement() {
        count++;
    }
    
    public int getCount() {
        return count;
    }
}
```

## Deadlock (교착상태)
- 두 개 이상의 스레드가 서로 상대방의 작업이 끝나기를 기다리며 무한정 대기하는 상태
- => 해결 방법 : 자원 할당 순서 정하기(순환 대기 방지), 타임아웃 설정(무한 대기 방지), 데드락 감지 및 복구 메커니즘 구현

```java
public class DeadlockExample {
    private static final Object resource1 = new Object();
    private static final Object resource2 = new Object();

    // 데드락 발생 가능성 있는 코드
    public static void deadlockRisk() {
        Thread t1 = new Thread(() -> {
            synchronized(resource1) {
                System.out.println("Thread 1: resource1 잠금");
                try { Thread.sleep(100); } catch (InterruptedException e) {}
                synchronized(resource2) {
                    System.out.println("Thread 1: resource2 잠금");
                }
            }
        });
        
        Thread t2 = new Thread(() -> {
            synchronized(resource2) {
                System.out.println("Thread 2: resource2 잠금");
                try { Thread.sleep(100); } catch (InterruptedException e) {}
                synchronized(resource1) {
                    System.out.println("Thread 2: resource1 잠금");
                }
            }
        });
        
        t1.start();
        t2.start();
    }
    
    // 데드락 방지 코드 - 자원 획득 순서 통일
    public static void deadlockPrevention() {
        Thread t1 = new Thread(() -> {
            synchronized(resource1) {
                System.out.println("Thread 1: resource1 잠금");
                try { Thread.sleep(100); } catch (InterruptedException e) {}
                synchronized(resource2) {
                    System.out.println("Thread 1: resource2 잠금");
                }
            }
        });
        
        Thread t2 = new Thread(() -> {
            synchronized(resource1) {  // 순서 통일: 항상 resource1 먼저 잠금
                System.out.println("Thread 2: resource1 잠금");
                try { Thread.sleep(100); } catch (InterruptedException e) {}
                synchronized(resource2) {
                    System.out.println("Thread 2: resource2 잠금");
                }
            }
        });
        
        t1.start();
        t2.start();
    }
```