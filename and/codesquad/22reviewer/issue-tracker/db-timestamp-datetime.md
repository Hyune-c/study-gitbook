# DB에서 TIMESTAMP와 DATETIME 타입의 차이

{% hint style="info" %}
`TIMESTAMP`는 TIMEZONE을 포함하고, `DATETIME`은 그렇지 않은 차이가 있습니다.\
이것은 국제화와 연관되며 크게 두 가지의 해결 방법이 있습니다.
{% endhint %}

```java
@Column(columnDefinition = "TIMESTAMP")
private LocalDateTime createdAt;
```

#### `TIMESTAMP`를 유지하며 하나의 DB에서 복수 개의 리전 데이터를 관리한다.

* 전체 데이터 조회가 간편합니다.
* 하지만 업무 성격상 크로스 리전의 니즈가 적다면 비효율적입니다.

#### `DATETIME`을 유지하며 리전별로 DB를 분리한다.

* 업무의 분리 단위가 리전인 경우 적합합니다.
* 전체 데이터를 통합하는 경우 비용이 커지지만, 보통의 경우 통합 작업은 자주 일어나지 않기에 비용은 상대적으로 고려사항이 아닙니다.

{% embed url="https://devdojo.com/bobbyiliev/what-is-the-difference-between-datetime-and-timestamp-data-type-in-mysql" %}
