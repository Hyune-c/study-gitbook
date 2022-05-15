# Spring Boot 버전별 변화

## 1.0 -> 2.0

1. Java 8 이 최소 사양, Java 9 공식 지원
2. Spring Framework 5
3. 써드파티 라이브러리 업그레이드
   * Tomcat 8.5
   * Flyway 5
   * Hibernate 5.2
   * Thymeleaf 3 - major
   * Elasticsearch 5.6
   * Gradle 4
   * Jetty 9.4
   * Mockito 2.x
4. Reactive Spring
   * Spring WebFlux
   * Reactive Spring Data
   * Reactive Spring Security
   * Embedded Netty Server
5. Functional APIs
6. Kotlin 지원
7. Gradle 플러그인
8. Actuator 변경점
   * 보안성 강화: 1.5 에서 기본으로 보여주던 endpoint 를 더이상 보여주지 않음
   * @Endpoints: 커스텀 endpoint 를 환경 (MVC, JMX, Jersey..) 에 상관 없이 편하게 구현
9. Spring Security
   * OAuth 2.0 통합
10. MySQL auto\_increment
    * Spring Data JPA, @GeneratedValue strategy 기본 동작 변경
    * GenerationType. AUTO
      * `Spring Boot 1.5` IDENTITY
      * `Spring Boot 2.0` TABLE
11. Database 커넥션 풀 관리 프레임워크 변경, Tomcat Pool -> HikariCP
12. JOOQ 지원
13. GIF 배너

## 2.0 -> 2.1

1. Java 11, Spring Framework 5.1
2. 써드파티 라이브러리 업그레이드
   * Tomcat 9
   * Undertow 2
   * Hibernate 5.3
   * JUnit 5.2
   * Micrometer 1.1
3. Actuator Endpoints
   * /actuator/caches
   * /actuator/health
4. JUnit5 지원 - 명시해줘야 됨
5. Bean Overriding: false

## 2.1 -> 2.2

1. Java 13, Spring Framework 5.2
2. 써드파티 라이브러리 업그레이드
   * Spring HATEOAS 1.0
   * Spring Kafka 2.3
   * Spring Security 5.2
   * Hamcrest 2.1
   * Mockito 3.1
   * AssertJ 3.12
   * Elasticsearch 6.7
   * Git Commit ID Plugin 3.0
   * Hazelcast 3.12
   * Jackson 2.10
   * Jedis 3.1
   * Lettuce 5.2
3. JUnit5 기본 지원

## 2.2 -> 2.3

1. Java 14, Gradle 6.3
2. 써드파티 라이브러리 업그레이드
   * Spring Data Neumann -> R2DBC 지원
   * Spring HATEOAS 1.1
   * Spring Integration 5.3
   * Spring Kafka 2.5
   * Spring Security 5.3
   * AssertJ 3.16, JUnit Jupiter 5.6, Mockito 3.3
   * Elasticsearch 7.6
   * Hibernate Validator 6.1
   * Jackson 2.11
   * QueryDSL 4.3
   * MongoDB 4.0
3. Docker 지원
4. Validation Starter 가 Web Starter 에서 제외
5. Graceful shutdown
6. Jackson 2.11

* 정확한 ISO-8601 확장 규격을 준수

## 2.3 -> 2.4

1. Java 15
2. JUnit Vintage Engine 제거

## 2.4 -> 2.5

1. Java 16, Gradle 7
2. 써드파티 라이브러리 업그레이드
   * Spring Data 2021.0
   * Spring HATEOAS 1.3
   * Spring Integration 5.5
   * Spring Kafka 2.7
   * Spring Retry 1.3
   * Spring Security 5.5
   * Spring Session 2021.0
   * Jackson 2.12
   * Mockito 3.7
   * JUnit Jupiter 5.7
   * Elasticsearch 7.12
3. Deprecations from Spring Boot 2.3, 2.4
   * 릴리즈 호환성 정책: deprecated 내용들은 최소 2개 minor release 동안 살아있음
4. HTTP/2 over TCP (h2c)
