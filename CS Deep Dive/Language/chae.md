# 📅 2025/05/08
# JVM의 구조와 Java의 실행방식을 설명해주세요.

<br>
![alt text](image.png)

## JVM이란?
- Java 가상머신으로 **Java 바이트 코드**를 실행할 수 있는 주체 

<br>

## JVM의 구조
- Class Loader
- Execution Engine
- Garbage Collector
- Runtime Data Area

<br>

## Java의 실행방식
1. 자바 애플리케이션의 실행에서 **Java 컴파일러**가 먼저 동작을 수행한다
2. Java 컴파일러는 .java 파일을 모두 JVM이 사용할 수 있는 **.class 파일로 컴파일** 한다. 이 시점이 **컴파일 타임**이다.
3. 이후 JVM을 실행하면서 **런타임 시점**이 시작된다.
4. JVM 내부에서는 애플리케이션을 실행하기 위해 Execution Engine이 필요한 클래스들을 Class Loader에 요청하고 Class Loader가 바이트코드의 .class에서 가져와 메모리에 올린다. 
5. 가져오는 클래스들의 바이트 코드들이 이상이 없는 지, 자바의 보안 규칙을 위배하지 않는 지 검사
6. 그 다음으로 Execution Engine이 메모리에 올라온 바이트코드를 실행하면서 애플리케이션이 실행된다. 계속 이러한 동작을 하면서 애플리케이션이 동작한다.

<br>

### ✨ 정리 포인트
- JVM은 Java 바이트코드를 실행하는 가상 머신이며, 주요 구성은 Class Loader, Runtime Data Area, Execution Engine, Garbage Collector입니다. Java의 실행 흐름은 .java 소스를 컴파일러가 .class로 변환하고, 이후 JVM이 클래스를 로드하여 메모리에 올린 뒤 Execution Engine이 이를 실행. JVM의 구조 덕분에 Java는 플랫폼 독립적인 언어가 된다.

--- 
# GC(Garbage Collection)가 무엇인지, 필요한 이유는 무엇인지, 동작방식에 대해 설명해주세요.

## GC(Garbage Collection)란
- 자바 가상 머신(JVM) 내에서 사용되는 메모리 관리 기술 중 하나. 이는 프로그램이 동적으로 할당한 메모리 중에서 **더 이상 사용되지 않는 객체들을 찾아 해제하여 메모리 누수를 방지**하고 프로그램의 성능을 최적화 한다.

<br>

## GC(Garbage Collection)의 필요성
- 메모리 누수 방지 : 프로그램에서 더 이상 필요하지 않은 객체들이 메모리에 계속 쌓이면, 시스템의 메모리가 부족해지고 성능이 저하될 수 있다 
- 편의성 : 개발자가 메모리 할당 및 해제에 대한 번거로움을 줄여준다. 명시적인 메모리 관리가 필요하지 않으므로 코드 작성이 간편해진다
- 안정성 : GC는 메모리 관리를 자동화하여 메모리 오류로부터 프로그램을 보호
- 객체 추적 : GC는 사용 중인 객체와 사용되지 않는 객체를 구별하기 위해 객체를 추적한다. 이를 위해 root 객체부터 시작하여 참조 체인을 따라가며 도달 가능한 객체를 식별한다
- 메모리 해제 : 가비지 식별이 완료되면 GC는 해당 객체들의 메모리르 해제하여 재사용 할 수 있도록 한다. 이 과정은 자원을 회수하여 다른 용도로 재사용할 수 있도록 한다

<br>

## GC(Garbage Collection)의 동작방식
1. Stop The World : JVM이 GC를 실행하기 위해 애플리케이션의 실행을 멈추는 작업. GC를 실행하는 쓰레드 외 다른 모든 쓰레드는 작업이 중단
2. Mark And Sweep : Stop The World 이후, GC가 사용되지 않는 메모리를 식별하는 과정을 Mark, 이 메모리를 제거하는 과정을 Sweep이라 한다

<br>

--- 

# 객체지향에 대해서 설명해주세요.

