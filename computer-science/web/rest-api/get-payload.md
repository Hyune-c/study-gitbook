# GET 메서드에 payload를 사용해도 되는가?

![](<../../../.gitbook/assets/image (9).png>)

* MDN에는 GET에 payload를 허용하긴 하지만 권장하지 않는다고 합니다.

![](<../../../.gitbook/assets/image (3) (2).png>)

* wikipedia에는 Optional로 작성되어 있습니다.

![](<../../../.gitbook/assets/image (8).png>)

* RFC에는 MDN과 같은 내용이 적혀 있습니다.

여기까지 종합해보면 결론은 `사용은 가능하지만 권장하지 않는다.` 가 되는 것 같습니다.



추가 정보로 스택 오버플로우 대화 내용의 일부를 요약합니다.

* 초기에는 payload를 사용하지 않는 것을 **SHOULD**로 명시했지만, 최신 버전에서는 삭제되었습니다.
* 알려진 API 설계 의도에 어긋납니다.
  * 이는 개발자간의 미스 커뮤니케이션만이 아니라 이미 개발된 모듈에도 영향을 받을 수 있습니다.
* 반면 엘라스틱서치에서는 대놓고 사용하기도 합니다.
  * [https://www.elastic.co/guide/en/elasticsearch/guide/current/\_empty\_search.html](https://www.elastic.co/guide/en/elasticsearch/guide/current/\_empty\_search.html)

![](<../../../.gitbook/assets/image (14) (1).png>)

{% embed url="https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/GET" %}

{% embed url="https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods" %}

{% embed url="https://www.rfc-editor.org/rfc/rfc7231#section-4.3.1" %}

{% embed url="https://stackoverflow.com/questions/978061/http-get-with-request-body" %}

