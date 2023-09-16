## Q. HTTP에 대해 설명해 주세요

## A. HTTP(HyperText Transfer Protocol)는 인터넷 상에서 정보를 주고받을 때 사용되는 통신 규약(protocol)입니다!

### HTTP

인터넷에서 데이터를 전송하기 위해 사용되는 프로토콜

클라이언트와 서버 간에 요청과 응답을 주고받는 방식으로 동작.

요청 메시지는 요청하는 페이지의 주소(URL), 요청의 종류(Method, GET, POST 등), 그리고 추가적인 정보(Header, Body)등을 포함.

응답 메시지는 상태코드(200 OK, 404 Not Found), 헤더 정보, 요청한 데이터(웹 페이지의 HTML 내용)등을 포함.

## 꼬리 질문

### HTTP의 주요 특징에 대해 설명해 주세요

<details>
<summary></summary>
<div markdown="1">

- 클라이언트 서버 구조
    - 클라이언트는 서버에 요청을 보내고 응답 대기, 서버는 요청에 대한 결과를 만들어 응답하는 구조
    - 양 쪽이 독립적으로 실행될 수 있음

- 무상태 프로토콜(Stateless)
    - 서버가 클라이언트의 상태를 보존하지 않음
    - 장점: 서버의 확장성이 높아짐 (스케일 아웃)
    - 단점: 클라이언트가 추가 데이터를 전송해야 해서 주고받아야 하는 데이터가 많아짐
- 비 연결성(Connectionless)
    - 기본 매커니즘은 연결을 유지하지 않음
    - TCP/IP 연결 시 모든 과정에서 연결/종료 과정이 포함됨
    - HTTP 지속 연결 (Persistent Connecions)로 문제 해결

</div>
</details>

### HTTP Method의 멱등성에 대해 설명해 주세요.

<details>
<summary></summary>
<div markdown="1">

- 여러 번 수행해도 항상 같은 결과를 얻을 수 있는 특성

- 멱등한 메서드를 사용하면 동일한 요청을 여러번 수행하더라도 응답이 일관되므로, 장애 복구, 네트워크 문제, 요청 재시도와 같은 상황에서 안정성과 예측 가능성을 보장할 수 있다.

- GET, PUT, DELETE 가 이에 해당함

</div>
</details>

### Stateless와 Connectionless에 대해 설명해 주세요.

<details>
<summary></summary>
<div markdown="1">

- Stateless
    - 각각의 요청이 서로 독립적으로 처리
    - 상태를 유지하지 않는 프로토콜 → 상태 정보가 서버에 저장되지 않는다
    - 서버에 부담을 줄일 수 있다.
    - 상태 정보가 필요한 경우에는 쿠키, 세션, 토큰 등의 기술을 사용

- Connectionless: 연결을 유지하지 않는 프로토콜 동작
    - 각각의 요청과 응답을 독립적으로 처리하는 방식 ex) UDP
    - 간단하고 빠른 데이터 전송이 필요한 경우에 유용

</div>
</details>

### HTTP는 왜 Stateless 구조를 채택하고 있을까요?

<details>
<summary></summary>
<div markdown="1">

- 서버에 상태 구조를 저장하지 않으므로 많은 수의 클라이언트와 동시에 연결 처리 가능
- 장애 복구 및 부하 분산을 용이하게 하게 된다.
- 서버는 요청에 대한 응답만 생성하면 되기 떄문에 구현이 단순해지고, 유지보수 및 업그레이드가 용이해진다
- 다양한 클라이언트 플랫폼과의 상호 운용성을 높여준다.

</div>
</details>

### HTTP Persistence Connection이 무엇인가요?

<details>
<summary></summary>
<div markdown="1">

- 여러 개의 HTTP 요청과 응답을 단일 TCP 연결(connection)을 통해 처리하는 메커니즘
- 네트워크 비용 및 성능 개선을 목적으로 도입
- 필수적으로 진행되는 여러 개의 HTTP 요청을 하나의 conneciton으로 묶는다.
- TCP 연결 설정과 해제의 오버헤드 줄이고, 네트워크 대역폭 절약 가능
- 웹 페이지의 로딩 속도와 서버 성능도 향상 가능
- HTTP 1.1 에서 기본적으로 활성화되어 있음.

</div>
</details>

### HTTP 1.1과 HTTP 2.0의 차이는 무엇인가요?

<details>
<summary></summary>
<div markdown="1">

- 기존 1.X 버전의 성능 향상에 초점 → 따라서 표준의 대체가 아닌 확장의 개념
- 기존의 일반 텍스트 형식 → 보내는 메시지를 `Frame` 단위로 분할 후 `Binary Encording` 진행
    - 파싱 및 전송 속도 상향, 오류 발생 가능성 감소의 효과
  
