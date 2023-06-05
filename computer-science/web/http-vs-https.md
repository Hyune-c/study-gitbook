# HTTP vs HTTPS

## HTTP (Hyper Text Transfer Protocol)

인터넷에서 하이퍼텍스트를 교환하기 위한 통신 규약으로, 80번 포트를 사용합니다.

* Stateless 프로토콜이며 Method, Path, Version, Headers, Body 등으로 구성됩니다.
* 암호화가 되지 않은 평문 데이터 전송 프로토콜로 보안에 취약합니다.

## HTTPS (Hyper Text Transfer Protocol Secure)

> HTTP (Hyper Text Transfer Protocol) + SSL (Secure Soket Layer)

HTTP 에 데이터 암호화가 추가된 프로토콜으로 공개키 암호화를 지원하며 433번 포트를 사용합니다.

### 공개키 암호화 vs 개인키 암호화

* 공개키 암호화: 공개키로 암호화를 하면 개인키로만 복호화할 수 있습니다.
  * 공개키는 모두에게 공개된 키 입니다.
  * 개인키는 나만 가지고 있으므로, 나만 볼 수 있습니다.
* 개인키 암호화: 개인키로 암호화하면 공개키로만 복호화할 수 있습니다.
  * 개인키는 나만 가지고 있는 키 입니다.
  * 공개키는 모두에게 공개되어 있으므로, 내가 인증한 정보임을 알려 신뢰성을 보장할 수 있습니다.

### SSL 인증서 작동 원리

* 실제 데이터 : 대칭키
* 대칭키의 키 : 공개키

![](../../.gitbook/assets/2021-07-07-02-30-26.png)
