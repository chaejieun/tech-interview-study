### 1. Singleton 패턴에 대해서 설명해주세요.
- 클래스의 인스턴스를 오직 하나만 생성하도록 보장하는 디자인 패턴
- 전역 상태를 관리하거나 리소스를 효율적으로 사용해야 할 때 유용
    - 설정 객체, 로깅, 캐시, DB 커넥션 풀 등 하나의 인스턴스로 공유하도록 하기 위해 사용
- 메모리 절약, 전역 접근 가능, 상태 일관성 유지
- 멀티스레드 환경에서 동기화 처리를 하지 않으면 인스턴스가 2개 이상 생성될 수 있어 double-checked locking, static block, enum 등을 통해 보완
- 구현 방법
    - 생성자를 private으로 선언하고, 정적 메서드를 통해 유일한 인스턴스에 접근

### 2. Bridge 패턴에 대해서 설명해주세요.
- 기능 계층(Abstraction) 과 구현 계층(Implementation) 을 분리하여 독립적으로 확장할 수 있도록 하는 구조 패턴 (인터페이스와 구현체 분리)
- 기능과 구현을 독립적으로 확장 가능, 코드 변경 시 영향 최소화
- 데이터베이스 연결 추상화, 다양한 메시지 송신 시스템 구현 시 사용
- 구현 방법
    1. 기능 계층(Abstraction) 정의:
        - 상위 수준의 기능을 정의하는 추상 클래스 또는 인터페이스를 생성
        - 구현 계층(Implementor)에 대한 참조를 가짐
    2. 구현 계층(Implementor) 인터페이스 정의:
        - 추상화에서 사용할 기본 연산들을 선언 해 구현 클래스들이 따라야 할 인터페이스를 정의
    3. 구체 구현(Concrete Implementor) 클래스 생성:
        - 구현 인터페이스를 실제로 구현하는 클래스들 구성
    4. 구체 기능(Refined Abstraction) 클래스 생성:
        - 기능 계층를 확장하여 실제 사용되는 기능 클래스 생성 
        - 구현 계층 인터페이스를 통해 실제 구현 위임

```
// 구현 계층: 채널 (Implementor)
interface MessageSender {
    void send(String content);
}

class SmsSender implements MessageSender {
    public void send(String content) {
        System.out.println("[SMS] " + content);
    }
}

class EmailSender implements MessageSender {
    public void send(String content) {
        System.out.println("[Email] " + content);
    }
}

// 기능 계층: 메시지 타입 (Abstraction)
abstract class Message {
    protected MessageSender sender;
    public Message(MessageSender sender) {
        this.sender = sender;
    }
    public abstract void sendMessage(String content);
}

// 확장 기능: 인증 메시지, 광고 메시지 등
class AuthMessage extends Message {
    public AuthMessage(MessageSender sender) {
        super(sender);
    }
    public void sendMessage(String content) {
        sender.send("[Auth] " + content);
    }
}

class PromoMessage extends Message {
    public PromoMessage(MessageSender sender) {
        super(sender);
    }
    public void sendMessage(String content) {
        sender.send("[Promo] " + content);
    }
}
```

### 3. Strategy 패턴에 대해서 설명해주세요.
- 행동(로직)을 객체로 캡슐화하고, 동적으로 교체할 수 있도록 하는 행동 패턴
- 조건문(if-else)의 복잡한 분기를 전략 객체로 분리하여 유연하고 테스트 가능
- 구현 방법 (결제 예시)
    - 전략 인터페이스(PaymentStrategy): 모든 결제 전략에 공통된 인터페이스를 정의
    - 구체적인 전략 클래스들:
        - CreditCardPayment: 신용카드 결제 전략
        - NaverPayPayment: 네이버페이 결제 전략
        - BankTransferPayment: 계좌이체 결제 전략
    - 컨텍스트(PaymentProcessor): 전략 객체를 참조하고 필요에 따라 전략을 교체

