# SpEL, Spring Expression Language

Expression Language 는 짧고 간단한 문법을 통해 필요한 데이터나 설정 값을 얻어올 수 있게 하는 특별한 형태의 표현식이다.\
SpEL은 그 중에서도 스프링 모든 영역에서 사용 가능한 언어 형식

* 주로 @Value("${config.value}") 와 같은 방식으로 설정 값을 주입 받는데 활용

## SpEL의 값 평가 (evaluation)

* SpelParser는 "" 안에 들어있는 문자열을 평가해서 (evaluation) 결과값을 만들어낸다.
* 'Hello World' 는 문자열 리터럴이 되며, concat 이라는 메서드도 호출할 수 있다.
* String 객체를 new 로 생성해서 사용도 가능

```java
ExpressionParser parser = new SpelExpressionParser();
Expression exp = parser.parseExpression("'Hello World'"); 
String message = (String) exp.getValue();  // "Hello World"

Expression expWow = parser.parseExpression("'Hello World'.concat('!')"); 
String messageWow = (String) expWow.getValue();  // "Hello World!"

Expression expString = 
	parser.parseExpression("new String('hello world').toUpperCase()"); 
String messageString = expString.getValue(String.class); // "HELLO WORLD"
```

## Bean의 Property를 설정할 때 사용하는 방식

* 기본적으로 #{ } 방식으로 property를 설정
* application.properties (또는 application.yml) 의 값을 가져올 때는 ${ } 방식으로 가져옴

```java
@Component
public class SimpleComponent {
	@Value("#{ 1+1 }")
	int two; // 2

	@Value("#{ 2 eq 2 }")
	boolean isTrue; // true

	@Value("${ server.hostname }")
	String hostName; // www.server.com

	@Value("#{ ${ server.hostname } eq 'www.server.com'}")
	boolean isHostSame; // true
}
```
