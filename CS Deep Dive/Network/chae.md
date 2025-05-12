# 📅 2025/05/12
# HTTP와 HTTPS의 차이점에 대해 설명해주세요

## HTTP란
- HTTP(Hyper Text Transfer Protocol)란 **서버/클라이언트 모델을 따라 데이터를 주고 받기 위한 프로토콜**이다.
즉, HTTP는 인터넷에서 하이퍼텍스트를 교환하기 위한 통신 규약으로, 80번 포트를 사용하고 있다. 따라서 HTTP 서버가 80번 포트에서 요청을 기다리고 있으며, 클라이언트는 80번 포트로 요청을 보내게 된다.

<br>

## HTTP의 구조
![alt text](image.png)
- HTTP는 애플리케이션 레벨의 프로토콜로 TCP/IP 위에서 작동한다. HTTP는 상태를 가지고 있지 않는 Statless 프로토콜이며, Method, Path, Version, Headers, Body등으로 구성된다.
- ex) 상태 유지가 필요한 경우 쿠키, 세션, 토큰 활용

<br>

## HTTPS란
- HTTPS(Hyper Text Transfer Protocol Secure)는 **HTTP에 데이터 암호화가 추가된 프로토콜**이다. HTTPS는 HTTP와 다르게 443번 포트를 사용하며, 네트워크 상에서 중간에 제3자가 정보를 볼 수 없도록 암호화를 지원한다.
- HTTPS는 대칭키 암호화 방식과 비대칭키 암호화 방식을 모두 사용한다

<br>

### ✨ 정리 포인트
- HTTP는 클라이언트와 서버가 데이터를 주고받기 위한 **비연결성(stateless)**의 애플리케이션 계층 프로토콜입니다.
주로 웹에서 HTML, JSON 같은 데이터를 주고받으며, 80번 포트를 사용합니다. 상태를 저장하지 않기 때문에, 인증이 필요한 경우에는 쿠키, 세션, 토큰 등을 별도로 사용
- HTTPS는 HTTP에 보안이 추가된 프로토콜로, SSL/TLS를 통해 데이터를 암호화해서 통신합니다. 443번 포트를 사용하며, 주로 대칭키와 비대칭키를 함께 사용해 보안성과 성능을 모두 확보합니다. 브라우저는 CA에서 발급한 인증서를 통해 서버의 신뢰성을 검증

---

# HTTP/1.1과 HTTP/2의 차이점에 대해 설명해주세요.
![alt text](image-1.png)

## HTTP/1.1
- 현재까지 가장 널리 사용되는 HTTP 프로토콜
- 요청/응답 모델을 사용(클라이언트가 서버에 요청, 서버가 클라이언트에 응답)
- 기본적으로 Connection당 하나의 요청을 처리하도록 설계
- 동시 전송 불가능하고 요청과 응답이 순차적 
- HTTP 문서 안에 포함된 다수의 리소스(Image, CSS, Script)를 처리하려면 요청할 리소스 개수에 비례해서 Latency(대기 시간) 길어짐

<br>

## HTTP2
- HTTP1.1의 단점을 보완하고 성능을 개선하기 위해 개발된 프로토콜
- 바이너리 프로토콜(Binary Protocol) 사용 : 바이너리 프레이밍 계층으로 성능 최적화
- 멀티플렉싱(Multiplexing) : 한 커넥션으로 동시에 여러 개의 메세지를 주고 받을 수 있으며, 응답은 순서에 상관없이 stream으로 주고 받음
- Servcer Push : 서버는 클라이언트의 요청에 대해 요청하지도 않은 리소스를 보내줄 수 있음
- Header Compression : Header 정보를 압축하기 위해 Header Table과 Huffman Encoding 기법을 사용하여 처리하는데 이를 HPACK 압축방식이라 부르며 별도의 명세서(RFC 7531)로 관리

<br>

### ✨ 정리 포인트
HTTP/1.1은 하나의 커넥션에서 요청을 순차적으로 처리해 **지연(latency)**이 큽니다.
반면, HTTP/2는 하나의 커넥션에서 여러 요청을 **동시에 처리(Multiplexing)**할 수 있어 성능이 훨씬 개선

---

# REST API란 무엇이며, RESTful한 API를 설계하는 원칙에 대해 설명해주세요

## REST API
- REST (REpresentational State Transfer)는 웹 서비스가 어떻게 동작해야 하는지에 대한 아키텍처 스타일 또는 설계 원칙
- REST는 클라이언트와 서버 간의 상호작용을 규정하며, 여러 가지 원칙과 제약 조건들을 가지고 있음
- 웹상의 자원을 이름으로 구분하고 해당 자원의 상태를 주고 받는 모든 것을 의미. HTTP 프로토콜을 그대로 활용하는 아키텍처
- HTTP 메소드 활용(GET,POST,PUT,PATCH,DELETE)
- HTTP 응답 상태 코드 활용

<br>

## RESTful API
- REST 아키텍처 스타일을 따르는 웹 API. 즉 REST 원칙을 잘 지키며 설계된 API를 RESTful API라 한다

<br>

### ✨ 정리 포인트
- REST는 이론적인 원칙과 가이드(클라이언트-서버 구조)
- RESTful API는 그 원칙과 가이드라인을 실제로 적용한 API를 의미
