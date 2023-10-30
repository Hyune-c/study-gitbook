# HTTP 구성

![](../../../../../.gitbook/assets/2021-07-09-17-16-44.png)

* Header 와 Body 는 `CR(carriage return, 0x0d) + LF(line feed, 0x0a)` 를 기준으로 값이 나뉩니다.

## Start line

* Request: request line

```
POST / HTTP/1.1
메소드 요청URL 프로토콜버전
```

* Response: status line

```
HTTP/1.1 200 OK
프로토콜버전 상태코드 상태코드설명
```

### HTTP Method

| Method  | Desc            |
| ------- | --------------- |
| GET     | 리소스 획득          |
| POST    | 엔티티 전송          |
| PUT     | 파일 전송           |
| HEAD    | 메시지 헤더 취득       |
| DELETE  | 파일 삭제           |
| OPTIONS | 제공하고 있는 메소드의 문의 |
| TRACE   | 경로 재조사          |
| CONNECT | 프록시에 터널링 요구     |

### HTTP Headers

> General Header

요청/응답 모두에서 사용 가능한 일반 목적의 항목입니다

| Field         | Desc                                                                                                |
| ------------- | --------------------------------------------------------------------------------------------------- |
| Date          | 메시지가 발생한 날짜와 시간을 포함합니다.                                                                             |
| Connection    | 트랜잭션이 끝난 후의 연결 상태를 제어합니다.                                                                           |
| Cache-Control | 요청과 응답 모두에서의 캐싱 메커니즘을 명시하는 지시문.                                                                     |
| Pragma        | 요청-응답 체인을 따라 어디든 다양한 영향을 줄 수 있는 구현-관련 헤더. `Cache-Control` 헤더가 존재하지 않는 HTTP/1.0 캐시와의 하위 호환성을 위해 사용됨. |
| Trailer       | 전송자가 청크 분할된 메시지의 끝에 부가적인 필드를 포함할 수 있게 해줍니다.                                                         |

> Request Header

요청 메세지 내에서만 나타나며 가장 방대합니다.

| Field             | Desc                                                                                         |
| ----------------- | -------------------------------------------------------------------------------------------- |
| Host              | 서버(가상 호스팅용)의 도메인명과 (선택적으로) 서버가 리스닝중인 TCP 포트 번호를 명시합니다.                                       |
| From              | 요청하는 유저 에이전트를 제어하는 사용자(사람)의 인터넷 이메일 주소를 포함합니다.                                               |
| Cookie            | Set-Cookie 헤더와 함께 서버로부터 이전에 전송됐던 저장된 HTTP 쿠키를 포함합니다.                                         |
| Referer           | 현재 페이지로 연결되는 링크가 있던 이전 웹 페이지의 주소입니다.                                                         |
| User-Agent        | 네트워크 프로토콜 피어가 요청하는 사용자 에이전트의 애플리케이션 타입, 운영 체제, 소프트웨어 벤더 또는 소프트웨어 버전을 식별할 수 있는 특성 문자열을 포함합니다. |
| Accept            | 돌려줄 데이터 타입에 대해 서버에 알립니다. MIME 타입입니다.                                                         |
| If-Modified-Since | 주어진 날짜 이후에 수정된 경우에만 요청을 조건부로 만들고 엔티티가 전송될 것을 기대합니다. 캐시가 만료되었을 때에만 데이터를 전송하는데 사용됩니다.          |

> Response Header

특정 유형의 HTTP 요청/헤더를 수신했을때, 이에 응답합니다.

| Field              | Desc                                                                                           |
| ------------------ | ---------------------------------------------------------------------------------------------- |
| Server             | 요청을 처리하기 위해 오리진 서버에 의해 사용되는 소프트웨어에 대한 정보를 포함합니다.                                               |
| Set-Cookie         | 서버에서 유저 에이전트로 쿠키를 전송합니다.                                                                       |
| Accept-Ranges      | 서버가 범위 요청을 지원하는지를 나타내며, 지원할 경우 범위가 표현될 수 있는 단위를 나타냅니다.                                         |
| Age                | 객체가 프록시 캐시에 있었던 초 단위의 시간.                                                                      |
| ETag               | 리소스의 버전을 식별하는 고유한 문자열 검사기입니다. If-Match 와 If-None-Match 를 사용하는 조건부 요청은 이 값을 사용하여 요청의 동작을 변경합니다. |
| Proxy-Authenticate | 프록시 서버 뒤에 있는 리소스에 접근하는데 사용되어야하는 인증 메소드를 정의합니다.                                                 |

> Entity Header

요청/응답 모두에서 사용가능하며, 개체를 설명합니다.

### HTTP Body

* empty line 을 기준으로 나뉩니다.
* 한 줄로 연속된 데이터를 가지고 있습니다.

## Cookie vs Session

stateless 의 문제점을 보완하기 위한 방식이지만, 두 방식 모두 보안 위협이 존재하기에 OAuth, JWT 방식이 나왔습니다.

|          | Cookie            | Session |
| -------- | ----------------- | ------- |
| Stored   | Browser in Client | Server  |
| Security | 변조의 위험성           | 탈취의 위험성 |