1. HTTP와 HTTPS의 차이점에 대해 설명해주세요.
   HTTP(HyperText Transfer Protocol)는 웹 상에서 클라이언트와 서버 간에 데이터를 주고받기 위한 프로토콜입니다. 하지만 HTTP는 데이터를 암호화하지 않고 평문으로 전송하기 때문에, 중간자 공격(MITM)이나 패킷 스니핑과 같은 보안 위협에 취약합니다.
   이러한 문제를 해결하기 위해 등장한 것이 HTTPS(HyperText Transfer Protocol Secure)입니다. HTTPS는 HTTP 위에 SSL/TLS 프로토콜을 결합한 형태로, 데이터를 암호화하여 안전하게 전송할 수 있도록 보장합니다. 사용자의 로그인 정보, 결제 정보 등 민감한 데이터를 다룰 때는 HTTPS가 필수입니다.
   두 프로토콜의 차이점은 주로 보안성에 있으며, HTTPS는 암호화, 무결성, 인증을 제공함으로써 통신의 신뢰성을 확보합니다. 또한 HTTPS를 사용하는 웹사이트는 SEO(검색 엔진 최적화) 측면에서도 우대받고, 브라우저에서는 자물쇠 아이콘으로 보안이 적용되었음을 표시해 사용자 신뢰도를 높일 수 있습니다.

2. HTTP/1.1과 HTTP/2의 차이점에 대해 설명해주세요.
   HTTP/1.1은 현재까지 가장 널리 사용되는 HTTP 프로토콜 버전이지만, 구조적으로 단일 요청-응답 방식을 기반으로 하기 때문에 성능에 한계가 있습니다. 하나의 TCP 연결에서 한 번에 하나의 요청만 처리할 수 있기 때문에, 리소스를 많이 요청하는 웹 페이지에서는 병목 현상과 지연이 발생할 수 있습니다. 이를 해결하기 위해 HTTP/2가 등장했습니다.
   HTTP/2는 기존의 HTTP와 호환되면서도 성능을 크게 개선한 프로토콜입니다. 가장 큰 특징은 **멀티플렉싱(Multiplexing)**을 지원한다는 점입니다. 이를 통해 하나의 TCP 연결에서 여러 개의 요청과 응답을 동시에 주고받을 수 있어 효율적입니다. 또한 헤더 압축(Header Compression), 서버 푸시(Server Push) 등의 기능을 통해 요청 크기를 줄이고, 클라이언트가 요청하지 않아도 서버가 예측하여 리소스를 미리 전송할 수 있도록 합니다.
   정리하면, HTTP/1.1은 직관적이지만 비효율적인 구조를 가지고 있고, HTTP/2는 이를 개선하여 속도와 네트워크 효율성을 향상시킨 프로토콜입니다.

3. REST API란 무엇이며, RESTful한 API를 설계하는 원칙에 대해 설명해주세요.
   REST(Representational State Transfer)는 자원을 이름으로 구분하고, 해당 자원에 대해 HTTP 기반의 표준적인 CRUD 방식으로 조작하는 설계 아키텍처입니다. REST API란 이러한 REST 원칙을 따르는 API로, 일반적으로 **HTTP 메서드(GET, POST, PUT, DELETE)**를 활용하여 자원에 대한 요청을 표현합니다.
   RESTful한 API를 설계하기 위한 핵심 원칙은 다음과 같습니다.
   첫째, 자원(Resource)은 URI로 표현되어야 하며, 동사는 사용하지 않고 명사형으로 작성합니다. 예를 들어 /users는 사용자 목록을, /users/1은 특정 사용자를 나타냅니다.
   둘째, HTTP 메서드의 의미를 명확히 사용해야 합니다. GET은 조회, POST는 생성, PUT은 수정, DELETE는 삭제를 의미합니다.
   셋째, **무상태성(Stateless)**을 유지해야 합니다. 즉, 서버는 요청 간의 상태 정보를 저장하지 않으며, 모든 요청은 독립적이어야 합니다.
   넷째, 응답에는 **표준적인 HTTP 상태 코드(200, 201, 400, 404, 500 등)**를 활용하여 요청 결과를 명확하게 전달해야 합니다.
   RESTful API는 단순하고 일관성 있는 구조로 인해 유지보수가 용이하고, 다양한 클라이언트와의 통신에 적합한 API 디자인 방식으로 널리 사용됩니다.

   # 📅 2025/05/27

4. HTTP 상태 코드에 대해 설명해주세요.
   HTTP 상태 코드는 클라이언트의 요청에 대해 서버가 어떤 응답을 했는지 숫자 형태로 알려주는 코드입니다.
   크게 다섯 가지 범위로 나눌 수 있습니다.

   - 1xx는 정보 응답
   - 2xx는 성공(예: 200 OK, 201 Created)
   - 3xx는 리다이렉트(예: 301 Moved Permanently, 302 Found)
   - 4xx는 클라이언트 오류(예: 400 Bad Request, 401 Unauthorized, 404 Not Found)
   - 5xx는 서버 오류(예: 500 Internal Server Error, 502 Bad Gateway)

   상태 코드를 통해 클라이언트와 서버가 서로 현재 상황을 정확히 파악할 수 있도록 도와줍니다.

5. TCP와 UDP의 차이점에 대해 설명해주세요.
   TCP와 UDP는 모두 전송 계층의 대표적인 프로토콜입니다.

   **TCP**는 연결 지향형 프로토콜로, 데이터가 순서대로 정확하게 전달되도록 보장합니다. 신뢰성이 필요한 서비스(예: 웹, 이메일 등)에 주로 사용됩니다. 다만, 이 과정에서 속도가 상대적으로 느릴 수 있습니다.

   **UDP**는 비연결형 프로토콜로, 데이터의 빠른 전송이 필요할 때 사용됩니다. 순서 보장이나 재전송 같은 신뢰성은 없지만, 오버헤드가 적어 실시간 스트리밍이나 게임 등 빠른 응답이 필요한 곳에 적합합니다.

   TCP는 신뢰성과 안정성이 중요할 때,
   UDP는 속도와 효율성이 중요할 때 주로 사용된다고 생각합니다.

6. 쿠키와 세션의 차이점에 대해 설명해주세요.
   쿠키와 세션은 모두 사용자 인증이나 상태 유지를 위해 사용되지만, 저장 위치와 관리 방식에 차이가 있습니다.

   **쿠키**는 클라이언트(브라우저)에 저장되며, 사용자의 컴퓨터에 데이터가 남아 있습니다. 만료 기간을 설정할 수 있고, 서버에 매 요청마다 함께 전송됩니다.

   **세션**은 서버에 저장되는 정보로, 주로 서버 메모리에 사용자 정보를 저장합니다. 클라이언트에는 세션 ID만 쿠키 형태로 전달되어 서버가 해당 사용자를 식별할 수 있습니다.