- `Mutiplexed Streams`
    - 하나의 connection 안에 여러 개의 stream이 존재
    - 조각난 frame을 여러 개의 stream을 통해 전달한다. → 다중화(Mutiplexing) 이 가능해짐!
  
- `Header Compression`
    - 기존: 연속된 요청의 경우 중복된 헤더 전송으로 오버헤드 발생
    - 전송되는 헤더 필드를 서버에서 유지
    - 이전에 표시된 헤더를 제외한 필드를 허프만 인코딩 수행해 압축
  
- 한계점
    - TCP 고유의 HOL Blocking이 존재. 이건 어떻게 못함
    - 서로 다른 stream이 전송되고 있을 때, 하나의 Stream에서 유실이 발생하거나 문제가 생기면 다른 Stream도 재전송 또는 지연되는 현상이 발생하기 때문
    - 이러한 태생적인 문제점을 해결하기 위해 QUIC / HTTP 3.0 등장

</div>
</details>

### HOLB에 대해 설명해 주세요.

<details>
<summary></summary>
<div markdown="1">

Head Of Line Blocking

웹에서 HOL Blocking을 말할 때에는 두 가지 종류가 있다.

- HTTP에서의 HOL Blocking
  - 요청-응답 쌍은 항상 순서를 유지하고 동기적으로 수행되어야 한다.
  - 이전의 요청이 처리되지 않았다면 그 다음 요청은 보낼 수 없다는 뜻
- TCP에서의 HOL Blocking
  - TCP는 패킷을 전송할 때에, 전달을 보장하기 때문에 패킷이 손실되면 재전송하게 된다.
  - 그리고 재전송이 발생하면 패킷의 순서가 역전되지 않도록 후속 패킷이 대기하게 된다.
  - 즉, TCP 상에서 3개의 패킷을 보낼 때, 먼저 보낸 패킷에서 손실이 발생하면 뒤도 막히게 된다.


</div>
</details>

### TCP의 keep-alive와 HTTP의 keep-alive의 차이는 무엇인가요?

<details>
<summary></summary>
<div markdown="1">

- TCP의 keep-alive는 네트워크 계층에서 작동하는 메커니즘으로, TCP 연결이 유지되는 동안 통신이 지속되고 있는지 확인하는 목적으로 사용
- 일정 시간마다 Keep-Alive 패킷을 보내 확인하고, 응답을 받지 못하면 연결을 종료한다.

</div>
</details>

### HTTP 1.1 이후로, GET에도 Body에 테이블을 실을 수 있게 되었습니다. 그럼에도 불구하고 왜 아직도 이런 방식을 지양하는 것일까요?

<details>
<summary></summary>
<div markdown="1">

1. 호환성과 보안
    - 일부 웹 서버 및 브라우저는 지원하지 않을 수도 있다.


2. 캐싱 및 쿼리 문자열 제한
    - GET의 Boby를 추가하면 캐싱이 어려워질 수 있다.
    - 쿼리 문자열의 길이 제한에도 영향을 줄 수 있다.


3. 의미론적인 측면

</div>
</details>

### Status Code 401과 403은 의미적으로 어떤 차이가 있나요?

<details>
<summary></summary>
<div markdown="1">

- HTTP 401 Unauthorized (권한 없음)
    - 클라이언트에게 인증 정보가 없음


- HTTP 403 Forbidden (금지됨):
    - 인증을 수행했지만 요청한 리소스에 대한 권한이 없음
    - 서버가 엑세스를 의도적으로 거부했다는 것을 나타냄

</div>
</details>

### HTTP 3.0의 주요 특징에 대해 설명해 주세요.

<details>
<summary></summary>
<div markdown="1">

1. 프로토콜 변경
    - 기존의 TCP를 사용하는 것이 아닌 QUIC프로토콜을 기반으로 동작


2. 다중화된 스트림
    - 한 번의 연결을 통해 여러 개의 독립적인 스트림을 동시에 전송할 수 있음
    - 병렬로 데이터를 전송하여 성능을 향상


3. 오류 복구 기능
    - 자체적으로 오류 복구 메커니즘을 활용하여 데이터의 손실을 최소화하고 신뢰성 유지


4. 향상된 보안
    - TLS 암호화를 사용하여 통신을 보호, QUIC 프로토콜 자체가 암호화를 지원하므로 추가적일 설정 없이 암호화된 연결을 제공함

</div>
</details>

## 참고 자료 및 레퍼런스

- 노션 개인 정리 자료
- [What is HTTP? - Cloudflare](https://www.cloudflare.com/ko-kr/learning/ddos/glossary/hypertext-transfer-protocol-http/)
- [HTTP/2 in Action - i4song](https://velog.io/@dnr6054/HOL-Blocking)
