1. CI(지속적 통합), 지속적 전달(Continuous Delivery), 지속적 배포(Continuous Deployment)의 차이는 무엇인가요? (각 개념의 정의와 차이점)
   **CI**는 지속적 통합(Continuous Integration)의 약자로 개발자들이 작성한 코드를 하나의 중앙 저장소에 자주 통합하고,
   그 과정에서 자동으로 빌드와 테스트를 수행하는 개발 문화이자 자동화 시스템입니다.
   코드가 변경될 때마다 빠르게 통합 및 검증을 진행함으로써, 코드 충돌을 줄이고 품질을 일정 수준 이상으로 유지할 수 있습니다.
   **지속적 전달**은 CI 이후의 단계로, 빌드와 테스트를 거친 애플리케이션을 운영 환경에 배포 가능한 상태로 지속적으로 유지하는 것입니다. 배포 자체는 시스템이 아닌 사람이 승인해야 이루어지지만, 그 직전까지의 과정(코드 -> 빌드 -> 테스트 -> 스테이징)은 모두 자동화되어 있습니다. 즉 지금 즉시 배포를 할 수 있는 상태인지 물을 때 바로 가능한 상태를 의미합니다.
   **지속적 배포**는 지속적 전달보다는 한 단계 더 나아간 개념으로 검증이 끝난 코드가 운영 환경에까지 자동으로 배포되도록 하는 방식입니다. 즉, 사람이 별도로 승인하지 않아도, 모든 테스트를 통과한 변경사항은 자동으로 운영 환경에 반영됩니다.
   이 방식은 자동화 수준이 가장 높지만, 충분한 테스트 커버리지와 모니터링이 전제되어야 합니다.

2. RESTful API란 무엇이며, 하나의 리소스를 설계할 때 지켜야 할 베스트 프랙티스에는 무엇이 있는지 설명해주세요.
   (예: 엔드포인트 구성, HTTP 메서드/상태코드 활용, 버전 관리 등)
   웹의 기본 구조인 HTTP를 기반으로 자원을 URI로 명확하게 표현하고, 표준 HTTP 메소드를 통해 해당 자원을 조작하는 아키텍쳐 스타일입니다. 이러한 원칙을 따르는 API를 RESTful API라고 하며, 주로 웹 서비스의 일관성, 확장성, 이해 용이성을 높이기 위해 사용됩니다.
   리소스 설계시 지켜야할 베스트 프레틱스에는 세가지가 있습니다.
   첫번째, 엔드포인트 구성시 리소스를 명사로 표현해야합니다.
   /users /users/{id}와 같이 표현해야합니다.
   두번째, HTTP 메서드를 의미에 맞게 활용해야 합니다.

   ##

   GET /users → 사용자 목록 조회
   GET /users/1 → 사용자 상세 조회
   POST /users → 사용자 생성
   PUT /users/1 → 사용자 전체 수정
   PATCH /users/1 → 사용자 일부 수정
   DELETE /users/1 → 사용자 삭제

   ##

   세번째, HTTP 상태 코드를 일관되게 활용해야합니다.
   클라이언트가 API 결과를 해석할 수 있도록
   성공시에는 200 Ok, 201 Created, 잘못된 요청에는 400 Bad Request, 인증 실패는 401 Unauthorized 등 표준 HTTP 응답 코드를 의미에 맞게 반환해야 합니다.

3. 마이크로서비스 아키텍처(MSA)와 모놀리식 아키텍처의 장단점을 비교해보세요.
   (예: 배포/스케일링 유연성, 복잡도, 운영상의 어려움 등)
   모놀리식 아키텍쳐는 애플리케이션 안에 모든 기능이 통합된 구조입니다. 하나의 프로젝트 안에 모든 비즈니스 로직이 함께 존재하며 빌드 배포도 하나의 단위로 처리됩니다. 이 방식은 초기 개발과 테스트가 단순하고 하나의 코드베이스로 전체 로직을 파악하기 쉬워 소규모 팀이나 초기 서비스에 적합합니다.
   하지만 큰 규모의 경우 코드가 복잡해지고 하나의 기능만 수정해도 전체 시스템을 다시 빌드하고 배포해야 하므로 유지보수와 배포 리스크가 커집니다. 또한 특정 기능만 스케일링하거나 장애 격리하기 어렵고, 기술 스택도 하나로 통일되어야하는 제약이 있습니다.
   반면 마이크로 아키텍처는 기능을 독립적인 서비스 단위로 나누어 각 서비스가 개발, 배포, 확장, 장애 복구가 가능한 구조입니다.
   예를 들어 주문, 결제, 회원 관리를 각각의 서비스로 나누어 관리를 할 수 있습니다.
   이 구조의 장점은 배포와 스케일링의 유연하다는 점입니다. 또한 기술스택을 서비스별로 선택을 할 수 있습니다.
   다만 서비스 간 통신이 API 또는 메시지 브로ㅜ커 등으로 이루어지기 때문에 네트워크 복잡도와 장애 처리 로직이 필요합니다.
   또한 트랜잭션 처리, 모니터링, 로그 통합, 배포 작업이 복잡해져 DevOps 인프라에 대한 이해도의 수준이 높아야합니다.

   # 📅 2025/05/29

