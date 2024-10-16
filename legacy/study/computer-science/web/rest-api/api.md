# 특정 목적의 API는 어떻게 만들어야 할까?

> REST API의 장점은 리소스 기반의 설계로 **범용성을 높이는 것**에 있다고 생각합니다.
>
> 그리고 사용자에게 보이는 표현 로직은 프론트에게 위임함으로서 느슨한 결합을 유도합니다.

* `/rooms/{room_id}`
  * 일반적인 API 설계로 리소스를 복수형으로 표현됩니다.&#x20;
  * 필요에 따라 queryParam을 추가합니다.

### A. 특정 가격 범위에 속하는 숙소의 개수 분포를 알고 싶습니다.

1. `/rooms?price_from=1000&price_to=5000`
   * 특정 가격 범위의 모든 숙소를 가져올 수 있습니다.
   * 가장 자유도가 높지만 분포를 위해서는 숫자만 필요 합니다.
     * 즉 니즈에 불필요한 정보도 반환되는 단점이 있습니다.
   * 프론트에서 2차 가공을 통해 니즈에 맞는 **{가격 범위:개수}**의 목록을 만들 수 있습니다.
2. `/rooms/price?price_from=1000&price_to=5000`
   * 리소스 대상을 rooms의 price로 한정합니다.
   * 프론트의 2차 가공이 들어가는 것은 동일하지만, price 정보만 반환되기에 데이터 양이 적습니다.

### B. 10의 자리를 절삭하고 싶은 니즈가 생겼습니다.

> 앞의 API에 queryParam을 추가하는 것은 이상합니다.
>
> queryParam은 조회 조건으로 사용되는데, 절삭은 조회 결과의 조작이기 때문입니다.

1. `/room_price_distribution`
   * 가장 쉽게 구현할 수 있는 형태로 해당 니즈를 만족하는 특화 API 입니다.
2. `/room_price_distribution?distribution_unit=10`
   * 절삭 단위에 대한 queryParam 추가로 유연함을 추가합니다.
     * 사용자의 요청은 `distribution_unit`을 지정하고
     * 어드민은 `distribution_unit`을 지정하지 않을 수 있습니다.

### 조금 더 생각해봅시다.

> A는 리소스 기반의 설계를 했고, B는 목적 기반의 설계를 했습니다.
>
> 즉 쓰이는 용도가 다르기에 설계 의도도 다른 것 입니다.

* A의 설계는
  * 설계에 대한 지식이 필요하며 비교적 개발이 어렵습니다.
  * 니즈가 바뀌어도 수정 영향도가 적습니다.
  * openApi, MSA 기반에서 적절하며 표현 로직을 가지지 않습니다.
* B의 설계는
  * 명확한 니즈에 특화된 개발로 비교적 개발이 쉽습니다.
  * 단기 생산성이 중요한 스타트업이나, 니즈 변경이 적은 내부용으로 적절합니다.



> 표현 로직을 프론트에게 위임하는 A의 설계는 높은 자유도로 변경에 강합니다.
>
> 하지만 이런 위임은 프론트엔드에 로직이 존재하게 하고, 높은 자유도는 로직의 파편화를 초래합니다.

![https://www.kennethlange.com/backends-for-frontends-pattern/](<../../../../../.gitbook/assets/image (16) (1) (1).png>)

* 가장 잘 알려진 방법은 BFF(Backend for Frontend) 입니다.
* BFF는 각 마이크로 서비스에서 리소스를 가져온 후 니즈에 맞게 가공하는, 매핑 역할을 합니다.
  * 표현 레이어를 위한 로직과 핵심 도메인 로직을 분리합니다.
* 하지만 마이크로 서비스와의 통신에서 의도한 것보다 큰 비용이 발생하는 부작용도 있습니다.
  * 물론 저 비용을 최소화하기 위해 gRPC, Private VPC 등을 구성합니다.
* 앞의 니즈를 예시로 들면
  * &#x20;Web BFF에서는 각 도메인에서 room 정보를 가져오고&#x20;
  * 그 중에서 price만  발라낸 후 10단위의 절삭을 합니다.

![https://techblog.woowahan.com/2667/](<../../../../../.gitbook/assets/image (12).png>)

* 마이크로 서비스와의 통신을 줄이기 위해 캐시를 적극적으로 사용하는 방법도 있습니다.
  * 각 BFF에서 표현 레이어에 특화된 캐시에 직접 붙는 방법입니다.
  * 서비스 간의 통신 비용이 줄어들지만, 느슨한 정보 동기화와 운영의 복잡함이 생깁니다.
