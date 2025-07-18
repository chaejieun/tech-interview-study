# 📅 2025/05/15
# CI(지속적 통합), 지속적 전달(Continuous Delivery), 지속적 배포(Continuous Deployment)의 차이는 무엇인가요? (각 개념의 정의와 차이점)

## CI (Continuous Integration)
- 빌드/테스트 자동화 과정. CI는 개발자를 위한 자동화 프로세스인 **지속적 통합(Contiunos Integration)**을 의미. 
- 지속적 통합의 실행은 소스/버전 관리 시스템에 대한 변경 사항을 정기적으로 커밋하여 모든 사람에게 동일 작업 기반을 제공하는 것.
- 커밋할 떄마다 빌드와 일련의 자동 테스트가 이뤄져 동작을 확인하고 변경으로 인해 문제가 생기는 부분이 없도록 보장.

## CD (Continuous Delivery) 
- CI 이후, **프로덕션 외 환경(스테이징 등)에 자동 배포**까지 진행하는 프로세스
- 배포를 언제든지 버튼 한 번으로 안정적으로 할 수 있도록 준비된 상태 유지.


## CD (Continuous Deployment)
- **프로덕션 배포 단계를 자동화**하는 DevOps 방식을 논리적 극한으로 끌어올린다.
- 코드 변경이 파이프라인의 이전 단계를 모두 성공적으로 통과하면 수동 개입 없이 해당 변경 사항이 프로덕션에 자동으로 배포.
- 지속적 배포를 채택하면 품질 저하 없이 최대한 빨리 사용자에게 새로운 기능을 제공할 수 있음.

--- 

# RESTful API란 무엇이며, 하나의 리소스를 설계할 때 지켜야 할 베스트 프랙티스에는 무엇이 있는지 설명해주세요. (예: 엔드포인트 구성, HTTP 메서드/상태코드 활용, 버전 관리 등)

# RESTful한 리소스 설계 시 Best Practice
1. URI 설계
-  명사(리소스) 기반 (동사 X)  ex) /orders, /users 사용
-  동사(액션) 사용 자제 ex)/create-order 자제
-  파일 확장자 포함 금지 ex ).json, .xml 금지

2. HTTP 메소드 활용
### CRUD 연산 매핑
- `GET`: 리소스 조회, 리소스 컬렉션 조회
- `POST`: 리소스 생성
- `PUT` : 리소스를 완전히 대체
- `PATCH` : 리소스의 일부를 변경
- `DELETE` : 리소스를 삭제

### HTTP 상태 코드 사용
| 상태 코드 | 의미                    | 예시 상황                     |
| ----- | --------------------- | ------------------------- |
| 200   | OK                    | 조회 성공, 삭제 성공              |
| 201   | Created               | 리소스 생성 성공                 |
| 204   | No Content            | 성공했으나 반환할 컨텐츠 없음 (DELETE) |
| 400   | Bad Request           | 잘못된 요청 파라미터               |
| 401   | Unauthorized          | 인증 필요                     |
| 403   | Forbidden             | 접근 권한 없음                  |
| 404   | Not Found             | 리소스 없음                    |
| 409   | Conflict              | 중복 리소스 생성 요청              |
| 500   | Internal Server Error | 서버 에러                     |


3. 리소스 표현
- 리턴 값: 리소스 생성 또는 수정 시, 새 리소스 표현 또는 수정된 리소스 표현을 반환
- 하위 리소스: 리소스를 표현할 때 하위 리소스에 대한 링크를 포함할 수 있습니다. 예를 들어, 사용자를 조회할 때 사용자에게 관련된 주문 리소스에 대한 링크를 포함할 수 있습니다. 
- Content-Type 명시: 응답에 포함되는 데이터의 형식(예: application/json, application/xml)을 Content-Type 헤더에 명시

### ✨ 추가 질문 포인트
#### 조회의 경우 POST를 사용 못하나요? 
- 복잡한 쿼리 조건 전달이 필요할 때 / 보안 또는 민감한 데이터를 포함할 때(주민번호,토큰) / 검색 요청 로그를 남기거나 기록성 요청일 때

--- 

## 마이크로서비스 아키텍처(MSA)와 모놀리식 아키텍처의 장단점을 비교해보세요. (예: 배포/스케일링 유연성, 복잡도, 운영상의 어려움 등)

