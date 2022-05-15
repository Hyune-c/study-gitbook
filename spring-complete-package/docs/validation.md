# Validation

주로 사용자 또는 서버의 요청 (http request) 내용을 확인하는 단계

## Validation의 종류

### 데이터 검증

* 필수 데이터의 존재 유무
* 문자열의 길이나 데이터 값의 범위
* email, 신용카드 번호 등 특정 형식에 맞춘 데이터

### 비즈니스 검증

* 서비스 정책에 따라 데이터를 검증
* 예) 배달앱인 경우 배달 요청을 할 때 해당 주문 건이 결제 완료 상태인지 확인
* 경우에 따라 외부 API 를 호출하거나 DB 를 조회하여 검증하는 경우도 존재

## Spring Validation

### Java Bean Validation

```java
public class MemberCreationRequest {
		@NotBlank(message="이름을 입력해주세요.")
		@Size(max=64, message="이름의 최대 길이는 64자 입니다.")
    private String name;
		@Min(0, "나이는 0보다 커야 합니다.")
    private int age;
		@Email("이메일 형식이 잘못되었습니다.")
    private int email;

    // the usual getters and setters...
}
```

* 요청 dto 에 어노테이션으로 명시 후 @RequestBody 에 @Valid 어노테이션을 달게 되면, Java Bean Validation 이 수행되고 문제가 없을 때만 메서드 내부로 진입 된다.
* 검증 중 실패가 발생하면 MethodArgumentNotValidException 발생

```java
@PostMapping(value = "/member")
public MemeberCreationResponse createMember(
	@Valid @RequestBody final MemeberCreationRequest memeberCreationRequest) {
	// member creation logics here...
}
```

### Spring Validator Interface

```java
public class Person {

    private String name;
    private int age;

    // the usual getters and setters...
}
```

```java
public class PersonValidator implements Validator {

    /**
     * This Validator validates only Person instances
     */
    public boolean supports(Class clazz) {
        return Person.class.equals(clazz);
    }

    public void validate(Object obj, Errors e) {
        ValidationUtils.rejectIfEmpty(e, "name", "name.empty");
        Person p = (Person) obj;
        if (p.getAge() < 0) {
            e.rejectValue("age", "negativevalue");
        } else if (p.getAge() > 110) {
            e.rejectValue("age", "too.darn.old");
        }
    }
}
```

Person이라는 javaBean 객체가 있을 때, Validator 를 구현한 PersonValidator 를 통해 검증한다.

* `supports` validator 가 동작할 조건을 정의. 주로 class의 타입을 비교
* `validate` 검증을 진행

### 실무 활용

1. 요청 dto 에서 Java Bean Validation 으로 1차 검증
2. 로직 초기에 비즈니스 검증 후 Custom Exception 처리(ErrorCode, ErrorMessage)

* Spring validator 장단점
  * 장점: Java Bean Validation 에 비해 조금 더 복잡한 검증이 가능
  * 단점
    * Validation 을 수행하는 코드를 찾기가 어렵다. (상대적으로)
    * 비즈니스 검증 로직의 파편화 위험.
