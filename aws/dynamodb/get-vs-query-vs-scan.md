# Get vs Query vs Scan

#### Get

* 단일 조회

#### Query&#x20;

* 추천하는 사용 방식!
* 특정 파티션 키가 (인덱스) 있는 항목 조회
  * 즉 한정적인 조건만 설정 가능하다.
* query 후 키를 정렬하고 데이터의 하위 집합만 가져오도록 조건을 적용할 수 있습니다.
  * subquery 같은 것인듯?

#### Scan

* 가장 풍부한 조건 설정이 가능합니다.
  * 하지만 모든 데이터를 로드시킨 후 함으로 리소스 부담이 큽니다.
  * DynamoDB는 데이터 로드량에 따라 비용이 청구됩니다.
  * 따라서 충분히 작은 테이블에 대해서 정밀한 조건의 조회가 필요할 때만 써야됩니다.

> 셋째, 스캔을 수행하는 워크로드는 순식간에 엄청난 비용이 들 수 있다. \
> 이는 read capacity unit 이 실제로 읽은 바이트 수를 고려하기 때문

{% embed url="https://sujl95.tistory.com/84" %}

#### Query 심화

* rdb에서 통용되는 like 검색이 되지 않습니다.
  * 하지만 between 절이나 `%` 가 뒤에 붙는 형태는 `begins_with` 절이 지원됩니다.

{% embed url="https://docs.aws.amazon.com/ko_kr/amazondynamodb/latest/developerguide/Query.html" %}

#### 공통

* query와 scan은 최대 1메가까지만 조회됩니다.

> 스캔한 항목의 총 개수가 최대 데이터 세트 크기 제한인 1MB를 초과하면 스캔이 중지되고 결과는 LastEvaluatedKey 후속 작업에서 스캔을 계속할 수 있는 값으로 사용자에게 반환됩니다. \
> 결과에는 한도를 초과하는 항목 수도 포함됩니다. \
> 검색 결과 필터 기준을 충족하는 테이블 데이터가 없을 수 있습니다.

* 전체 개수를 구하는 것은 scan 조회가 필요하기에 권장하지 않습니다.

{% embed url="https://stackoverflow.com/questions/27316643/how-to-get-item-count-from-dynamodb" %}

* 페이지네이션
  * `LastEvaluatedKey`를 통해 커서 기반 페이지네이션으로 구현합니다.

{% embed url="https://docs.aws.amazon.com/ko_kr/amazondynamodb/latest/developerguide/Query.Pagination.html" %}