## 객체지향 (Object-Oriented Programming, OOP)이란
- **사물(객체)를 소프트웨어로 모델링하여 프로그래밍 하는 방식** 데이터(속성)와 기능(행위)을 하나의 단위(클래스, 객체)로 묶어서 설계하고 개발

<br>

## 객체지향의 장단점
1. 장점 
- 코드 재사용 용이
- 유지보수 용이
- 확장성 용이
- 가독성 용이

<br>

2. 단점
- 초기 설계가 복잡
- 프로그래밍 난이도 상승
- 속도 측면에서는 절차지향보다 느릴 수 있음 (상대적으로)


<br>

## 객체지향 5대 원칙
1. SRP(Single Responsibility Principle, 단일 책임 원칙) : 객체는 오직 하나의 책임을 가져야 한다
2. OCP(Open-Closed Principle, 계방-폐쇠 원칙) : 객체는 확장에 대해서는 개방적이고 수정에 대해서는 폐쇄적이어야 한다
3. LSP(Liskov Substitution Principle, 리스코프 치환 원칙) : 자식 클래스는 언제나 자신의 부모 클래스를 대체할 수 있습니다. 즉, 부모 클래스가 들어갈 자리에 자식 클래스를 넣어도 계획대로 잘 작동해야 한다.
4. ISP(Interface Segregation Principle, 인터페이스 분리 원칙) : 클라이언트에서 사용하지 않는 메서드는 사용해선 안된다는(의존 관계를 맺어서는 안된다) 원칙입니다. (인터페이스의 SRP)
5. DIP(Dependency Inversion Principle, 의존성 역전 원칙) : 추상적인 것은 자신보다 구체적인 것에 의존하지 않고, 변화하기 쉬운 것에 의존해서는 안된다. 즉, 자신이 변하기 쉬운 것에 의존하지 말라는 것.

--- 
# # 📅 2025/05/26
# SOLID(객체지향 5대원칙)에 대해서 설명해주세요.

## 1. SRP (Single Responsibility Principle) 단일 책임 원칙
- 하나의 클래스는 하나의 책임만 가져야 한다.
- **클래스를 변경하지 않는 이유는 단 하나여야 한다.** 변경이 있을 때 파급 효과가 적어야 한다. 
-   이를 지키지 않으면, 한 책임의 변경에 의해 다른 책임과 관련된 코드에 영향을 미칠 수 있다. 결국, 유지보수가 매우 비효율적이다.

## 2. OCP (Open-Closed Principle) 개방-폐쇄 원칙
- **소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.**
    - 즉, 기존의 코드를 변경하지 않고 기능을 수정, 추가할 수 있도록 설계해야 한다.
- 인터페이스를 구현한 새로운 클래스를 하나 만들어서 새로운 기능을 구현 


### 예제
```java
class Rectangle {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    public double getWidth() {
        return width;
    }

    public double getHeight() {
        return height;
    }
}

class Circle {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public double getRadius() {
        return radius;
    }
}

class AreaCalculator {
    public double calculateRectangleArea(Rectangle rectangle) {
        return rectangle.getWidth() * rectangle.getHeight();
    }

    public double calculateCircleArea(Circle circle) {
        return Math.PI * circle.getRadius() * circle.getRadius();
    }
}

public class Main {
    public static void main(String[] args) {
        Rectangle rectangle = new Rectangle(5, 10);
        Circle circle = new Circle(3);
        AreaCalculator calculator = new AreaCalculator();

        System.out.println("사각형 넓이: " + calculator.calculateRectangleArea(rectangle));
        System.out.println("원 넓이: " + calculator.calculateCircleArea(circle));

        // 새로운 도형 (삼각형) 추가 시 AreaCalculator 수정 필요
    }
}


// 리팩토링 후
interface Shape {
    double area();
}

class Rectangle implements Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height;
    }
}

class Circle implements Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}

class Triangle implements Shape {
    private double base;
    private double height;

    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }

    @Override
    public double area() {
        return 0.5 * base * height;
    }
}

class AreaCalculator {
    public double calculateArea(Shape shape) {
        return shape.area();
    }
}

public class Main {
    public static void main(String[] args) {
        Rectangle rectangle = new Rectangle(5, 10);
        Circle circle = new Circle(3);
        Triangle triangle = new Triangle(4, 6);
        AreaCalculator calculator = new AreaCalculator();

        System.out.println("사각형 넓이: " + calculator.calculateArea(rectangle));
        System.out.println("원 넓이: " + calculator.calculateArea(circle));
        System.out.println("삼각형 넓이: " + calculator.calculateArea(triangle));
    }
}
```

