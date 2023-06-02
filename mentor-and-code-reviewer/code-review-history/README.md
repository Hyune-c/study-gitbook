---
description: 진행했던 코드 리뷰 중 의미 있는 것들을 기록합니다. - Codesquad, Codestates, Programmers
---

# Code Review History

### JPA entity 의 식별자 기본 생성 전략 선택

{% content-ref url="../../study/framework-and-library/jpa/generatedvalue-strategy.md" %}
[generatedvalue-strategy.md](../../study/framework-and-library/jpa/generatedvalue-strategy.md)
{% endcontent-ref %}



### Entity 의 field type 은 무엇이 적절한가?

{% content-ref url="../../study/framework-and-library/jpa/entity-field-type.md" %}
[entity-field-type.md](../../study/framework-and-library/jpa/entity-field-type.md)
{% endcontent-ref %}



### `@Controller` 클래스 레벨에 `@RequestMapping` 을 명시하는 것

`nit`

* 저는 RequestMapping을 클래스 레벨로 묶는 것을 선호하지 않습니다.
* 경험상 에러가 발생하면 url을 통해 엔드포인트로 바로 가고 싶은 니즈가 있는데, 이렇게 분리되면 복붙이 불편했습니다.



### GET 메서드에 payload 를 사용한 것

{% content-ref url="../../study/computer-science/web/rest-api/get-payload.md" %}
[get-payload.md](../../study/computer-science/web/rest-api/get-payload.md)
{% endcontent-ref %}



### Builder Pattern 사용

{% content-ref url="../../study/computer-science/design-pattern/builder-pattern.md" %}
[builder-pattern.md](../../study/computer-science/design-pattern/builder-pattern.md)
{% endcontent-ref %}



### API 설계는 어떻게 해야 되는가?

{% content-ref url="../../study/computer-science/web/rest-api/api.md" %}
[api.md](../../study/computer-science/web/rest-api/api.md)
{% endcontent-ref %}



### 현재는 access token(JWT)만 내려주고 있지만, 추후에는 refresh token도 추가해 볼 생각입니다. 두 토큰이 똑같이 `authId`와 `expired_time`만을 갖게 하려고 했는데, access token과 refresh token과 차이를 나게하는 부분이 `expired_time`만 있게 해도 되는지 잘 모르겠습니다. (둘을 구분할 수 있는 속성이 더 있어야 하는지?)

![](<../../.gitbook/assets/image (5) (2).png>)

* 보통 **claims**를 활용합니다. **registerd claims**를 활용한 예시를 첨부합니다.



### `TimeZone.setDefault(TimeZone.getTimeZone("GMT"));` 에 대한 리뷰

> For most purposes, UTC is considered interchangeable with Greenwich Mean Time (GMT), but GMT is no longer precisely defined by the scientific community.

* **UTC** 명시를 권장합니다.

{% embed url="https://www.baeldung.com/java-time-zones" %}

###

### DB에서 `TIMESTAMP`와 `DATETIME` 타입의 차이

{% embed url="https://hyune.gitbook.io/hyune-wiki/mentor-and-code-reviewer/code-review-history/db-timestamp-datetime" %}



### 한방 쿼리 vs 애플리케이션에서 조립

{% embed url="https://hyune.gitbook.io/hyune-wiki/mentor-and-code-reviewer/code-review-history/vs" %}



### java spring init 설명

{% embed url="https://github.com/Hyune-s-lab/java-spring-init" %}

* api 스펙을 공유하고 수정함에 있어 생산성을 고려해야 합니다.
  * swagger 를 통해 코드와 밀접하게 관리할 수 있다.
* docker compose 활용을 권장합니다.
  * local 세팅으로 프로젝트를 띄우기에 가장 쉬운 방법이다.
* readme 를 잘 활용해야 합니다.
  * 면접관은 readme 와 프로젝트 구조를 보고 더 볼지를 판단한다.



### 인증을 어떻게 해야되나?

* 커리큘럼상 security 를 학습했지만, 지금 사용하기에는 너무 어려운 기술이다. 추천하지 않는다.
* OAuth2 에 대해 학습은 좋지만, 구현은 추천하지 않는다.
* session 구성을 권장한다.



### 레이어 구분과 dto

{% embed url="https://hyune.gitbook.io/hyune-wiki/code-reviewer-and-mentoring/codesquad/undefined/service-dto" %}



### 백엔드 개발 환경 설정

{% embed url="https://hyune-c.tistory.com/entry/%EB%B0%B1%EC%97%94%EB%93%9C-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD%EC%9D%84-%EC%84%B8%ED%8C%85%ED%95%B4%EB%B3%B4%EC%9E%90" %}



### 지속적인 기술 정보 얻기

* RSS

{% embed url="https://hyune-c.tistory.com/entry/RSS%EB%A1%9C-%EB%B8%94%EB%A1%9C%EA%B7%B8%EB%A5%BC-%EB%AA%A8%EC%95%84%EB%B3%B4%EC%9E%90" %}

