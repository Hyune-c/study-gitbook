# Entity의 field type

### ID

> The primary key, or the property or field of a composite primary key, must be one of the following Java language types:\
> \- Java primitive types\
> \- Java primitive wrapper type\
> \- sjava.lang.String\
> \- java.util.Date (the temporal type should be DATE)\
> \- java.sql.Date\
> \- java.math.BigDecimal\
> \- java.math.BigInteger\
> \
> \- Java Persistence API 공식 문서에서\
> [https://docs.oracle.com/javaee/6/tutorial/doc/bnbqa.html#bnbqf](https://docs.oracle.com/javaee/6/tutorial/doc/bnbqa.html#bnbqf)

* JPA 공식 문서를 보면 primitive types 도 허용하고 있습니다.

하지만

> We recommend that you declare consistently-named identifier attributes on persistent classes and that you use a nullable (i.e., non-primitive) type.\
> \
> [https://docs.jboss.org/hibernate/orm/5.3/userguide/html\_single/Hibernate\_User\_Guide.html#entity-pojo-identifier](https://docs.jboss.org/hibernate/orm/5.3/userguide/html\_single/Hibernate\_User\_Guide.html#entity-pojo-identifier)

* 일반적인 구현체인 Hibernate의 문서를 보면 명시적으로 non-primitive type의 사용을 권장하고 있습니다.
* id를 primitive type으로 하면 0과 null을 구분할 수 없습니다.
  * primitive type의 기본 값이 0이기 때문입니다.
* 그렇기 때문에 null이 허용되는 wrapper type을 활용해야 제대로 구분할 수 있습니다.

### Except ID

> 반면 **ID가 아닌 값**은 제 평소 사용에 대한 명백한 근거를 찾기 힘들었습니다.\
> 하지만 저와 비슷한 고민을 한 스택 오버 플로우의 질문을 찾았고 그것을 기반으로 제 생각을 좀 더 정리해보았습니다.

1. 데이터의 null 여부를 판단할 수 있어야 합니다.
2. null 데이터도 가져올 수 있어야 합니다.
   * 혹자는 null 데이터의 존재 자체를 문제로 말할 수 있지만, 경험상 실무 DB에는 null인 컬럼이 꽤 존재했습니다.
3. 소수 필드의 **boxing-unboxing**은 배제합니다.
   * **boxing-unboxing** 이슈는 반복문과 같이 사용될 때 발생한다고 생각합니다.
   * 컴퓨팅 능력이 충분히 저렴해지고 높아졌습니다.&#x20;
4. 코딩 스타일의 일관성을 가져갈 수 있습니다.
5. 일부 `@Ttransient` 필드에 대해서는 사용하기도 합니다.

위와 같은 이유로 저는 Entity의 모든 필드를 wrapper type으로 사용하는 걸 선호합니다.

{% embed url="https://stackoverflow.com/questions/2331630/entity-members-should-they-be-primitive-data-types-or-java-data-types" %}
