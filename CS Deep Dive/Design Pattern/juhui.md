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