### 모놀리식 아키텍처(Monolithic Architecture, MA)
- 하나의 통합된 코드 베이스로 여러 비즈니스 기능을 수행하는 전통적인 소프트웨어 개발 모델. **단일 애플리케이션 내에 서비스의 모든 로직이 통으로 들어가 있는 구조**
-  중앙 집중된 구조이기 때문에 분산된 애플리케이션에 비해 엔드 투 엔드 테스트(End-to-End, E2E: 사용자 관점에서 애플리케이션의 흐름을 처음부터 끝까지 테스트하는 것)를 더 빠르게 수행할 수 있다


### 모놀리식 아키텍처(Monolithic Architecture, MA) 장점
- 단순하고 통일성 있는 구조
- 단일 코드베이스 -> 간편한 개발 
- 빠르고 편한 E2E 테스트
- 손쉬운 모니터링, 디버깅

### 모놀리식 아키텍처(Monolithic Architecture, MA) 단점
- 유지 보수 및 안정성 문제
- 느린 개발 및 배포 속도
- 위축된 확장성
- 기술 유연성 낮음 (스택 제한)

### 모놀리식 아키텍처(Monolithic Architecture, MA) 적합한 경우?
- 기술적 복잡도가 낮은 소규모 프로젝트
- MVP 수준의 단일 비즈니스 또는 신설 도메인 등
- 시장 진입을 위해 빠르고 간편하게 기능 개발 및 배포를 수행해야 할 때


### 마이크로서비스 아키텍처(MicroService Architecture, MSA)
- 서비스를 아주 작은 서비스(Microservice) 단위로 나눠 **각 서비스에서 독립적으로 서비스를 구성하는 모델** 
- 중앙 집중적인 관리 체계 대신 경량화된 API나 메세지로 직접 통신하며 접근하는 방식
- 배포가 빠르고 잦은 만큼 애자일 작업 방식을 취하기도 편리
- 일부분에 문제가 생기면 시스템 전체가 다운될 수 있는 모놀리식 아키텍처와 달리, 한 서비스가 다운되더라도 다른 서비스는 문제없이 작동 가능
- 자체 DB를 서비스마다 가지고 있어서 데이터 무결성을 유지하는 데도 도움


### 마이크로서비스 아키텍처(MicroService Architecture, MSA) 장점
- 유연한 확장성
- 더 민첩한 배포 주기
- 유지 관리 안정성
- 기술 유연성 높음(서비스별 독립적인 스택 선정 가능)

### 마이크로서비스 아키텍처(MicroService Architecture, MSA) 단점
- 복잡한 구조, 높은 구현 난이도
- 모니터링, 디버깅, 통합 테스트가 어려움
- 인프라 및 자원, 인력에 드는 막대한 비용
- 까다로운 DB 트랜잭션 관리

### 마이크로서비스 아키텍처(MicroService Architecture, MSA) 적합한 경우?
- 기술적 복잡도가 높은 대규모 프로젝트
- 다양한 기술 스택을 사용하고, 여러 비즈니스별 요구사항이 명확한 경우
- 장애를 줄이고 시스템 전체의 가용성과 탄력성을 높여야 할 때


---

# 📅 2025/05/29
# SOLID 원칙이란 무엇이며, 각각의 원칙과 소프트웨어 유지보수성/유연성과의 관계를 설명해주세요.

## 1. Single Responsibility Principle (SRP): 단일 책임 원칙
- 하나의 클래스는 오직 하나의 책임, 즉 하나의 변경 이유만을 가져야 합니다. 만약 클래스가 여러 책임을 가지게 되면, 하나의 책임을 변경할 때 다른 책임에 영향을 줄 가능성이 높아집니다.
- 유지보수성 향상 : 클래스가 하나의 책임만 가지므로, 해당 책임의 변경 사항이 다른 부분에 미치는 영향이 적어짐. 따라서, 특정 기능을 수정하거나 버그를 해결할 대 다른 코드 부분을 건드릴 위험이 줄어들어 유지보수가 쉬어진다.
- 유연성 증대 : 각 책임이 분리되어 있으므로, 특정 기능을 변경하거나 새로운 기능을 추가할 때 기존 코드에 미치는 영향을 최소화하면서 독립적으로 작업할 수 있다. 

