1. Singleton 패턴에 대해서 설명해주세요.
   클래스의 인스턴스를 오직 하나만 생성하도록 보장하는 생성 패턴을 말합니다. 전역에서 이 인스턴스에 접근할 수 있도록 하며 공유 리소스나 설정 정보 등에 주로 사용됩니다.
   예시로는 DB커넥션 풀, 설정 파일 로더, 로깅 시스템 등이 있습니다.

2. Bridge 패턴에 대해서 설명해주세요.
   구현부와 추상부를 분리해서 서로 독립적으로 변경할 수 있도록 하는 구조 패턴입니다.

3. Strategy 패턴에 대해서 설명해주세요.
   행위를 캡슐화한 알고리즘들을 인터페이스로 정의하고, 런타임에 이 알고리즘들을 교체할 수 있도록 설계하는 행동 패턴입니다.

# 📅 2025/05/22

4. Builder 패턴에 대해서 설명해주세요.
   복잡한 객체(생성자에 파라미터가 많거나, 옵션이 다양한 객체)를 단계별로 나눠서 유연하고 가독성 있게 생성할 수 있도록 도와주는 생성 패턴입니다.
   장점은 필수 값과 선택 값을 구분하여, 원하는 값만 선택적으로 설정이 가능합니다. 코드가 읽기 쉽고, 생성 과정이 명확합니다.

```java
   Person p = new Person.Builder()
   .setName("홍길동")
   .setAge(20)
   .setAddress("서울")
   .build();
```

5. Factory Method 패턴에 대해서 설명해주세요.
   객체 생성 방법(로직)을 **서브클래스(구현체)**로 분리하여,상위 클래스에서는 객체 생성의 인터페이스만 정의하고 구체적인 객체 생성은 하위 클래스에서 결정하도록 만드는 생성 패턴입니다.
   장점은 새로운 객체 타입을 쉽게 추가할 수 있다는 점과 객체 생성 코드를 한 곳에 모아서 관리, 코드 수정이 유연하다는 것입니다.

```java
   abstract class AnimalFactory {
      abstract Animal createAnimal();
   }
   class DogFactory extends AnimalFactory {
      Animal createAnimal() { return new Dog(); }
   }
   class CatFactory extends AnimalFactory {
      Animal createAnimal() { return new Cat(); }
   }
   // 사용
   AnimalFactory factory = new DogFactory();
   Animal dog = factory.createAnimal();
```

6. 퍼사드 패턴에 대한 예를 들어주세요.
   퍼사드(Facade) 패턴은 여러 개의 복잡한 서브시스템(객체, API 등)을
   하나의 간단한 인터페이스로 감싸서, 외부에서는 복잡함을 모르고 쉽게 사용할 수 있도록 만드는 구조 패턴입니다.
   대표적인 실제 사례
   컴퓨터 전원 버튼: 버튼 하나로 CPU, 메모리, 디스크 등 여러 부품이 동시에 초기화됨

   ```java
   class CPU { void start() { ... } }
   class Memory { void load() { ... } }
   class Disk { void read() { ... } }

   class ComputerFacade {
      private CPU cpu = new CPU();
      private Memory memory = new Memory();
      private Disk disk = new Disk();

      void startComputer() {
         cpu.start();
         memory.load();
         disk.read();
         System.out.println("부팅 완료!");
      }
   }

   // 사용
   ComputerFacade computer = new ComputerFacade();
   computer.startComputer(); // 한 번의 호출로 복잡한 과정을 간단하게 실행
   ```

## 📅 2025/06/09

7. Spring에서 Bean의 기본 스코프가 싱글톤인 이유는 무엇인가요?

Singleton Pattern: 인스턴스를 불필요하게 생성하지 않고 오직 JVM 내에서 한 개의 인스턴스만 생성하여 재사용을 위해 사용되는 디자인 패턴

Bean의 기본 스코프가 싱글톤인 이유
| 이유 | 설명 |
| ---------------------- | -------------------------------------------------------- |
| **자원 절약** | 동일한 Bean을 여러 번 생성하는 대신 한 번만 생성하여 메모리 사용 최소화 |
| **공유 객체로 활용** | 설정이나 DAO, 서비스 클래스 등은 **상태가 없는(stateless)** 공유 객체로 쓰기에 적합 |
| **생성 비용 최소화** | Bean을 매번 생성하지 않아도 되어 **성능 최적화**에 도움 |
| **DI(의존성 주입)과 궁합이 좋음** | 대부분의 의존성 주입 대상은 한 번 생성되면 **변하지 않는 고정된 구조**로 쓰이기 때문 |

8. Repository 패턴의 목적과 장점을 설명하고, 프로젝트에서 JPA와 함께 어떻게 활용했는지 공유해주세요.

Repository Pattern: 도메인 객체와 데이터 접근 로직을 분리하여, 비즈니스 로직이 데이터 접근 방식에 의존하지 않도록 하는 구조적 패턴.

장점:

1. 데이터 로직과 비즈니스 로직을 분리할 수 있다.
2. 도메인에서는 일관된 인터페이스를 통해 데이터를 요청할 수 있다.
3. 데이터 저장소의 데이터를 캡슐화할 수 있다. 객체지향적인 프로그래밍에 더 적합하다.
4. 객체 간의 결합도가 감소한다.
5. 어플리케이션의 전체적인 디자인이 바뀌어도 적용할 수 있는 유연한 아키텍쳐이다.

JPA와 함께 활용하는 경우

- Spring Data JPA에서 JpaRepository를 상속하여 사용한다.
- 커스텀 쿼리 작성이 필요한 경우 @Query또는 QueryDSL을 사용한다.

```java
public interface UserRepository extends JpaRepository<User, Long> {
    Optional<User> findByEmail(String email);
}
```

9. 옵저버(Observer) 패턴을 언제 사용하는 것이 적절한지 설명하고, 실제 프로젝트에서 활용한 경험이 있다면 말씀해주세요.

Observer Pattern: 객체 간 1:N 관계를 정의하며, 어떤 객체의 상태가 변경되었을 때 그 객체에 의존하는 모든 객체에게 자동으로 알림을 보내는 디자인 패턴.
주체(Subject)와 관찰자(Observer)로 구성되며, 주체는 자신의 상태가 변경되면 등록된 모든 관찰자에게 알림을 보낸다. 관찰자는 주체에 등록되고 알림을 받으면 적절히 업데이트된다.

옵저버 패턴 사용 상황

1. 여러 객체가 한 객체에 의존할 때
   ex) 주식 가격 변동할 때 그것을 소유한 사용자가 알림을 받는 경우
2. 비즈니스 로직과 후속 처리 로직을 분리하고 싶을 때
   ex) 회원 가입 시 이메일 발송, 관리자 알림 등 부가 처리를 옵저버로 분리