###  => ✨ 기존의 코드를 변경하지 않고 어떻게 기능을 수정, 추가할 수 있을까?
상속(다형성), 추상화(인터페이스)를 활용하면 된다. 자주 변경하는 부분을 추상화해서 기존 코드를 수정하지 않고 기능을 확장할 수 있도록 해서 유연성을 살릴 수 있다.

## 3. LSP (Liskov Substitution Principle) 리스코프 치환 원칙
- 하위 타입 객체는 상위 타입 객체에서 가능한 행위를 수행할 수 있어야 한다.
    - **즉, 상위 타입 객체를 하위 타입 객체로 대체하여도 정상적으로 동작해야 한다.**
- 다형성에서 하위 클래스는 인터페이스가 규약을 다 지켜야 한다.
- 상속 관계에서는 꼭 일반화 관계(IS-A)가 성립해야 한다.
- 상속 관계가 아닌 클래스들을 상속관계로 설정하면 LSP 위반.


### 예제
```java
class Bird {
    public void fly() {
        System.out.println("새가 날아갑니다.");
    }
}

class Penguin extends Bird {
    @Override
    public void fly() {
        // 펭귄은 날 수 없으므로 이 메서드는 적절하지 않습니다.
        throw new UnsupportedOperationException("펭귄은 날 수 없습니다.");
    }
}

public class Main {
    public static void main(String[] args) {
        Bird bird1 = new Bird();
        bird1.fly(); // 정상 동작

        Bird bird2 = new Penguin();
        bird2.fly(); // 예외 발생! LSP 위반
    }
}
```
- ex) 예를 들어서, 자동차 인터페이스가 있다고 하자. 자동차 인터페이스의 엑셀 기능은 자동차가 앞으로 가는 기능을 한다. 그런데 엑셀 기능을 실행했는데 자동차가 뒤로 간다고 생각해보자. 참으로 끔찍한 일이다. 이는 LSP를 위반하는 것이다.
설령 기능이 느리더라도 엑셀 기능을 실행했을 때 자동차는 앞으로 가야한다.

## 4. ISP (Interface Segregation Principle) 인터페이스 분리 원칙
- 클라이언트는 자신이 사용하는 메소드에만 의존해야 한다.
- **특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 한 개보다 낫다**
- 인터페이스는 해당 인터페이스를 사용하는 클라이언트를 기준으로 잘게 분리되어야 한다.


- ex) 예를 들어서, '자동차'라는 하나의 범용 인터페이스 보다는 운전, 정비, 타이어 등의 세부적인 인터페이스로 나누는 것이 더 낫다는 것이다. 이렇게 된다면, 타이어를 교체할 때는 타이어 인터페이스만 확인하고 변경하면 된다.
이렇게 세부적인 인터페이스로 나눈다면 인터페이스가 명확해지고, 대체 가능성이 높아진다.

## 5. DIP (Dependency Inversion Principle) 의존 역전 원칙
- 의존 관계를 맺을 때, 변하기 쉬운 구체적인 것 보다는 변하기 어려운 추상적인 것에 의존해야 한다는 것이다.
    - 즉, 구현 클래스에 의존하지 말고, 인터페이스에 의존하라는 뜻이다.
- 클라이언트가 인터페이스에 의존해야 유연하게 구현체를 변경할 수 있다. 구현체에 의존한다면 변경에 어려움이 생긴다.
- 고수준 모듈은 저수준 모듈의 구현에 의존해서는 안된다.
    -  저수준 모듈이 변경되어도 고수준 모듈은 변경이 필요없는 형태가 이상적이다.

<br>