## 2. Open/Closed Principle (OCP): 개방-폐쇄 원칙
- 기존 코드를 수정하지 않고도 기능을 확장할 수 있도록 설계해야 한다. 이는 추상화와 다형성을 통해 달성할 수 있다
- 유지보수성 향상 : 기존 코드를 수정하지 않고 새로운 기능을 추가할 수 있으므로, 이미 테스트 되고 안정화된 코드를 건드릴 필요가 없어 잠재적인 버그 발생 위험을 줄인다.
- 유연성 증대 : 새로운 요구사항이 발생했을 때, 기존 코드를 변경하는 대신 새로운 클래스를 추가하여 기능을 확장할 수 있다. 이는 시스템을 더욱 유연하게 만들어 변화에 쉽게 대응할 수 있도록 한다.

## 3. Liskov Substitution Principle (LSP): 리스코프 치환 원칙
- 부모 클래스의 인스턴스를 사용하는 코드에서 자식 클래스의 인스턴스로 대체해도 프로그램의 정확성이 깨지지 않아야 한다. 즉, 서브타입은 슈퍼타입의 행위를 보존해야 한다.
- 유지보수성 향상 : 상위 타입의 인터페이스를 따르는 하위 타입은 언제든지 교체 가능하므로, 코드의 일관성을 유지하고 예측 가능성을 높여 유지보수를 용이하게 한다.
- 유연성 증대 : 다형성을 활용하여 다양한 하위 타입의 객체를 일관된 방식으로 처리할 수 있게 되어 코드의 재사용을 높이고, 새로운 하위 타입을 쉽게 추가할 수 있어 시스템의 유연성을 향상시킨다.

## 4. Interface Segregation Principle (ISP): 인터페이스 분리 원칙
- 하나의 거대한 인터페이스 대신, 클라이언트에게 필요한 메소드만을 제공하는 여러 개의 작은 인터페이스로 분리해야 한다.
- 유지보수성 향상 : 불필요한 메소드에 의존하지 않으므로, 특정 인터페이스의 변경이 다른 클라이언트에 미치는 여향을 최소화하여 시스템의 안정성을 높이고 유지보수를 용이하게 한다.
- 유연성 증대 : 각 클라이언트에 필요한 인터페이스만 제공함으로써 시스템의 결합도를 낮추고, 각 컴포넌트가 독립적으로 변화하고 발전할 수 있도록 하여 유연성을 높인다.

## 5. Dependency Inversion Principle (DIP): 의존성 역전 원칙
- 구체적인 구현에 의존하는 대신, 추상화(인터페이스나 추상 클래스)에 의존하도록 설계해야 한다. 이를 통해 고수준 모듈과 저수준 모듈 사이의 결합도를 낮출 수 있다
- 유지보수성 향상 : 고수준 모듈이 저수준 모듈의 구체적인 구현에 의존하지 않으므로, 저수준 모듈의 변경이 고수준 모듈에 미치는 영향을 줄여 유지보수를 용이하게 한다
- 유연성 증대 : 추상화에 의존함으로써 다양한 구현체를 쉽게 교체하거나 확장할 수 있게 되어 시스템의 유연성을 높인다. 또한, 단위테스트를 용이하게 만들어 코드의 품질을 향상시키는 데 도움이 된다.

<br>

# 합성(Composition)과 상속(Inheritance)의 차이를 설명하고, 각각을 어떤 상황에서 사용하는 것이 적절한지 이야기해주세요.

# 상속(Inheritance) : IS-A 관계
- 상속은 한 클래스가 다른 클래스의 속성과 메소드를 물려받는 것. 하위 클래스는 상위 클래스의 특성을 포함하며, 필요에 따라 새로운 속성이나 메소드를 추가하거나 기존의 것을 오버라이드(override)할 수 있다. 
- A는 B이다 (IS-A) 관계를 모델링하는 데 적합

## 상속의 특징
- 강한 결합(tight coupling) : 하위 클래스는 상위 클래스에 강하게 의존하게 된다. 상위 클래스의 변경은 하위 클래스에 영향을 미칠 수 있다.
- 코드 재사용 용이 : 상위 클래스의 기능을 그대로 물려받아 코드 중복을 줄일 수 있다
- 컴파일 타임 관계 : 상속 관계는 컴파일 시점에 결정

