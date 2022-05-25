# Entity의 field type

### ID

> We recommend that you declare consistently-named identifier attributes on persistent classes and that you use a nullable (i.e., non-primitive) type.\
> \
> [https://docs.jboss.org/hibernate/orm/5.3/userguide/html\_single/Hibernate\_User\_Guide.html#entity-pojo-identifier](https://docs.jboss.org/hibernate/orm/5.3/userguide/html\_single/Hibernate\_User\_Guide.html#entity-pojo-identifier)

* id를 primitive type으로 하면 id가 0인지, null인지 구분하기 힘듭니다.
  * primitive type의 기본 값은 0이기에 0과 null을 구분할 수 없습니다.
* 그렇기 때문에 null이 가능한 wrapper type을 활용해야 합니다.

### Except ID

> 반면 ID가 아닌 값에 대해서는 뚜렷한 가이드가 없습니다.\
> 때문에 스택 오버 플로우에서 제 의견과 비슷한 것을 차용하여 작성합니다.

저는 entity 클래스에는 모두 wrapper type을 사용합니다.

1. 데이터의 null 여부를 판단할 수 있어야 합니다.
2. null인 데이터도 가져올 수 있어야 합니다.
   1. 혹자는 null인 컬럼이 존재하는게 이상하다고 말할 수 있지만, 제가 일해본 legacy db에는 null인 컬럼이 많았습니다.
3. 소수 필드의 **boxing-unboxing**은 문제가 되지 않습니다.
   1. 컴퓨팅 능력이 발달되었고, **boxing-unboxing** 이슈는 반복문과 같이 발생한다고 생각합니다.
4. 코딩 스타일의 일관성을 가져갈 수 있습니다.
5. 일부 `@Ttransient` 필드에 대해서는 사용하여도 된다고 생각합니다.

{% embed url="https://stackoverflow.com/questions/2331630/entity-members-should-they-be-primitive-data-types-or-java-data-types" %}
