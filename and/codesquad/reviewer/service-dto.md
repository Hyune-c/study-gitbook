# Service는 어떤 dto를 반환해야 할까?

## 리뷰 대상 코드

```java
public Slice<DishListResponse> findDishesByCategory(String categoryName, Criteria criteria) {
        List<Dish> dishes = dishRepository.findByCategoryName(
            categoryName, criteria.getLimit(), criteria.getOffset());

        List<DishListResponse> responses = dishes.stream()
            .map(DishListResponse::from)
            .collect(Collectors.toList());
        return new Slice<>(responses, criteria);
    }
```

* 33조의 코드를 보면 service에서 조회 메서드를 통해 dto를 반환합니다.
* 그런데 response라는 네이밍에서 유추할 수 있듯이 외부로 바로 반환되는 dto입니다.

## 장점

* 해당 화면/기능만을 로직이 완전히 분할되어 개발이 편하고 변경에 강합니다.
* 개발이 편하다는 것이 별 것 아니라고 생각할 수 있습니다.
  * 하지만 간결성이나 익숙한 패턴의 사용, 일관성 있는 코딩은 생산성에 지대한 영향을 줍니다.

## 단점

* 기능이 특화되는 만큼 재사용성이 떨어집니다.

### 예시

* 33팀은 공통 플랫폼/OpenApi을 만드는 팀입니다.
*   DishListResponse는 아래와 같은 필드를 가지고 있습니다.

    ```java
    private final String title;
    private final String description;
    private final Integer fixedPrice;
    private final Integer discountPrice;
    ```
* AAA 사이트에서는 해당 API로 잘 쓰고 있었습니다.
* 그런데 어느날 신설된 BBB 사이트에서는 영문 title 반환이 필요해졌습니다.
  * response이 형태가 달라진 것입니다.
  * 단순히 engTitle만 추가하면 된다고 생각할 수 있지만, BBB 사이트를 위해 수정한 response는 AAA 사이트에도 노출된다는 것이 문제입니다.
  * 즉 의도하지 않은 사이드 이펙트가 생김으로 인해 재사용성이 떨어집니다.
* 만약 지금의 구조에서 AAA 사이트에 영향을 주지 않으면서 BBB 사이트의 니즈를 만족하려면, BBB 사이트를 위한 response를 반환하는 메서드를 새로 만들어야 합니다.
  * 이미 만들어진 response를 transform하는 것은 추천하지 않습니다.

## 어떻게 해야되냐?

### CQRS 모델을 고려하신 것이라면 지금도 나쁘지는 않습니다.

* 실제로 해당 기능이 특화된 경우 지금의 구조도 좋습니다.
  * 리소스 기반이 아닌 니즈 기반의 API 설계가 필요한 경우가 있습니다.
    * 대표적으로는 사내 어드민에 그리드 형태의 화면을 만들 때 입니다.
    * 이 경우 다수의 테이블을 조인하고 response를 projection하는 형태로 설계하여 repository 레벨에서부터 response를 반환할 수도 있습니다.
  * 하지만 이것이 의도한 것이라면 **좀 더 특화된 네이밍과 클래스 분리**를 하는 것이 좋습니다.

### 재사용을 고려한다면

* 좀 더 리소스를 기반으로 사용하기 위한 고민이 필요합니다.
* 한가지 예로는 **service에서는 범용 dto를 반환하고 controller에서 api에 맞는 특화 response를 만들 수** 있습니다.
* 즉 레이어별로 input, output dto를 만들면 결합도가 낮아져 재사용성은 높아집니다.

### 하지만

* 사이드 프로젝트와 같이 기간이 한정되고 큰 요구사항의 변화가 없는 경우 재사용만을 고려하는 것은 과할 수 있습니다.
  * 네이밍의 고민과 페어에게 로직을 설명해야되는 수고가 생깁니다.
* 실무에서도 마찬가지이기에 **생산성과 재사용/변경의 사이에서 트레이드 오프** 하셔야됩니다.
  * 저도 실무에서는 확장성이 거의 예상되지 않는 업무는 의도적으로 구조화하지 않기도 합니다.

## 기타 참고 사항

* CQRS 패턴
* BFF (백엔드 포 프론트)
* 언제 올지 모르는 너무 먼 미래보다는 지금의 요건에 충실하게 만들자.

{% content-ref url="../22reviewer/undefined/service-dto/undefined.md" %}
[undefined.md](../22reviewer/undefined/service-dto/undefined.md)
{% endcontent-ref %}