* 커리어리

{% embed url="https://careerly.co.kr/" %}

###

### 코드 리뷰

{% embed url="https://github.com/codestates-seb/seb39_main_023/pull/6" %}



### 멘토링 개선 의견

> 페어와의 기술 선택 협의에 작은 어려움이 있다. 리뷰시 더 강한 표현을 해주셨으면 좋겠다.&#x20;

페어로 작업을 하다보면 어느 한쪽의 의견이 강하거나, 기술 선택에 욕심이 생길 수 있습니다.\
아쉽지만 위 내용의 조율은 제가 개입하기 힘듭니다. 실제로 제 의견은 중요하지 않구요.\
제가 드릴 수 있는 가이드는 아래 정도 일 것 같습니다.&#x20;

* 현재의 과정에서 최신 기술의 도입은 전혀 중요하지 않다.&#x20;
  * 내부를 잘 모르는 외부 라이브러리의 도입보다는, 시간이 걸리더라도 내부를 직접 구현해보는 것을 추천한다.
* 기능을 최대한 줄여라. 최소 기능이 구현된 후에 추가 기능을 고민하면 된다.
  * 본인들이 지금 생각하는 것보다 더 기능을 줄여야한다. 극단적으로 CRUD 만 해도 좋다.

> 라이브 세션 전에 주제를 공유하면 좋겠다.

본 gitbook 을 지속적으로 업데이트하겠습니다.\
메이저 변경이 있는 경우 채널로 노티하고, 최소 D-1 에는 완성본을 공유할 수 있도록 하겠습니다.



### PR 의 단위와 브랜치 활용에 대해

멘티님들 입장에서는 `코멘트가 남아있으니 다 수정하고 머지해야 되는 것 아니냐?` 고 말할 수도 있습니다. 하지만 0주차에 말한 것 처럼 제 코멘트를 모두 수용할 필요는 없습니다. 필요에 따라 본인의 생각을 관철하셔도 좋습니다.

그리고 한번 열린 pr 이 몇 번의 핑퐁을 거쳤음에도 닫히지 않는다는건 pr 의 단위가 너무 큰 것이 아닌가 고민하셔야 됩니다. 어렵겠지만 다수의 피쳐를 다수의 브랜치를 활용해 다수의 pr 을 올릴 수 있어야 합니다. 이것은 개발자가 많아지면 당연한 수순이고, 자연스럽게 컨플릭트를 피하기 위해 SRP 와 같은 설계를 고민하게 됩니다.

고급 기술 스택의 활용보다 이런 일련의 과정을 아시는 것이 더 중요하다고 생각합니다.



### `@Controller` 클래스 레벨에 `@RequestMapping` 을 명시하는 것

{% embed url="https://hyune.gitbook.io/hyune-wiki/code-reviewer-and-mentoring/codesquad/airbnb#controller-requestmapping" %}



### Entity 의 field type  primitive, wrapper 중 어느 것이 적절한가?

{% embed url="https://hyune.gitbook.io/hyune-wiki/framework-and-library/jpa/entity-field-type" %}



### 목적이 있는 문서를 작성하고 공유해라

* API 명세 공유 방법을 고민하는 동료를 위해 방법을 찾음.

{% embed url="https://hyune.gitbook.io/hyune-wiki/and/openapi-swagger-3.0/undefined" %}



### 클린 코드를 공부해라.

* **클린 코드, 이펙티브 자바** 보다는 입문서로 **엘레강트 오브젝트**를 추천합니다.



### JPA Entity 연관 관계를 어떻게 작성해야 될까?

* JPA 의 기능들을 모두, 잘 써야만 된다는 생각에 대해서 입니다.
* 최범균님 유튜브의 `JPA 기초`는 모두 시청하기를 권장합니다.

{% embed url="https://www.youtube.com/watch?v=rZZSYG__8Jc&list=PLwouWTPuIjUi9Sih9mEci4Rqhz1VqiQXX&index=13" %}



### 테스트

* 풍부한 단위 테스트는 좋은 설계가 전제되어야 하고 테스트 객체에 대한 이해가 필요해 꽤 힘든 일입니다.
* 현재 단계에서는 유스 케이스 기준의 시나리오 테스트를 추천합니다.
* 테스트 더블에 대해 공부하는 것도 좋습니다. fixture, stub 위주



### 서버에 파일을 직접 저장하는 구현에 대해

* 분산 환경에 적합하지 않습니다.
  * 파일 저장 요청을 통해 A 서버 파일이 저장됩니다. (murtipart)
  * 파일 불러오기 요청이 B 서버로 가면 A 서버의 파일을 가져올 수 있을까요?
* 실무에서는 보통 S3 를 활용합니다.
  * 세션 클러스터링의 접근법을 공부하시면 좋습니다.
