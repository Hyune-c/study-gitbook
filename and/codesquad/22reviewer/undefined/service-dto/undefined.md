# 확장 질문

### 이전 리뷰 내용

> &#x20;service 레이어에서 특정 response(컨트롤러 레이어의 DTO) 를 만들어 반환하지 않고, 범용 DTO를 만들어 반환하게 되면, controller 레이어에서 이 범용DTO 를 가공하여 제공하는 곳에 알맞은 형태의 response 를 가공해서 넘겨줄 수 있다.즉 service 레이어 메서드를 건드릴 일이 없고, 재사용성이 증가한다.

### 질문 & 추가 리뷰

#### 지난 번 리뷰에서 말씀 해주셨던 내용이 좋다고 생각 했었고, 이번 프로젝트에 적용 해보았는데요. 진행하며 궁금증이 생겨서 dm 드립니다. 범용DTO 라는 특성상 나중에 어떻게 만들어 질지 모르는 response에 대응하기 위해선 범용DTO 안에 로직을 넣어선 안될 것 같았습니다.

* <mark style="color:purple;">네. dto 레이어간의 데이터 이동을 목적으로 하기에 로직이 없는 것이 보통입니다.</mark>

> The difference between data transfer objects and [business objects](https://en.wikipedia.org/wiki/Business\_object) or [data access objects](https://en.wikipedia.org/wiki/Data\_access\_object) is that a DTO does not have any behavior except for storage, retrieval, serialization and deserialization of its own data ([mutators](https://en.wikipedia.org/wiki/Mutator\_method), [accessors](https://en.wikipedia.org/wiki/Method\_\(computer\_programming\)), [parsers](https://en.wikipedia.org/wiki/Parsing) and [serializers](https://en.wikipedia.org/wiki/Serialization)).

{% embed url="https://en.wikipedia.org/wiki/Data_transfer_object" %}

#### 이런 생각을 하고 코드를 짜고 보니 결국 범용DTO 는 DB에 쿼리를 날려 얻은 Entity와 완벽히 동일한, 1:1 구조로 나오게 되더라구요.

> 이것에 대해서는 이야기할 것이 꽤 많습니다. 지금에 맞는 것을 선별적으로 가져가시기를 권장합니다.

* <mark style="color:purple;">필요성을 느끼지 못한다면 dto를 만들지 않는 것도 방법입니다.</mark>&#x20;
  * <mark style="color:purple;">dto를 만드는 행위 자체도 성능과 유지보수 비용이 들기 때문입니다.</mark>

{% embed url="https://martinfowler.com/bliki/LocalDTO.html" %}

* 하지만&#x20;

#### 이러면 service 레이어에서 repository를 호출해 Entity를 얻고, 이 Entity를 그대로 반환하는 것과 어떠한 차이가 있을까? 의문이 들어서 질문 드리고 싶습니다.

* <mark style="color:purple;">entity를 service 레이어의 반환형으로 사용하는 것은 기능상 가능하지만 꽤 어색합니다.</mark> \ <mark style="color:purple;">osiv를 공부해보시면 좋을 것 같습니다.</mark>
* <mark style="color:purple;">레이어를 건너 뛰어버린다는 점에서는 일반적이지는 않습니다.</mark>[<mark style="color:purple;">https://youtu.be/RVO02Z1dLF8?list=PL1DJtS1Hv1PiGXmgruP1\_gM2TSvQiOsFL\&t=508</mark>](https://youtu.be/RVO02Z1dLF8?list=PL1DJtS1Hv1PiGXmgruP1\_gM2TSvQiOsFL\&t=508)<mark style="color:purple;"></mark>