4. SOLID 원칙이란 무엇이며, 각각의 원칙과 소프트웨어 유지보수성/유연성과의 관계를 설명해주세요.
   SOLID 원칙은 객체지향 설계에서 코드의 유지보수성과 유연성을 높이기 위해 제안된 5가지 대표적인 설계 원칙입니다.
   각 원칙은 다음과 같습니다.

   **SRP(단일 책임 원칙)**:
   한 클래스는 하나의 책임만 가져야 합니다. 이를 지키면, 특정 기능의 변경이 다른 기능에 영향을 주지 않아 유지보수가 쉬워집니다.

   **OCP(개방-폐쇄 원칙)**:
   소프트웨어는 확장에는 열려 있고, 기존 코드 변경에는 닫혀 있어야 합니다. 즉, 기존 코드를 수정하지 않고 새로운 기능을 쉽게 추가할 수 있어서 유연한 설계가 가능합니다.

   **LSP(리스코프 치환 원칙)**:
   자식 클래스가 부모 클래스의 역할을 대체할 수 있어야 합니다. 이 원칙을 지키면 상속 구조에서 예기치 못한 오류를 방지할 수 있어, 안정적으로 기능을 확장하고 유지보수할 수 있습니다.

   **ISP(인터페이스 분리 원칙)**:
   하나의 커다란 인터페이스보다, 여러 개의 구체적이고 작은 인터페이스로 분리하는 것이 좋습니다. 불필요한 의존성이 줄어들어, 변경에 대한 영향을 최소화할 수 있습니다.

   **DIP(의존 역전 원칙)**:
   구체적인 구현체가 아니라, 추상화(인터페이스나 추상 클래스)에 의존해야 합니다. 이를 통해 코드의 결합도를 낮추고, 유연한 구조로 변경과 확장이 용이해집니다.

5. 합성(Composition)과 상속(Inheritance)의 차이를 설명하고, 각각을 어떤 상황에서 사용하는 것이 적절한지 이야기해주세요.
   합성과 상속은 객체지향에서 코드 재사용성을 높이기 위한 두 가지 방법입니다.

   **상속(Inheritance)**은 기존 클래스를 확장하여 새로운 클래스를 만드는 방식입니다.
   상위 클래스의 모든 필드와 메서드를 하위 클래스가 물려받기 때문에, 공통 동작을 여러 클래스에서 재사용할 때 적합합니다.
   하지만 상속 구조가 복잡해지면 코드가 강하게 결합되어 변경에 취약해질 수 있습니다.

   **합성(Composition)**은 기존 클래스의 인스턴스를 새로운 클래스의 멤버로 포함시켜 기능을 사용하는 방식입니다.
   합성은 유연하게 객체의 행동을 바꿀 수 있고, 런타임에 동적으로 기능을 조합할 수 있다는 장점이 있습니다.
   결합도가 낮아 유지보수성이 더 높고, 변경에 유연하게 대응할 수 있습니다.

   적절한 사용 상황을 말씀드리면,
   ‘is-a’ 관계가 명확하고, 부모 클래스의 기능을 그대로 확장할 때는 상속을 사용합니다.

   ‘has-a’ 관계이거나, 기능을 동적으로 조합하거나 유연하게 변경하고 싶을 때는 합성을 사용하는 것이 적합하다고 생각합니다.

