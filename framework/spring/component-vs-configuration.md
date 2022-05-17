# @Component vs @Configuration

#### **@Bean @Configuration**

* 수동으로 스프링 컨테이너에 빈을 등록하는 방법
* 개발자가 직접 제어가 불가능한 라이브러리를 빈으로 등록할 때 불가피하게 사용
* 유지보수성을 높이기 위해 애플리케이션 전범위적으로 사용되는 클래스나 다형성을 활용하여 여러 구현체를 빈으로 등록 할 때 사용
* 1개 이상의 @Bean을 제공하는 클래스의 경우 반드시 @Configuration을 명시해 주어야 싱글톤이 보장됨

#### **@Component**

* 자동으로 스프링 컨테이너에 빈을 등록하는 방법
* 스프링의 컴포넌트 스캔 기능이 @Component 어노테이션이 있는 클래스를 자동으로 찾아서 빈으로 등록함
* 대부분의 경우 @Component를 이용한 자동 등록 방식을 사용하는 것이 좋음
* @Component 하위 어노테이션으로 @Configuration, @Controller, @Service, @Repository 등이 있음



### @Configuration 안에 @Bean을 사용해야 하는 이유

* @Configuration가 선언된 클래스 안의 Bean은 스프링 컨테이너에서 관리됩니다.
* 즉 CGLib으로 프록시 패턴을 적용되며 싱글톤을 보장합니다.

```java
// @Configuration이 있다면 
Test.sample.AppConfig$$EnhancerBySpringCGLIB$$780402cc@6179e425

// @Configuration이 없다면 
Test.sample.AppConfig@2796aeae
```



{% embed url="https://castleone.tistory.com/2" %}

{% embed url="https://mangkyu.tistory.com/75" %}