# 인터페이스와 추상클래스의 차이점에 대해 설명해주세요.
| 특징             | 인터페이스(Interface)                                  | 추상 클래스(Abstract Class)                                     |
| ---------------- | ------------------------------------------------------- | --------------------------------------------------------------- |
| **목적** | 규약(Contract) 정의, 역할 명시, 다중 상속 지원              | 클래스 계층 구조 형성, 일부 구현 제공, 공통 기능 정의                 |
| **추상 메서드** | 모든 메서드는 기본적으로 추상 메서드 (`abstract` 키워드 생략 가능) | 추상 메서드 (`abstract` 키워드 필요)를 포함할 수 있고, 구체적인 메서드도 가질 수 있음 |
| **구현된 메서드** | 가질 수 없음 (Java 8부터 `default` 메서드 추가)            | 구체적인 구현을 가진 메서드를 가질 수 있음                           |
| **필드 (변수)** | 상수( `static final`)만 가질 수 있음                        | 인스턴스 변수, 상수 등을 가질 수 있음                               |
| **생성자** | 가질 수 없음                                            | 가질 수 있음 (하위 클래스 생성 시 호출됨)                           |
| **다중 상속** | 다중 인터페이스 구현 (implements) 가능                      | 단일 상속만 가능 (extends)                                       |
| **`extends` vs `implements`** | 인터페이스는 클래스에 `implements` 키워드로 구현됨              | 클래스는 추상 클래스를 `extends` 키워드로 상속받음                 |


<br>

# 언제 사용 사례와 장점
**인터페이스**
- 클래스가 제공해야 하는 기능을 명시하고 싶을 때 (규약 정의)
- 클래스가 여러 가지 역할을 수행할 수 있도록 하고 싶을 때 (다중 구현)
- 전혀 코드를 공유하지 않고 순수하게 명세만 정의하고 싶을 때

**추상 클래스**
- 클래스 간에 **공통되는 코드를 제공**하고 하위 클래스에서 특정 부분을 구현하도록 강제하고 싶을 때(코드의 재사용을 높임)
- 클래스 계층 구조를 명확하게 표현하고 싶을 때 ("IS-A" 관계)
- 인스턴스 변수를 포함하고 싶을 때
- 추상 클래스는 템플릿 메서드 패턴(Template Method Pattern)와 같은 디자인 패턴에서 주로 사용

<br>

# 컬렉션 프레임워크에 대해서 설명해주세요.
- 컬렉션 프레임워크(Collection Framework)는 자바에서 데이터를 저장, 관리 및 처리하기 위한 인터페이스와 클래스들의 집합입니다. 
- 이 프레임워크는 데이터를 효율적으로 구조화하고 조작할 수 있는 다양한 자료구조를 제공합니다. 


## 컬렉션 핵심 인터페이스
- `Collection`: 컬렉션의 최상위 인터페이스입니다. 요소들의 그룹을 나타내며, 기본적인 공통 기능을 정의합니다. (`add()`, `remove()`, `contains()`, `size()`, `iterator()` 등)

- `List`: 순서가 있는 컬렉션으로, 요소의 중복을 허용합니다. 인덱스를 통해 요소에 접근할 수 있습니다. (ArrayList, LinkedList, Vector)
- `Set`: 순서가 없고, 요소의 중복을 허용하지 않는 컬렉션입니다. (HashSet, TreeSet, LinkedHashSet)
- `Queue`: 특정 순서로 요소를 처리하는 컬렉션입니다. 주로 FIFO (First-In, First-Out) 방식을 따릅니다. (LinkedList, PriorityQueue, ArrayDeque)
- `Map`: 키(Key)와 값(Value)의 쌍으로 이루어진 데이터를 저장하는 컬렉션입니다. 키는 중복될 수 없지만, 값은 중복될 수 있습니다. (HashMap, TreeMap, LinkedHashMap, Hashtable)

## 컬렉션 프레임워크의 장점
- 코드 재사용성 향상: 이미 구현된 효율적인 자료구조를 활용하여 개발 시간을 단축하고 코드의 품질을 높인다
- 성능 향상 : 각 자료구조의 특징에 맞춰 최적화된 구현을 제공하여 효율적인 데이터 처리 가능
- API 통일성: 일관된 인터페이스와 클래스 구조를 제공하여 사용하기 편리

