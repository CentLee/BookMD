# Exception Resolver

#### 스프링은 기본적으로 제공하는 Exception Resolver에 세 가지 종류가 있다. 

#### HandlerExceptionResolverComposite 에 다음 순서로 등록
1. ExceptionHandlerExceptionResolver = @ExceptionHandler 을 처리한다. API 예외 처리는 대부분 이 기능으로 해결
2. ResponseStatusExceptionResolver = HTTP 상태 코드를 지정해준다. 
```java 
@ResponseStatus(value = HttpStatus.NOT_FOUND) 
```
- @ResponseStatus 는 개발자가 직접 변경할 수 없는 예외에는 적용할 수 없다. (애노테이션을 직접 넣어야 하는데, 내가 코드를 수정할 수 없는 라이브러리의 예외 코드 같은 곳에는 적용할 수 없다.)
- 추가로 애노테이션을 사용하기 때문에 조건에 따라 동적으로 변경하는 것도 어렵다. 이때는 ResponseStatusException 예외를 사용하면 된다.

3. DefaultHandlerExceptionResolver = 우선 순위가 가장 낮으며 스프링 내부 예외 처리