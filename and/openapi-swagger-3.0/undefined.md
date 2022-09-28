# 정적 문서 내보내기

{% hint style="info" %}
swagger 를 작성하는 프로젝트의 경우 보통 url 전달로 API 명세를 소통합니다.\
하지만 망 분리 등의 이슈로 직접 접근이 불가능한 경우 부득이하게 문서를 전달해야 되는 경우가 있습니다.\
\
이 때 만약 명세를 위한 문서를 별도로 작성한다면 **문서와 실제 API 의 간극이 발생합니다.**\
다행히 swagger 는 이를 보완하기 위한 기능을 제공하고 있습니다.
{% endhint %}

### 1. boot sample project with swagger

* 3개의 sample API 구현
* sample respone spec 확인 가능

<figure><img src="../../.gitbook/assets/image (3) (3).png" alt=""><figcaption></figcaption></figure>

### 2. export schema (json)

* url 가져오기
  * `/v3/api-docs` 링크를 누르거나
  * console 에서 명령어를 통해 url 을 가져옵니다.

```java
// 3.x
> ui.getConfigs().url

// 2.x
> swaggerUi.api.url
```

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

### 3. check schema

![](<../../.gitbook/assets/image (1) (3) (1).png>)

### 4. convert to document

* [https://editor.swagger.io/](https://editor.swagger.io/)
* json 을 붙여넣기만 하면 완성!

<figure><img src="../../.gitbook/assets/image (2) (3).png" alt=""><figcaption></figcaption></figure>

* 필요시 yml 전환 가능

<figure><img src="../../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

### Reference

{% embed url="https://stackoverflow.com/questions/48525546/how-to-export-swagger-json-or-yaml" %}

{% embed url="https://www.baeldung.com/spring-rest-openapi-documentation" %}
