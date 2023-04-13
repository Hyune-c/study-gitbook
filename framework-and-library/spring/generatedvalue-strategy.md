# @GeneratedValue strategy

> entity identifier를 생성하는 전략을 선택합니다.

### GenerationType.AUTO

* 식별자 생성시 JPA 구현체의 기본 전략을 따릅니다.
* Spring Boot 2.x의 JPA 구현체인 Hibernate 5.0 기준
  * MySQL은 **GenerationType.TABLE** 전략이 선택됩니다.

### GenerationType.IDENTITY&#x20;

* 식별자 생성을 DBMS에 위임합니다.
  * AutoIncrement를 지원하는 **MySQL**, PostgreSQL, SQL Server, DB2에서 사용됩니다.

### GenerationType.SEQUENCE&#x20;

* 식별자 생성시 DB Sequence를 사용합니다.
  * Sequence를 지원하는 DBMS인 **Oracle**, PostgreSQL, DB2, H2 DB에서 사용됩니다.

### GenerationType.TABLE

* 식별자 생성시 별도의 테이블을 사용합니다.
* DB Sequence를 흉내낸 방식으로 별도의 table을 활용하기에 추가적인 DB 커넥션이 발생합니다.
  * 나아가 부정합을 일으킬 수 있어 일반적으로 사용되지 않습니다.

{% embed url="https://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html#identifiers-generators" %}

{% embed url="https://lion-king.tistory.com/entry/JPA-JPA-Id-GenerationTypeAUTO-IDENTITY" %}

{% embed url="https://ngdeveloper.com/generationtype-identity-vs-generationtype-sequence-vs-generationtype-auto/" %}

{% embed url="https://vladmihalcea.com/why-you-should-never-use-the-table-identifier-generator-with-jpa-and-hibernate/" %}

### SpringBoot 1.5.x와 2.0.x의 차이

> 식별자 생성 전략이 **GenerationType.IDENTITY**에서 **GenerationType.TABLE**으로 변경되었습니다.\
> 메이저 버전 업그레이드가 필요한 환경에서는 경험할 수 있었겠지만, 제가 일하는 환경은 이미 다 2.5.x 였기 때문에 지식으로만 알고 있습니다.

* Spring Boot 2.x의 JPA 구현체인 Hibernate 5.0 기준, MySQL은 **GenerationType.TABLE** 전략이 선택됩니다.
* Hibernate의 ID 생성 전략을 따라 갈지 말지 결정하는 **useNewIdGeneratorMappings 프로퍼티가 1.5.x 버전의 false에서 2.0.x 에는 true로 변경**되었습니다.
* 즉 식별자 생성 전략이 JPA 구현체에 종속적이게 설정이 바뀌면서 **GenerationType.TABLE**이 선택 됩니다.

{% embed url="https://jojoldu.tistory.com/295" %}