# 합성(Composition) : HAS-A 관계
- 합성은 한 클래스의 인스턴스를 다른 클래스의 속성으로 포함시켜 기능을 재사용하는 방식.  
- A는 B를 가진다(HAS-A) 관계를 모델링하는데 적합하다

## 합성의 특징
- 느슨한 결합(loose coupling) : 포함하는 클래스는 포함되는 클래스에 대한 직접적인 의존성이 적다. 포함되는 클래스의 변경이 포함하는 클래스에 미치는 영향이 상대적으로 적다
- 유연성 증대 : 실행 시간에 객체의 구성을 동적으로 변경할 수 있다
- 코드 재사용 및 조합 용이 : 여러 객체의 기능을 조합하여 더 복잡한 기능을 구현할 수 있다

## 상속이 적절한 경우
1. 클래스 간에 명확한 "IS-A" 관계가 존재할 때 (예: 개는 동물이다).
2. 상위 클래스의 인터페이스를 하위 클래스가 그대로 확장하고 싶을 때.
3. 기존 클래스의 기본 동작을 크게 변경하지 않고 일부 특성을 특화하고 싶을 때.
4. 클래스 계층 구조가 비교적 안정적일 때.

## 합성이 적절한 경우
1. 클래스 간에 "HAS-A" 관계가 더 자연스러울 때 (예: 자동차는 엔진을 가진다).
2. 코드 재사용보다는 유연성과 낮은 결합도를 중요시할 때.
3. 실행 시간에 객체의 행동을 동적으로 변경하고 싶을 때 (전략 패턴 등).
4. 다양한 기능들을 조합하여 새로운 기능을 만들고 싶을 때.

<br>

# 단위 테스트(Unit Test), 통합 테스트(Integration Test), 기능 테스트(Functional Test) 각각의 차이와 목적은 무엇인가요?
## 단위 테스트(Unit Test)
- 개별적인 가장 작은 코드 단위(함수, 메소드, 클래스 등)
- 각 코드 단위가 **독립적으로** 정확하게 동작하는 지 검증. 외부 의존성(데이터베이스, 다른 모듈 등)은 보통 Mocking 또는 Stubbing을 사용하여 격리한다.

## 통합 테스트(Integration Test)
- 둘 이상의 **통합된** 컴포넌트 또는 모듈 간의 상호작용
- 여러 컴포넌트가 함께 올바르게 작동하는 지, 데이터가 정확하게 교환되는 지, 상호작용에 문제가 없는 지 검증

## 기능 테스트(Functional Test)
- **최종 사용자의 관점**에서 시스템의 특정 기능 전체
- 소프트웨어가 명세된 요구사항을 충족하는 지, 특정 입력에 대해 예상된 출력을 내는 지 검증. 
- 내부 구현 방식은 고려하지 않고 **결과**에 초점을 맞춘다.


# 📅 2025/06/13
# Heap 메모리는 언제 사용하나요?
- 힙(Heap) 메모리는 프로그램 실행 중에 **동적으로 할당되고 해제되는 데이터**를 저장하는 영역. 스택 메모리와 달리, 컴파일 시점이 아닌 **런타임 시점에 크기가 결정되고 관리**된다. 자바와 같은 가비지 컬렉션(GC) 언어에서는 주로 객체 인스턴스를 저장하는 데 사용.

1. 객체 인스턴스 (Object Instances) 생성 시
- `new String("Hello")`, `new MyObject();`
2. 동적 크기 데이터 구조를 다룰 때
3. 긴 수명을 가지는 데이터가 필요할 때
4. 여러 메서드 또는 여러 스레드 간에 공유되어야 할 데이터
5. 대량의 데이터를 다룰 때

- 힙 메모리는 프로그램이 실행되는 동안 생성되고 소멸되는 모든 객체와 동적으로 크기가 결정되는 데이터 구조를 저장하는 데 사용됩니다. 자바에서는 new 연산자를 통해 생성되는 모든 인스턴스가 힙에 할당된다고 생각하면 됩니다.


