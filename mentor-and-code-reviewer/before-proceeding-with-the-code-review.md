# 진행하기에 앞서..

{% hint style="info" %}
개발에 대한 생각은 개발자마다, 심지어 대가들 끼리도 미묘하게 다릅니다. \
저의 멘토링 & 코드 리뷰는 당연하게도 저의 지극히 개인적인 관점과 경험에서 진행됩니다. \
그렇기에 멘티는 다양한 의견을 듣고 본인에 적합한 피드백을 스스로 선택하기를 기대합니다.
{% endhint %}



### 개발 환경 세팅 추천

{% embed url="https://hyune-c.tistory.com/29" %}



### REST API 설계를 어느 수준으로 해야될까

#### 리얼 월드에 RESTful API 는 없다.

* RESTful API 설계는 리소스 단위의 접근으로 클라이언트에게 자유도를 주기에 유연한 개발을 할 수 있습니다.
* 하지만 리얼 월드에서는 의도적으로 RESTful 하지 않은 API 를 만드는 경우도 있습니다.
  * ex) OpenApi 의 경우 사용 편의성을 위해 의도적으로 RESTful 하지 않게 만듭니다.

{% embed url="http://haah.kr/2017/06/12/rest-the-big-lie/" %}

> 토스 결제 API 를 보면 [https://tossdev.github.io/api.html](https://tossdev.github.io/api.html)

* GET, POST 메서드만 활용합니다.
* 수 많은 에러응답 코드 중에 **400, 401, 403**만 사용합니다.

{% embed url="https://youtu.be/E4_0WWqmF3M" %}

> 카카오페이 결제 API 에도 비슷한 것이 있습니다. [https://tech.kakaopay.com/post/msa-transaction/](https://tech.kakaopay.com/post/msa-transaction/)

![](<../.gitbook/assets/image (10) (2).png>)

#### 그럼에도 불구하고 공부 해야합니다.

* 가장 기초적이고 보편적인 API 설계 방법이기 때문입니다.

{% embed url="http://www.yes24.com/Product/Goods/94462254" %}



### 예외처리는 어떻게 할까?

* try-catch 문의 catch 문을 의미있게 활용해주세요.
  * catch 문에 log 만 남기는 것은 적절한 활용이 아닙니다.
* CustomException 을 만들었다면 그것에 적합한 테스트를 만들어 주세요.
  * 적절한 테스트가 떠오르지 않는다면 어쩌면 무의미한 CustomException 일 수 있습니다.



### 커밋 메세지를 어떻게 써야할까?

{% embed url="https://udacity.github.io/git-styleguide/" %}

* **유다시티 커밋 가이드**에 따르면 type 을 나누고 suject, body, footer 를 작성하라고 합니다.
* 하지만 커밋의 목적을 생각해보면 **유지 보수 개발시 참고를 위한 트래킹** 때문이라고 생각합니다.
* intellij git blame plugin 으로 예를 들면
  * 커밋의 subject 만 보이며 body 까지 보려면 history 를 봐야되는 수고가 듭니다.
  * 생산성을 생각해볼 때 subject 만으로 이해가 가능한 커밋이 좋은 커밋이라고 생각합니다.

```
// issue 번호를 커밋 메시지 앞에 기록
#40 일반 유저 동적 쿼리 추가 

// jira issue 번호를 커밋 메시지 앞에 기록
PLATDEV-974 s3 다운로드 기능 구현 

// jira issue 번호 구분 + 중분류 구분을 기록
[PRECHARGE-270] 테스트 정상화 - yml 복구
[PRECHARGE-270] 사용 처리 global lock - 테스트 코드 개선
[PRECHARGE-377] 실시간 발행 api - web 구현

// type을 이모지로 표현
✨ MemberWIthDynamicUpdate 구현
```



### 클린 코드를 고민할수록 좋은 코드가 나옵니다.

#### local branch 에서는 정리되지 않은 커밋이 많아도 좋습니다.

* 오히려 다양한 시도를 해볼 수 있고 필요한 시점으로 돌아가기 쉽습니다.
* remote branch 에 올릴 때 squash, rebase 로 정리하면 됩니다.

#### 구조화는 점진적으로 하는 것을 추천합니다.

* 박재성님의 TDD 강의를 보면 최소한의 기능을 만들고 로직을 붙여 나갑니다.
* 절차지향적일지라도 일단 큰 로직을 만들고 메서드로 분리합니다.
  * intellij 의 리팩토링 기능은 충분히 강력합니다.
* 이런 과정으로 충분히 작아진 기능은
  * 이동시키기가 쉬워져 긴가민가한 경우를 직접 테스트 해볼 수 있습니다.
  * 나아가 함수형 프로그래밍 적용이 가능합니다.

#### 과한 구조화는 독이 될 수 있습니다.

* 구조화된 코드는 변경에 유연합니다.
  * 하지만 좋은 구조화를 위해서는 패턴과 네이밍의 깊은 고민이 필요합니다.
  * 그리고 아무리 좋은 구조라도 응집된 하나의 메서드보다 가독성이 좋기는 힘듭니다.
* 실무에서도 짧은 기간이나 팀 코딩 컨벤션에 따라 의도적으로 구조화하지 않는 경우도 있습니다.
* 즉 기간이 한정되어 있고 요구 사항 변경이 적은 프로젝트라면 선택과 집중이 필요할 수 있습니다.

{% embed url="https://overreacted.io/ko/goodbye-clean-code/" %}

#### 기본기 향상에 집중해주세요.

{% embed url="https://hyune-c.tistory.com/58" %}

#### 관련 서적을 읽어주세요.

{% embed url="http://www.yes24.com/Product/Goods/59626179" %}

{% embed url="http://www.yes24.com/Product/UsedShopHub/Hub/65551284" %}

* 사실 위 2권은 3년차 정도까지는 계속 읽어야될 정도로 깊이가 깊습니다.
* 입문으로는 **엘레강트 오브젝트**를 추천합니다.

{% embed url="http://www.yes24.com/Product/Goods/96193044" %}



### 통합 테스트에 집중 해주세요.

* 단위 테스트를 잘만들기 위해서는 구조화와 mock/stub 에 대한 학습이 필요합니다.
  * 하지만 이것은 굳이 지금 수준에 중요한 것이 아니라고 생각합니다.
* 그럼에도 불구하고 공부하고 싶다면 아래 책을 봐주세요.

{% embed url="http://www.yes24.com/Product/Goods/104084175" %}



### 문서 작업에 신경 써주세요.

#### 문서 작성에 있어서는 금융권 API 연동 문서를 보기를 추천합니다.&#x20;

어렵고 딱딱한 금융 API 연동을 쉽게 해주기 위해 토스 같은 회사들이 얼마나 노력하고 있나 보시면 좋습니다.\
어렵고 딱딱한 금융 세계에서 후발 주자가 기성 주자를 이기려면 더 친절하고 쉽고 가독성 좋게 만들어야겠죠? \
난해하고 힘들어 보자마자 나가게 만들어서는 안되겠죠?

여러분의 작업은 작게는 동료나 리뷰어, 나아가서는 면접관에게도 보이게 됩니다. \
그들이 여러분의 코드에 매력을 느끼도록 좀 더 친절하게 작성해주세요.

{% embed url="https://docs.tosspayments.com/reference" %}



### 리뷰 진행

#### 작성이 완료된 PR 에 리뷰어를 할당 or 코멘트로 알림 해주세요.  그리고 사전 노티 없이 커밋을 추가하거나 PR 을 종료하지 말아주세요.

이미 리뷰어가 지정된 후 내용이 변경되면 리뷰어는 **리뷰해도 되는건가?** 라는 판단을 할 수가 없습니다.\
그렇게 신뢰성이 떨어지면 PR 이 올라왔음에도 불구하고, **또 바뀌겟지** 라고 생각해 리뷰가 늦어지게 됩니다.

#### PR은 500줄 미만으로 리뷰를 원하는 부분을 코드에 핀포인트로 기록해주세요.

작성 의도가 명확할 때 좋은 리뷰가 나옵니다. \
좋은 질문을 하는 법과 같은 맥락입니다.

#### PR 리뷰 상태를 적절히 이용해주세요.

* Changes requested
  * 머지하기에 적합하지 않음.
  * 충분한 대화와 수정 후 재 리뷰 가 필요 합니다.
* Approved
  * 승인된 PR 은 리뷰어가 최종 확인 후 머지합니다.
* Merged
  * 머지된 PR 에서는 더 이상 conversation 을 진행하지 않습니다. (Closed 도 마찬가지)
  * conversation 이 필요하다면 별도의 채널로 질문해주세요.

#### 자주 사용되는 관용어구를 알아주세요.

* nit (nitpick)
  * 리뷰어들은 항상 더 나은 방법이 있을 수 있다는 의견을 자유롭게 남길 수 있어야 합니다.&#x20;
  * 그러나 별로 중요하지 않은 건이라면 코드 작성자가 선택할 수 있도록 넛지만 합니다.
* fyi (For your information)
  * 참고 바람

{% embed url="https://wnsgml972.github.io/devops/2020/05/17/CodeReview1/" %}