```
// 전략 인터페이스
interface PaymentStrategy {
    void pay(PaymentRequest request);
}

// 전략 구현체들
class KakaoPayStrategy implements PaymentStrategy {
    public void pay(PaymentRequest request) {
        System.out.println("카카오페이로 결제 요청");
    }
}

class NaverPayStrategy implements PaymentStrategy {
    public void pay(PaymentRequest request) {
        System.out.println("네이버페이로 결제 요청");
    }
}

class VirtualAccountStrategy implements PaymentStrategy {
    public void pay(PaymentRequest request) {
        System.out.println("가상계좌 생성 및 결제 요청");
    }
}

// Context
class PaymentProcessor {
    private PaymentStrategy strategy;
    public void setStrategy(PaymentStrategy strategy) {
        this.strategy = strategy;
    }
    public void process(PaymentRequest request) {
        strategy.pay(request);
    }
}
```

4. Builder 패턴에 대해서 설명해주세요.
- 복잡한 객체의 생성 과정을 단계별로 나누어, 동일한 생성 절차에서 서로 다른 표현을 만들 수 있게 하는 생성 패턴
- 특히 생성자에 많은 파라미터가 있을 때, 가독성과 유지보수성 향상
- 특징 
    - 필수값과 선택값을 구분해서 객체를 생성할 수 있음
    - 메서드 체이닝 방식으로 객체 생성 가능
    - new 키워드 대신 Builder를 통해 유연하게 생성

5. Factory Method 패턴에 대해서 설명해주세요.
- 객체 생성 코드를 하위 클래스에 위임함으로써 객체 생성을 캡슐화하는 패턴
- 상위 클래스는 객체 생성 방법만 정의, 실제 인스턴스 생성은 하위 클래스에서 결정
- 구조
    - Product: 생성될 객체의 인터페이스
    - ConcreteProduct: 실제 생성되는 클래스
    - Creator: 팩토리 메서드를 선언
    - ConcreteCreator: 팩토리 메서드를 구현하여 객체 생성
    ```
        // Product
        interface Notification {
            void send();
        }

        // Concrete Products
        class EmailNotification implements Notification {
            public void send() {
                System.out.println("Sending Email...");
            }
        }

        class SmsNotification implements Notification {
            public void send() {
                System.out.println("Sending SMS...");
            }
        }

        // Creator
        abstract class NotificationFactory {
            public abstract Notification createNotification();
        }

        // Concrete Creator
        class EmailNotificationFactory extends NotificationFactory {
            public Notification createNotification() {
                return new EmailNotification();
            }
        }

        // 사용
        NotificationFactory factory = new EmailNotificationFactory();
        Notification notification = factory.createNotification();
        notification.send();  // "Sending Email..."
    ```
6. 퍼사드 패턴에 대한 예를 들어주세요.
- 복잡한 서브시스템을 간단한 인터페이스 하나로 감싸, 사용자가 쉽게 접근할 수 있도록 하는 구조 패턴
- 서브시스템의 내부 복잡성을 숨기고, 클라이언트는 간단한 API만 사용
```
// 복잡한 서브시스템
class FileReader {
    void readFile(String filePath) {
        System.out.println("Reading file: " + filePath);
    }
}

class Compressor {
    void compress(String fileData) {
        System.out.println("Compressing file data...");
    }
}

class Encryptor {
    void encrypt(String compressedData) {
        System.out.println("Encrypting compressed data...");
    }
}

// 퍼사드 클래스
class CompressionFacade {
    private FileReader reader = new FileReader();
    private Compressor compressor = new Compressor();
    private Encryptor encryptor = new Encryptor();

    public void compressAndEncrypt(String filePath) {
        reader.readFile(filePath);
        compressor.compress("file data");
        encryptor.encrypt("compressed data");
    }
}

// 사용
CompressionFacade facade = new CompressionFacade();
facade.compressAndEncrypt("document.txt");
```