# Git에서 merge와 rebase의 차이는 무엇이며, 각각을 언제 사용하는 것이 적절한가요?

## Merge(병합)
- `git merge` 명령어는 두 브랜치의 변경 사항을 **새로운 커밋**을 생성하여 합친다. 이때, 두 브랜치의 기존 커밋 히스토리는 그대로 유지

## Merge(병합) 동작 방식
- `feature` 브랜치의 변경 사항을 `main` 브랜치로 병합한다고 가정해 봅시다.
- `main` 브랜치에서 `git merge feature` 명령을 실행하면, Git은 `main` 브랜치와 `feature` 브랜치의 공통 조상 커밋을 찾고, 각 브랜치에서 발생한 변경 사항들을 합쳐서 새로운 병합 커밋(`M`)을 생성합니다.

## Rebase(리베이스)
- `git rebase` 명령어는 현재 브랜치의 커밋들을 **다른 브랜치의 최신 커밋 위로 재배치**합니다. 이 과정에서 기존 커밋들은 사라지고 **새로운 커밋으로 재생성**됩니다. 결과적으로 선형(Linear)적이고 깔끔한 커밋 히스토리를 만들 수 있습니다.

## Rebase(리베이스) 동작 방식
`feature` 브랜치의 변경 사항을 `main` 브랜치 위로 리베이스한다고 가정해 봅시다.
`feature` 브랜치에서 `git rebase main` 명령을 실행하면:
    1. `feature` 브랜치와 `main` 브랜치의 공통 조상 커밋(B)을 찾습니다.
    2. `feature` 브랜치에만 있는 커밋들(D, E)을 임시 저장합니다.
    3. `feature` 브랜치를 `main` 브랜치의 최신 커밋(C)으로 이동시킵니다.
    4. 임시 저장했던 `feature` 브랜치만의 커밋들(D, E)을 `main` 브랜치의 최신 커밋(C) 위에 순서대로 다시 적용하여 새로운 커밋(D', E')을 생성합니다.

### ✨ 정리 포인트
일반적인 팀 환경에서는 `develop` 브랜치와 같은 공유 브랜치로 기능을 통합할 때 `merge`를 사용하고, 개발자 개개인의 `feature` 브랜치처럼 아직 공유되지 않은 로컬 브랜치를 `develop` 브랜치의 최신 상태로 업데이트하고 깔끔하게 만들고 싶을 때 `rebase`를 사용하는 것이 일반적입니다.

# 트랜잭션의 ACID 특성이란 무엇이며, 각각(원자성, 일관성, 격리성, 지속성)이 의미하는 바는 무엇인가요?
1. 원자성(Atomicity)
- 트랜잭션 내의 모든 연산은 마치 하나의 행위처럼 모두 성공하거나 실패해야 한다. 부분적으로만 반영되는 것은 허용되지 않는다.
2. 일관성(Consistency)
- 트랜잭션이 실행되기 전후에 데이터베이스의 상태는 항상 일관성을 유지해야 한다. 
3. 격리성(Isolation)
- 동시에 여러 트랜잭션이 실행되더라도, 각 트랜잭션은 마치 독립적으로 실행되는 것처럼 다른 트랜잭션의 영향을 받지 않아야 한다
4. 지속성(Durability)
- 트랜잭션이 성공적으로 커밋(Commit)된 후에는, 그 변경 사항이 영구적으로 데이터베이스에 반영되어야 합니다.

# 📅 2025/06/30
# 관계형 데이터베이스(SQL)와 NoSQL 데이터베이스의 차이점은 무엇이며, 각각 어떤 상황에서 더 적합한지 설명해주세요.

## 관계형 데이터베이스(Relational Database, RDBMS)
- 데이터를 행과 열로 구성된 테이블 형태로 저장하며, 각 테이블은 명확하게 정의된 스키마를 가진다.
- 테이블 간에 정의된 관계를 통해 데이터를 연결. 
- SQL을 사용하여 데이터를 조회, 삽입, 수정, 삭제하며 SQL은 강력한 데이터 조작 및 분석 기능을 제공하며, `JOIN` 연산을 통해 여러 테이블의 데이터를 결합할 수 있다.
- ACID를 보장하며, 주로 수직 확장(Scale-Up)에 적합하다. 

