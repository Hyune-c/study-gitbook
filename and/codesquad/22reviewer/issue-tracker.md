# Issue Tracker

### 현재는 access token(JWT)만 내려주고 있지만, 추후에는 refresh token도 추가해 볼 생각입니다. 두 토큰이 똑같이 `authId`와 `expired_time`만을 갖게 하려고 했는데, access token과 refresh token과 차이를 나게하는 부분이 `expired_time`만 있게 해도 되는지 잘 모르겠습니다. (둘을 구분할 수 있는 속성이 더 있어야 하는지?)

![](<../../../.gitbook/assets/image (5).png>)

* 보통 **claims**를 활용합니다. **registerd claims**를 활용한 예시를 첨부합니다.

### `TimeZone.setDefault(TimeZone.getTimeZone("GMT"));` 에 대한 리뷰

> For most purposes, UTC is considered interchangeable with Greenwich Mean Time (GMT), but GMT is no longer precisely defined by the scientific community.

* **UTC** 명시를 권장합니다.

{% embed url="https://www.baeldung.com/java-time-zones" %}

### DB에서 `TIMESTAMP`와 `DATETIME` 타입의 차이

{% content-ref url="issue-tracker/db-timestamp-datetime.md" %}
[db-timestamp-datetime.md](issue-tracker/db-timestamp-datetime.md)
{% endcontent-ref %}

### 한방 쿼리 vs 다수의 쿼리 조회 후 애플리케이션에서 조립

{% content-ref url="issue-tracker/vs.md" %}
[vs.md](issue-tracker/vs.md)
{% endcontent-ref %}
