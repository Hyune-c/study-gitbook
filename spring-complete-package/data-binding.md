# Data Binding

사용자나 외부 서버의 요청 데이터를 특정 도메인 객체에 저장해서 Request 에 담아주는 것을 뜻한다.

## Converter\<S, T> Interface

```java
package org.springframework.core.convert.converter;

public interface Converter<S, T> {

    T convert(S source);
}
```

S(Source) 타입을 받아 T(Target) 타입으로 변환해주는 Interface

* 활용 방법

```java
// 요청
GET /user-info
x-auth-user : {"id":123, "name":"Paul"}

// 유저 객체
public class XAuthUser {
    private int id;
    private String name;

    // the usual getters and setters...
}

@GetMapping("/user-info")
public UserInfoResponse getUserInfo(
	@RequestHeader("x-auth-user") XAuthUser xAuthUser){

	// get User Info logic here...
}
```

```java
@Component
public class XAuthUserConverter implements Converter<String, XAuthUser> {
	@Override
	public XAuthUser convert(String source) {
		return objectMapper.readValue(source, XAuthUser.class);
	}
}
```

헤더에 담긴 json 형식 문자열을 XAuthUser에 바로 담고 싶은 경우 Converter 를 Bean 으로 등록할 수 있다..

이와 비슷하게 PathParameter 나 기타 특수한 경우의 데이터를 특정 객체에 담고 싶은 경우

* Converter 를 만들어서 Spring 에 Bean 으로 등록
* 스프링 내에 ConversionService 라는 내장된 서비스에서 Converter 구현체 Bean 들을 Converter 리스트에 등록
* 외부데이터가 들어오고, Source Class Type → Target Class Type 이 Converter 에 등록된 형식과 일치하면 해당 Converter 가 동작하는 원리

## Formatter

특정 객체 ↔ String 간의 변환을 담당

* Date ↔ String 간의 변환을 수행하는 Formatter

```java
package org.springframework.format.datetime;

public final class DateFormatter implements Formatter<Date> {
    public String print(Date date, Locale locale) {
        return getDateFormat(locale).format(date);
    }

    public Date parse(String formatted, Locale locale) throws ParseException {
        return getDateFormat(locale).parse(formatted);
    }
		// getDateFormat 등 일부 구현은 핵심에 집중하기 위해 생략... 
}
```

* `print` API 요청에 대한 응답을 줄 때, Date 형식으로 된 데이터를 특정 locale 에 맞춘 String 으로 변환
* `parse` API 요청을 받아올 때, String 으로 된 "2021-01-01 13:15:00" 같은 날짜 형식의 데이터를 Date 로 변환하도록 함

Formatter 도 Converter 와 마찬가지로 Spring Bean 으로 등록하면 자동으로 ConversionService 에 등록시켜주기 때문에 필요에 따라 자동으로 동작하게 된다. (요청/응답 시 해당 데이터 타입이 있는 경우)
