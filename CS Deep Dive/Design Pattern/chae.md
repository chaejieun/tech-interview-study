# 📅 2025/05/07
# Singleton 패턴에 대해서 설명해주세요
- 싱글톤 패턴은 객체 지향 프로그래밍에서 특정 클래스가 단 하나만의 인스턴스를 생성하여 사용하기 위한 패턴. 
- 생성자를 여러 번 호출하더라도 '인스턴스'가 **하나만** 존재하도록 보장하여 애플리케이션에서 동일한 객체 인스턴스에 접근할 수 있도록 하는 것.

<br>

## 싱글톤(Singleton) 패턴을 사용하는 이유
1. 메모리 측면 이점 
- 한 개의 인스턴스만을 고정 메모리 영역에 생성하고 추후 해당 객체를 접근할 때 메모리 낭비 방지 가능 
2. 속도 측면 이점
- 생성된 인스턴스를 사용할 때는 이미 생성된 인스턴스를 활용하여 속도 측면에 이점
3. 데이터 공유 쉬움
- 전역으로 사용하는 인스턴스이기 때문에 다른 클래스에서 데이터를 공유하며 사용할 수 있음.
- but, 동시성 문제 발생 가능하기 때문에 유의하여 설계해야 한다

<br>

## 싱글톤(Singleton) 패턴 구현 방법
- private 선언 (new 키워드 사용 불가능)
- getInstance() 메서드가 처음 실행 될 떄만 하나의 instance 생성되고 그 후에는 instance를 return
- 단 하나의 객체만을 생성, 사용

<br>

## 🔍 예제
### Java에서의 싱글톤 패턴 구현
```java
public class Singleton {
    // 단 1개만 존재해야 하는 객체의 인스턴스로 static 으로 선언
    private static Singleton instance;

    // private 생성자로 외부에서 객체 생성을 막아야 한다.
    private Singleton() {
    }

    // 외부에서는 getInstance() 로 instance 를 반환
    public static Singleton getInstance() {
        // instance 가 null 일 때만 생성
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```
=> 싱글톤 객체를 getInstance()를 통해 여러 변수에서 호출하더라도 같은 인스턴스를 참조

<br>

## 싱글톤(Singleton) 패턴 문제점
1. Multi-thread 환경에서 instance가 없을 때 동시에 getInstance() 서드를 실행하는 경우 각각 새로운 instance를 생성할 수 있음
- => 해결법 : sychronized 키워드 사용, double-checked locking 동기화 처리
2. 싱글톤은 전역 인스턴스를 사용하기 때문에 단위 테스트 시 상태 공유로 인해 테스트 간 간섭 발생
- => 해결법 : 테스트 시, mock이나 리플렉션으로 인스턴스 초기화하거나 싱글톤 사용 최소화

<br>


## ✨ 정리 포인트
싱글톤 패턴은 클래스의 인스턴스를 오직 하나만 생성하고, 어디서든 해당 인스턴스를 공유할 수 있도록 하는 디자인 패턴입니다. 주로 설정 클래스, 로깅, DB 커넥션 풀처럼 **하나만** 있어야 하는 자원에 사용됩니다.  
Java에서는 생성자를 **private**으로 선언하고, 정적 메서드인 **getInstance()**를 통해 인스턴스를 반환합니다.  
다만 멀티스레드 환경에서는 동시 접근 시 문제가 발생할 수 있어서, synchronized 키워드를 사용하거나 Double-Checked Locking 패턴으로 해결합니다.

---
# Bridge 패턴에 대해서 설명해주세요
- 객체의 구현부(implementation)와 추상층(abstraction)을 분리하여 각각 독립적으로 변형할 수 있게 하는 구조적인 디자인 패턴
- 서로 독립된 두 개의 계층이 서로 연결되어 동작하게 하는 것을 중점으로 한다

<br>

## 브릿지(Bridge) 패턴의 구조
![alt text](image.png)

- Abstraction: 기능의 추상적 정의, 구현체를 참조함
- RefinedAbstraction: Abstraction을 확장한 구체 클래스
- Implementor: 구현부의 인터페이스 정의
- ConcreteImplementor: 실제 구현 클래스

<br>

