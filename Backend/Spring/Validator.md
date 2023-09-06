# Validator

### 비즈니스 로직 안에서 직접 검증 로직을 모두 넣어놓는 다면 코드가 방대해진다. 고로 Validator를 사용해서 검증기를 별도로 분리해서 사용할 수 있게 지원하는 인터페이스이다.

```java
public interface Validator {
    boolean supports(Class<?> clazz); 특정 객체에 대한 검증을 지원하는 여부
    void validate(Object target, Errors errors); 검증할 객체와 BindingResult 혹은 에러들.
}

@InitBinder
  public void init(WebDataBinder dataBinder) {
       log.info("init binder {}", dataBinder);
       dataBinder.addValidators(itemValidator);
  }

이렇게 등록하고
@Validated 를 @ModelAttribute Item item
검증할 객체 앞에 선언하게되면 특정 객체에 대해 등록한 검증기 로직을 먼저 실행하고 그 이후 컨트롤러 호출을 해서 나머지 로직을 동작하게 된다.
```