* 만약 업무 요건 상 온프레미스로 구현해야 한다면 2가지 정도의 방법이 있을 것 같습니다.
  * 중앙 저장 공간을 구성한다. ex) NAS
  * DB 에 blob type 으로 저장한다.&#x20;



### &#x20;중괄호 개행에 대해

{% embed url="https://google.github.io/styleguide/javaguide.html" %}
4.1.2 Nonempty blocks: K & R style
{% endembed %}

{% embed url="https://naver.github.io/hackday-conventions-java/#braces" %}
5.1. K\&R 스타일로 중괄호 선언
{% endembed %}



### 추가 사이드 프로젝트 진행에 대해

{% hint style="info" %}
제일 좋은 것은 지인이나 closed 한 커뮤니티에서 직접 모집하는 것 입니다.
{% endhint %}

{% embed url="https://www.inflearn.com/community/studies?order=score" %}

* 최근 가장 핫한 커뮤니티.
* 하지만 태그 기능이 빈약하고 학생들 위주라 그런가 프론트 위주임.

{% embed url="https://okky.kr/events/gathering" %}

* 전통의 강자 커뮤니티
* 리뉴얼이 되어도 올드한 느낌이 나긴 하지만, 근본 Java 로 시작한 커뮤니티라 백엔드가 많음.
* 단 광고나 MVP 개발을 위한 글도 있으니 주의.



### Bean Validation 실수

<figure><img src="../../.gitbook/assets/image (3) (2).png" alt=""><figcaption></figcaption></figure>

{% embed url="https://github.com/Hyune-s-lab/bean-validation" %}



### 리소스 정의에 대해

<figure><img src="../../.gitbook/assets/image (1) (4).png" alt=""><figcaption></figcaption></figure>



### 인프콘 2022 에서 재미있는 주제

#### 마인드셋에 대해

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

* 업무라는 것에 대해 접근하는 생각

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

* 기업의 간판은 전혀 중요하지 않다. **나에게 필요한 무엇을 경험할 수 있는** 곳이 중요하다.
* 소프트웨어만 지속적인 것이 아니다. **나 역시도 지속적이어야하기** 때문이다.

#### 멀티모듈에서 나오는 레이어 분리

<figure><img src="../../.gitbook/assets/image (1) (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (2) (3).png" alt=""><figcaption></figcaption></figure>



### 프로그래밍의 옳고 그름이란

{% embed url="https://github.com/Programmers-Hyune-c/cosmic-baseball-init/pull/18#pullrequestreview-1280893817" %}

<figure><img src="../../.gitbook/assets/image (1) (6).png" alt=""><figcaption></figcaption></figure>



### if-else 개선하기

{% embed url="https://github.com/Programmers-Hyune-c/cosmic-baseball-init/pull/27#discussion_r1106583993" %}



### nullable 객체의 예외 처리에 대해

{% embed url="https://github.com/Programmers-Hyune-c/cosmic-baseball-init/pull/28#discussion_r1106628152" %}



### 테스트를 위해 운영 코드를 수정해도 될까?

결론부터 얘기하면 `수정해도 된다` 입니다.\
하지만 수정의 목표는 설계를 좋게하기 위함이지, 테스트를 하기 위함이어서는 안됩니다.

{% embed url="https://stackoverflow.com/questions/55606889/is-it-best-practice-to-modify-the-production-code-to-be-testable-solely-for-te" %}

{% embed url="https://smelting.tistory.com/76" %}



### TDD 를 꼭 해야 되는 것인가?

변경이 잦은 초기 개발 단계에는 어울리지 않을 수도 있다.

<img src="../../.gitbook/assets/image (1).png" alt="" data-size="original">

{% embed url="https://www.linkedin.com/posts/gyuwonyi_%EC%B2%9C%EC%95%88%EA%B0%80%EB%8A%94-%EB%B2%84%EC%8A%A4%EB%A5%BC-%EA%B8%B0%EB%8B%A4%EB%A6%AC%EB%A9%B0-%EB%8C%80%EA%B8%B0%EC%97%85-tdd-%EA%B0%95%EC%9D%98-%EC%9A%94%EC%B2%AD%EC%97%90-%EB%B9%A0%EB%A5%B4%EA%B2%8C-%EB%8B%B5%EC%9E%A5-%EB%A9%94%EC%9D%BC%EC%9D%84-%EC%9E%91%EC%84%B1%ED%96%88%EB%8B%A4-activity-7039886755776401408-IHBd?utm_source=share&utm_medium=member_desktop" %}



### RequestMapping 의 value 표현에 대해

```java
@GetMapping("/")
@GetMapping("")
@GetMapping
```

SpringBoot 2 (Spring 5) 까지는 큰 문제가 없지만 SpringBoot 3 (Spring 6) 부터는 문제가 될 수 있습니다.

{% embed url="https://www.baeldung.com/spring-boot-3-url-matching" %}