## 브릿지(Bridge) 패턴 장점
1. 추상화와 구현 간의 결합도를 줄인다
- 추상화와 구현이 분리되어 있어 둘 사이 의존성 감소, 그 결과 두 요소를 독립적으로 확장하거나 변경이 가능
2. 단일 책임 원칙 준수
- 추상화와 구현이 각각 다른 일을 처리하도록 분리함으로써, 각 클래스는 자신의 책임 영역에만 집중
3. 시스템 구조 개선
-  고수준의 추상화 코드와 저수준의 구현 코드를 분리함으로써, 깔끔하고 이해하기 쉬운 시스템 구조 가능 

<br>

## 브릿지(Bridge) 패턴 단점
1. 복잡성 증가
2. 추상화와 구현 간의 연결하는 코드를 작성해줘야 한다

<br>

## 🔍 예제
### Java에서의 브릿지 패턴 구현
```java
// Implementor
interface DrawAPI {
    void drawCircle(int radius, int x, int y);
}

// ConcreteImplementor
class RedCircle implements DrawAPI {
    public void drawCircle(int radius, int x, int y) {
        System.out.println("Red Circle at (" + x + "," + y + ") radius: " + radius);
    }
}

class GreenCircle implements DrawAPI {
    public void drawCircle(int radius, int x, int y) {
        System.out.println("Green Circle at (" + x + "," + y + ") radius: " + radius);
    }
}

// Abstraction
abstract class Shape {
    protected DrawAPI drawAPI;
    
    protected Shape(DrawAPI drawAPI){
        this.drawAPI = drawAPI;
    }
    public abstract void draw();
}

// RefinedAbstraction
class Circle extends Shape {
    private int x, y, radius;

    public Circle(int x, int y, int radius, DrawAPI drawAPI) {
        super(drawAPI);
        this.x = x;
        this.y = y;
        this.radius = radius;
    }

    public void draw() {
        drawAPI.drawCircle(radius, x, y);
    }
}

// 사용 예시
public class BridgePatternDemo {
    public static void main(String[] args) {
        Shape redCircle = new Circle(100,100, 10, new RedCircle());
        Shape greenCircle = new Circle(100,100, 10, new GreenCircle());

        redCircle.draw();
        greenCircle.draw();
    }
}
```
--- 

# Strategy 패턴에 대해서 설명해주세요
- 전략(Strategy) 패턴은 실행(런타임) 중에 알고리즘 전략을 선택하여 객체 동작을 실시간으로 바뀌도록 할 수 있게 하는 행위 디자인 패턴
- '전략'이란 알고리즘이 될 수도 있으며, 기능이나 동작이 될 수도 있는 특정한 목표를 수행하기 위한 행동 계획
- 객체의 행위를 변경하고 싶은 경우 **직접 수정하지 않고** 전략이라 불리는 **캡슐화한 알고리즘 객체**를 변경해줌으로써 유연하게 확장하는 방법

<br>

## 구성 요소
- Strategy (전략 인터페이스) : 공통된 알고리즘의 인터페이스 정의
- ConcreteStrategy (구체 전략) : 실제 알고리즘 또는 동작을 구현하는 클래스
- Context (문맥) : Strategy 객체를 사용하는 클래스. 실행 시 전략을 주입받음

<br>

## 장점
- 알고리즘을 정의하고 캡슐화하여 런타임 시에 알고리즘을 선택하는 데 사용됨
- 알고리즘을 쉽게 변경 및 대체할 수 있으므로 **유연함**
- 알고리즘 추가 및 수정을 할 때 코드 수정이 최소화되므로 **확장성**이 높아짐
- 알고리즘을 캡슐화했기에 코드 **재사용성**이 좋음
- 각각 알고리즘을 독립적으로 테스트할 수 있으므로 **용이**함

<br>

## 단점 
- 추가적인 클래스 및 인터페이스가 필요하기에 코드 복잡성이 증가될 수 있음
- 런타임 시에 알고리즘을 선택하는 데 추가적인 오버헤드 발생 가능
- 전략패턴을 구현하는 것이 어려울 수 있으므로, 적절한 분석과 설계가 필요함

<br>

## 🔍 예제
### Java에서의 전략 패턴 구현
```java
// 전략 인터페이스
public interface PaymentStrategy {
    void pay(int amount);
}

// 구체 전략 클래스들
public class CreditCardPayment implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println(amount + "원을 신용카드로 결제합니다.");
    }
}

public class KakaoPayPayment implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println(amount + "원을 카카오페이로 결제합니다.");
    }
}

// Context 클래스
public class PaymentService {
    private PaymentStrategy strategy;

    public PaymentService(PaymentStrategy strategy) {
        this.strategy = strategy;
    }

    public void processPayment(int amount) {
        strategy.pay(amount);
    }
}
```