--- 
# 📅 2025/06/10
# 오버라이딩과 오버로딩이 무엇이며 어떤 차이가 있을까요?

## 오버로딩(Overloading)
- 오버로딩은 **하나의 클래스 내에서** 같은 이름의 메서드를 여러 개 정의를 하는 것. 이때, 각 메서드는 **매개변수의 개수나 타입, 또는 순서가 달라야 한다**

## 오버라이딩(Overriding)
- 오버라이딩은 **부모 클래스(상위 클래스)로부터 상속받은 메서드**를 자식 클래스(하위 클래스)에서 **내용을 변경하여 다시 정의**하는 것을 의미. 부모 클래스의 메서드와 동일한 시그니처(이름, 매개변수 목록, 반환타입)을 가져야 한다.
- **상속관계에서 부모 클래스의 기능을 자식 클래스의 특성에 맞게 재정의** => **다형성**을 가능하게 함


# 동일성(identity)와 동등성(equality)에 대해 설명해주세요. (equals(), ==)

## 동일성(Identity)
- 동일성은 두 객체가 **정확히 같은 메모리 주소**를 가리키는 지, 즉 **메모리 상에서 동일한 인스턴스**인지를 비교하는 개념. 이는 객체의 '아이덴티티'를 의미.
- 주로 `==` 연산자를 사용하여 비교
- 원시 타입(primitive types)(int,boolean, char 등) 등에서는 값 자체를 비교
- 참조 타입(reference types)(객체,배열 등)에서는 객체가 저장된 **메모리 주소값**을 비교


# String, StringBuilder, StringBuffer 각각의 차이에 대해 설명해주세요.

## String
문자열의 내용이 자주 변경되지 않거나, 불변성이 중요한 경우(예: Map의 키)에 적합

- 불변성(immutable) : String 객체는 한 번 생성되면 절대 그 내용을 변경할 수 없습니다. 
- 스레드 안정성 (Thread-Safe): 불변하기 때문에 여러 스레드가 동시에 String 객체에 접근해도 데이터의 일관성이 깨질 염려가 없습니다. 따라서 스레드-세이프합니다.
- 성능: 문자열 연결(+)이나 수정 작업이 빈번하게 발생할 경우, 새로운 String 객체가 계속 생성되므로 성능 저하 및 메모리 낭비가 발생할 수 있습니다. 

## StringBuilder
단일 스레드 환경에서 문자열을 동적으로 조작하거나 많은 문자열 연결 작업이 필요한 경우에 적합

- 가변성 (Mutable): StringBuilder 객체는 내용을 변경할 수 있습니다. 즉, 문자열을 추가하거나 수정하는 연산을 수행하면 기존 객체 내부의 문자열 버퍼를 직접 조작합니다. 새로운 객체를 생성하는 오버헤드가 없습니다.
- 스레드 안정성 (Not Thread-Safe): StringBuilder는 동기화(Synchronization)를 지원하지 않습니다. 따라서 여러 스레드가 동시에 하나의 StringBuilder 객체에 접근하여 내용을 변경하려고 하면, 예상치 못한 결과(데이터 손상)가 발생할 수 있습니다. 즉, 스레드-세이프하지 않습니다.
- 성능: 문자열의 추가, 삭제, 수정 등 변경 작업이 빈번하게 발생할 경우 String보다 훨씬 빠르고 효율적입니다. 새로운 객체 생성 비용이 없기 때문입니다.


## StringBuffer
멀티스레드 환경에서 안전하게 문자열을 동적으로 조작하거나 많은 문자열 연결 작업이 필요한 경우에 적합

- 가변성 (Mutable): StringBuilder와 마찬가지로 내용을 변경할 수 있습니다. 기존 객체 내부의 문자열 버퍼를 직접 조작합니다.
- 스레드 안정성 (Thread-Safe): StringBuffer의 모든 메서드는 synchronized 키워드로 동기화되어 있습니다. 이는 한 번에 하나의 스레드만 해당 메서드를 실행할 수 있도록 보장하여 스레드-세이프합니다.
- 성능: 동기화 오버헤드 때문에 StringBuilder보다 성능이 약간 떨어집니다. 하지만 String보다는 훨씬 효율적입니다.
