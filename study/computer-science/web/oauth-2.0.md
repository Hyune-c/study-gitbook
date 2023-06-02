# OAuth 2.0

## Authorization Code Grant

> 권한 부여 승인 코드 방식

![](<../../../.gitbook/assets/image (10) (1).png>)

* 자체 생성한 권한 부여 승인 코드를(Authorization Code) 전달하는 방식으로 기본이 되는 방식입니다.&#x20;
  * Authorization Code 획득 후 해당 Code로 Access Token 획득해야 합니다.
  * 사용자의 권한 요청 승인 후 지정된 url로 콜백이 옵니다.
* 간편 로그인에서 사용되는 방식으로 클라이언트가 사용자를 대신하여 특정 자원에 접근을 요청할 때 사용되는 방식입니다.
  * 보통 타사의 클라이언트에게 보호된 자원을 제공하기 위한 인증에 사용됩니다.&#x20;
* Refresh Token의 사용이 가능한 방식입니다.

## &#x20;Implicit Grant&#x20;

> 암묵적 승인 방식

![](<../../../.gitbook/assets/image (4).png>)

* 자격 증명을 안전하게 저장하기 힘든 클라이언트에 적합한 방식입니다.
  * ex: JavaScript등의 스크립트 언어를 사용한 브라우저
* 암시적 승인 방식에서는 Authorization Code 없이 바로 Access Token이 발급 됩니다.&#x20;
  * Access Token이 바로 전달되므로 일회성이고 만료기간을 짧게 설정하는 것을 권장합니다.
* Refresh Token 사용이 불가능한 방식이며, 이 방식에서 권한 서버는 client\_secret를 사용해 클라이언트를 인증하지 않습니다.&#x20;

## Resource Owner Password Credentials Grant&#x20;

> 자원 소유자 자격증명 승인 방식

![](<../../../.gitbook/assets/image (13) (1).png>)

* username, password로 Access Token을 받는 간단한 방식입니다.
* 인증 정보를 모두 보유하고 있는 서비스에서 사용되는 인증 방식입니다.&#x20;
* Refresh Token의 사용도 가능합니다.

## **Client Credentials Grant**

> &#x20;클라이언트 자격증명 승인 방식

![](<../../../.gitbook/assets/image (1) (1) (2).png>)

* 클라이언트의 자격 증명만으로 Access Token을 획득하는 방식입니다.
* OAuth2의 권한 부여 방식 중 가장 간단한 방식입니다.
  * 클라이언트 자신이 관리하는 리소스 혹은 권한 서버에 해당 클라이언트를 위한 제한된 리소스 접근 권한이 설정되어 있는 경우 사용됩니다.
* 이 방식은 자격증명을 안전하게 보관할 수 있는 클라이언트에서만 사용되어야 합니다.
* Refresh Token은 사용할 수 없습니다.



{% embed url="https://blog.naver.com/mds_datasecurity/222182943542" %}

{% embed url="https://datatracker.ietf.org/doc/html/rfc6749" %}