## NoSQL 데이터베이스 (Not Only SQL Database)
- 관계형 모델 외에 키-값, 문서, 칼럼, 그래프 등 다양한 방식으로 데이터를 저장한다.
- 스키마가 없거나 유연하여, 데이터 구조의 변경이 자유롭고 새로운 필드를 쉽게 추가할 수 있다.
- 주로 수평 확장(Scale-Out)에 적합하며, 대규모 분산 시스템 구축에 용이하다 
- 특정 유형의 데이터 액세스 패턴에서 매우 빠른 읽기/쓰기 성능을 제공한다. 특히 대규모 비정형 데이터를 처리하는 데 유리.

- SQL과 NoSQL 데이터베이스는 각각의 장단점을 가지고 있으므로, 애플리케이션의 특성과 요구사항에 따라 적절한 데이터베이스를 선택하는 것이 중요합니다. 때로는 두 가지 유형의 데이터베이스를 함께 사용하는 하이브리드 아키텍처가 최적의 솔루션이 될 수도 있습니다. 예를 들어, 핵심 비즈니스 로직과 관련된 중요 데이터는 관계형 데이터베이스에 저장하고, 실시간 분석이나 대용량 로그 데이터는 NoSQL 데이터베이스에 저장하는 방식입니다.


# 인덱스(index)란 무엇이며, 쿼리 성능을 어떻게 향상시키는지? 또한 인덱스 사용 시 주의할 점은 무엇인가요?
- 데이터베이스 테이블에 인덱스를 생성하면, 지정된 컬럼의 데이터를 미리 정렬하여 저장하거나, 데이터의 물리적인 위치를 가리키는 포인터를 함께 저장한다. 이렇게 하면 데이터베이스 관리 시스템이 데이터를 검색할 때 테이블의 모든 행을 하나씩 스캔하지 않고, 인덱스를 통해 필요한 데이터가 있는 위치로 바로 이동할 수 있게 된다.

## 쿼리 성능 향상
1. 빠른 데이터 검색 (WHERE절 성능 향상)
2. 정렬 작업 속도 향상 (ORDER BY절 성능 향상)
3. 조인 작업 속도 향상
4. 최소한의 데이터 읽기

## 인덱스 사용 시 주의할 점
1. 인덱스 추가 작업 부하 
    - 필요한 인덱스만 최소한으로 윶;
2. 추가적인 저장 공간 필요
    - 인덱스도 데이터이므로 디스크 공간을 차지한다. 
3. 인덱스 선택의 중요성
    - 컬럼 값의 중복도가 낮은 컬럼에 인덱스를 생성하는 것이 효과적. 
    - 복합 인덱스
4. 인덱스 무효화
5. 옵티마이저의 선택 

- 인덱스는 데이터 검색 속도를 비약적으로 향상시키지만, 데이터 변경 시 성능 저하와 추가 저장 공간 요구라는 Trade-off가 존재합니다. 따라서 시스템의 쿼리 패턴과 데이터 변경 빈도를 면밀히 분석하여 가장 효율적인 인덱스 전략을 수립하는 것이 중요합니다.

# SQL 쿼리가 느리게 동작할 때 문제를 진단하고 최적화하는 방법은 무엇인가요? (예: 실행 계획(EXPLAIN) 분석, 슬로우 쿼리 로그 확인 등)

1. 슬로우 쿼리 로그 확인
2. 실행 계획(Execution Plan 또는 EXPLAIN) 분석
3. 인덱스 최적화
    - 인덱스 무효화 원인 제거: WHERE 절에서 함수 사용, 데이터 타입 불일치, 부정형 조건, LIKE '%keyword'와 같은 패턴으로 인덱스가 사용되지 않는 경우, 쿼리 또는 데이터 모델을 수정하여 인덱스를 활용할 수 있도록 합니다.
4. 쿼리 재작성 및 최적화
    - 서브쿼리 대신 조인(JOIN) 사용: 경우에 따라 서브쿼리보다 조인이 더 효율적일 수 있습니다.
    - SELECT * 대신 필요한 컬럼만 선택
    - LIMIT 사용
5. 데이터베이스 통계 정보 갱신
6. 하드웨어 및 시스템 설정 최적화
7. 데이터 모델링 개선