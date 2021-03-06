# Table of contents

* [Welcome](README.md)

## 실무 경험 & 팁

* [파일 조작하기](and/undefined.md)
* [Codesquad](and/codesquad/README.md)
  * [Code Reviewer](and/codesquad/reviewer/README.md)
    * [코드 리뷰를 진행하기에 앞서..](and/codesquad/22reviewer/before-proceeding-with-the-code-review.md)
    * [반찬 가게](and/codesquad/22reviewer/undefined/README.md)
      * [Service는 어떤 dto를 반환해야 할까?](and/codesquad/reviewer/service-dto.md)
        * [확장 질문](and/codesquad/22reviewer/undefined/service-dto/undefined.md)
    * [Airbnb](and/codesquad/22reviewer/airbnb.md)
    * [Issue Tracker](and/codesquad/22reviewer/issue-tracker.md)
      * [DB에서 TIMESTAMP와 DATETIME 타입의 차이](and/codesquad/22reviewer/issue-tracker/db-timestamp-datetime.md)
      * [한방 쿼리 vs 애플리케이션에서 조립](and/codesquad/22reviewer/issue-tracker/vs.md)
  * [Side Project](and/codesquad/side-project.md)
* [Database](and/database/README.md)
  * [INSERT INTO SELECT SHARED LOCK(row LOCK)](and/database/insert-into-select-shared-lock-row-lock.md)
* [HTTP Request 추적하기 with HAR File](and/http-request-with-har-file.md)

## Framework & Library

* [Spring](framework/spring/README.md)
  * [@Component vs @Configuration](framework/spring/component-vs-configuration.md)
* [JPA](framework-and-library/jpa/README.md)
  * [@GeneratedValue strategy](framework-and-library/spring/generatedvalue-strategy.md)
  * [Entity의 field type](framework-and-library/spring/entity-field-type.md)
* [Logback](framework-and-library/logback/README.md)
  * [기본 설정](framework-and-library/logback/undefined.md)
* [Monitoring](framework-and-library/monitoring/README.md)
  * [VisualVM](framework-and-library/monitoring/visualvm/README.md)
    * [설치](framework-and-library/monitoring/visualvm/undefined.md)
    * [문자열 생성으로 테스트](framework-and-library/monitoring/visualvm/undefined-1.md)
  * [nGrinder](framework-and-library/ngrinder.md)

## Database

* [MySQL](database/mysql/README.md)
  * [SQL 문 수행 절차](database/mysql/sql.md)
  * [트랜잭션과 잠금](database/mysql/undefined.md)
  * [인덱스](database/mysql/index.md)

## AWS

* [S3](aws/s3/README.md)
  * [용어](aws/s3/undefined.md)
  * [Amazon SDK 1.x with Spring](aws/s3/amazon-sdk-1.x-with-spring.md)
* [DynamoDB](aws/dynamodb.md)
  * [Get vs Query vs Scan](aws/dynamodb/get-vs-query-vs-scan.md)

## Computer science

* [OS](computer-science/os/README.md)
  * [Process vs Thread](computer-science/os/process-vs-thread.md)
  * [Process](computer-science/os/process.md)
* [Web](computer-science/web/README.md)
  * [HTTP](computer-science/web/http/README.md)
    * [HTTP vs HTTPS](computer-science/web/http-vs-https.md)
    * [HTTP 구성](computer-science/web/http.md)
    * [HTTP 그외](computer-science/web/http-1.md)
  * [REST API](computer-science/web/rest-api/README.md)
    * [GET 메서드에 payload를 사용해도 되는가?](computer-science/web/rest-api/get-payload.md)
    * [특정 목적의 API는 어떻게 만들어야 할까?](computer-science/web/rest-api/api.md)
  * [TCP / UDP](computer-science/web/tcp-vs-udp.md)
  * [인터넷의 작동 원리](computer-science/web/undefined.md)
  * [OAuth 2.0](computer-science/web/oauth-2.0.md)
* [Design Pattern](computer-science/design-pattern/README.md)
  * [Builder Pattern](computer-science/design-pattern/builder-pattern.md)
* [MSA](computer-science/msa.md)

## Language

* [Java](language/java/README.md)
  * [Copy](language/java/copy.md)
  * [메모리 관리](language/java/undefined.md)
  * [Garbage Collection](language/java/garbage-collection.md)
  * [자료구조](language/java/undefined-1.md)
  * [Java 17](language/java/java-17.md)

## Book & Online Class

* [한 번에 끝내는 Spring 완.전.판 초격차 패키지 Online](book-and-online-class/spring-complete-package/README.md)
  * [AOP, Aspect Oriented Programming](book-and-online-class/spring-complete-package/aop.md)
  * [Data Binding](book-and-online-class/spring-complete-package/data-binding.md)
  * [IoC(Inversion of Control), DI(Dependency Injection)](book-and-online-class/spring-complete-package/ioc-and-di.md)
  * [Null Safety](book-and-online-class/spring-complete-package/null-safety.md)
  * [Spring Resource](book-and-online-class/spring-complete-package/resource.md)
  * [Spring Boot 버전별 변화](book-and-online-class/spring-complete-package/spring-boot.md)
  * [SpEL, Spring Expression Language](book-and-online-class/spring-complete-package/spring-expression-language.md)
  * [Validation](book-and-online-class/spring-complete-package/validation.md)
* [이펙티브 자바 3판](book-and-online-class/effective-java/README.md)
  * [2장 객체 생성과 파괴](book-and-online-class/effective-java/2/README.md)
    * [아이템 1. 생성자 대신 정적 팩터리 메서드를 고려하라](book-and-online-class/effective-java/2/2.md)
    * [아이템 2. 생성자에 매개변수가 많다면 빌더를 고려하라](book-and-online-class/effective-java/2/2-1.md)
    * [아이템 3. private 생성자나 열거 타입으로 싱글턴임을 보증하라](book-and-online-class/effective-java/2/2-2.md)
    * [아이템 4. 인스턴스화를 막으려거든 private 생성자를 사용하라](book-and-online-class/effective-java/2/2-3.md)
    * [아이템 5. 자원을 직접 명시하지 말고 의존 객체 주입을 사용하라](book-and-online-class/effective-java/2/2-4.md)
    * [아이템 7. 다 쓴 객체 참조를 해제하라](book-and-online-class/effective-java/2/2-5.md)
  * [3장 모든 객체의 공통 메서드](book-and-online-class/effective-java/3/README.md)
    * [아이템 11. equals를 재정의하려거든 hashCode도 재정의하라](book-and-online-class/effective-java/3/3.md)
    * [아이템 12. toString을 항상 재정의하라](book-and-online-class/effective-java/3/3-1.md)
    * [아이템 14. Comparable을 구현할지 고려하라](book-and-online-class/effective-java/3/3-2.md)
  * [4장 클래스와 인터페이스](book-and-online-class/effective-java/4.md)

## Webinar

* [요즘 힙한 스타트업의 DBDB DEEP한 이야기](webinar/dbdb-deep.md)
