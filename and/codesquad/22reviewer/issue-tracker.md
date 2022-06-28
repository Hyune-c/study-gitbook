# Issue Tracker

### 현재는 access token(JWT)만 내려주고 있지만, 추후에는 refresh token도 추가해 볼 생각입니다. 두 토큰이 똑같이 `authId`와 `expired_time`만을 갖게 하려고 했는데, access token과 refresh token과 차이를 나게하는 부분이 `expired_time`만 있게 해도 되는지 잘 모르겠습니다. (둘을 구분할 수 있는 속성이 더 있어야 하는지?)

![](<../../../.gitbook/assets/image (5).png>)

* 보통 **claims**를 활용합니다. **registerd claims**를 활용한 예시를 첨부합니다.

### `TimeZone.setDefault(TimeZone.getTimeZone("GMT"));` 에 대한 리뷰

> For most purposes, UTC is considered interchangeable with Greenwich Mean Time (GMT), but GMT is no longer precisely defined by the scientific community.

* **UTC** 명시를 권장합니다.

{% embed url="https://www.baeldung.com/java-time-zones" %}

### DB에서 `TIMESTAMP`와 `DATETIME` 타입의 차이

```java
@Column(columnDefinition = "TIMESTAMP")
private LocalDateTime createdAt;
```

> `TIMESTAMP`는 TIMEZONE을 포함하고, `DATETIME`은 그렇지 않은 차이가 있습니다.\
> 이것은 국제화와 연관되며 크게 두 가지의 해결방법이 있습니다.

#### `TIMESTAMP`를 유지하며 하나의 DB에서 복수 개의 리전 데이터를 관리한다.

* 전체 데이터 조회가 간편합니다.
* 하지만 업무 성격상 크로스 리전의 니즈가 적다면 비효율적입니다.

#### `DATETIME`을 유지하며 리전별로 DB를 분리한다.

* 업무의 분리 단위가 리전인 경우 적합합니다.
* 전체 데이터를 통합하는 경우 비용이 커지지만, 보통의 경우 통합 작업은 자주 일어나지 않기에 비용은 상대적으로 고려사항이 아닙니다.

### 한방 쿼리 vs 다수의 쿼리 조회 후 애플리케이션에서 조립

> 이것

> 한방 쿼리

#### 장

* 가장 비용이 큰 요청 중 하나인 DB I/O를 절약할 수 있습니다.
* native SQL에 익숙한 사람이라면 가독성이 더 좋습니다.
  * 직관적인 쿼리 튜닝이 가능합니다. with DBA
* SQL만으로 업무 흐름을 파악할 수 있습니다.

#### 단점

* 유지보수가 될 수록 쿼리의 복잡도가 늘어나 영향도 분석이 쉽지 않습니다.
* 거대한 쿼리는 DB 부하를 초래합니다.&#x20;
* 업무 로직이 영속성 레이어로 전파될 가능성이 높습니다.

> 애플리케이션에서 조립

#### 장점

* 충분히 작은 단위의 조회 후 projection을 하기에 재사용이(작은 단위의 조회를) 가능합니다.
* ORM의 장점을 활용할 수 있습니다.

#### 단점

* 가장 비용이 큰 요청 중 하나인 DB I/O가 추가 발생합니다.
