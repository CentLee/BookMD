# BindingResult

### 스프링의 검증 오류를 보관하는 객체 
### 주의해야할 점은 BindingResult bindingResult 파라미터의 위치는 @ModelAttribute Item item 다음에 와야 한다. 
### 이 오류를 이용해서 타임리프에서 errors를 활용해서 뷰로 표현해줄 수 있다. 

```html
<div th:if="${#fields.hasGlobalErrors()}">
      <p class="field-error" th:each="err : ${#fields.globalErrors()}" th:text="$
{err}">전체 오류 메시지</p> </div>
```

```html
<input type="text" id="itemName" th:field="*{itemName}" th:errorclass="field-error" class="form-control" placeholder="이름을
입력하세요">
<div class="field-error" th:errors="*{itemName}">
상품명 오류
</div>
```

### ModelAttribute 타입 오류가 발생했을 때 BindingResult가 없으면 400에러 있으면 스프링이 FieldError를 담아서 컨트롤러를 호출해서 직접 전달해준다.

#### FieldError 생성자
```java
  public FieldError(String objectName, String field, String defaultMessage);
  public FieldError(String objectName, String field, @Nullable Object
  rejectedValue, boolean bindingFailure, @Nullable String[] codes, @Nullable
  Object[] arguments, @Nullable String defaultMessage)

  rejectedValue 오류가 났을 때 입력된 값 유지할 수 있다.
```

#### FieldError나 ObjectError를 직접 생성하는 것보다 더 간단하게 BindingResult의 RejectValue, reject를 활용하여 코드를 더 간단히 작성할 수 있다.


#### 타입 오류가 발생해서 스프링이 직접 FieldError를 전달해주면 그 안에는 typeMismatch라는 코드를 전달해준다. 그 코드를 프로퍼티를 사용해서 치환해서 같이 사용가능하다.