6. 단위 테스트(Unit Test), 통합 테스트(Integration Test), 기능 테스트(Functional Test) 각각의 차이와 목적은 무엇인가요?
   **단위 테스트(Unit Test)**:
   가장 작은 단위인 함수나 메서드, 클래스와 같은 단일 구성요소가 올바르게 동작하는지 검증합니다.
   목적은 코드의 개별 동작이 정확한지 빠르게 확인하는 것입니다.

   **통합 테스트(Integration Test)**:
   여러 개의 모듈이나 컴포넌트가 서로 연동될 때, 정상적으로 작동하는지 검증합니다.
   데이터베이스, 외부 API 등과의 연결이 올바른지 확인하는 데 중점을 둡니다.

   **기능 테스트(Functional Test)**:
   실제 사용자 입장에서 소프트웨어의 전체 기능이 요구사항대로 동작하는지 검증합니다.
   주로 UI 또는 API 단에서 사용자의 시나리오를 따라 테스트합니다.

   정리하자면,
   단위 테스트는 코드의 최소 단위를,
   통합 테스트는 여러 컴포넌트 간의 상호작용을,
   기능 테스트는 전체 시스템의 동작을 검증한다는 점에서 차이가 있습니다.

## 📅 2025/06/14

7. Heap 메모리는 언제 사용하나요?
   Heap메모리는 JVM에서 객체를 동적으로 생성할 때 사용하는 메모리 영역으로 애플리케이션 실행 중 new키워드로 생성되는 객체들이 저장된다.

   Heap특징

   1. GC가 관리한다.
   2. 메서드가 종료되어도 객체가 참조되고 있다면 살아있다.
   3. 접근 속도가 Stack보다 느리다.

   사용 시점

   - new 키워드로 객체 생서이, 객체는 Heap에 저장, 참조는 Stack에 저장된다.
   - 클래스의 인스턴스 변수 저장 시, 인스턴스 필드들은 Heap영역에 할당된다.
   - 메서드 실행 간 객체가 계속 필요한 경우, DB 연결, 캐시 객체 등은 메서드 종료 후에도 유지된다.
   - 대용량 객체나 배열 등, 크기가 큰 데이터도 Heap에 저장된다.

8. Git에서 merge와 rebase의 차이는 무엇이며, 각각을 언제 사용하는 것이 적절한가요?
   공통점

   1. 브랜치 통합을 위한 방법이다.
   2. 협업 시 기능 브랜치와 메인 브랜치를 병합할 때 사용한다.

   차이점
   | 항목 | `merge` | `rebase` |
   | ----- | ---------------------------- | ---------------------------- |
   | 히스토리 | **그대로 유지**, 브랜치 병합 기록이 남음 | **히스토리가 깔끔함**, 커밋들이 재정렬됨 |
   | 커밋 로그 | 병합 커밋(Merge commit) 생김 | 병합 커밋 없이 **기존 커밋이 재작성**됨 |
   | 충돌 처리 | 충돌은 한 번만 발생 | 충돌이 여러 커밋에서 발생할 수 있음 |
   | 작업 방식 | 두 브랜치의 끝을 합치는 방식 (`--no-ff`) | 내 커밋들을 베이스 브랜치 위로 **다시 붙이기** |

   사용시점

   - 협업 중 작업 병합: merge
     히스토리를 보존하며 작업 흐름 추적이 가능하다
     개인 브랜치 정리 후 Push: rebase
     줄기를 하나로 합쳐서 깔끔한 커밋 히스토리를 유지한다

9. 트랜잭션의 ACID 특성이란 무엇이며, 각각(원자성, 일관성, 격리성, 지속성)이 의미하는 바는 무엇인가요?

   트랜잭션
   데이터베이스에서 하나의 작업 단위로 수행되는 일련의 연산 집합이다. 모든 연산이 모두 성공하거나 모두 실패해야한다.

   ACID
   Atomicity(원자성): 트랜잭션 내 모든 작업은 하나의 단위로 실행, 일부만 수행되는 일은 없다
   Consistency(일관성): 트랜잭션 수행 전후 DB의 제약 조건 및 규칙은 항상 만족 해야 한다
   Isolation(격리성): 여러 트랜잭션이 동시에 실행되어도 서로 간섭없이 독립적으로 실행되어야한다
   Durability(지속성): 트랜잭션이 성공적으로 완료되면 그 결과는 영구적으로 저장된다
