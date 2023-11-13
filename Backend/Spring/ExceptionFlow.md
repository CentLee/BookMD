# ExceptionFlow


### 정상 요청 시

- WAS(/hello, dispatchType=REQUEST) -> 필터 -> 서블릿 -> 인터셉터 -> 컨트롤러 -> View

### 에러 요청 시

1. WAS(/error-ex, dispatchType=REQUEST) -> 필터 -> 서블릿 -> 인터셉터 -> 컨트롤러
2. WAS(여기까지 전파) <- 필터 <- 서블릿 <- 인터셉터 <- 컨트롤러(예외발생)
3. WAS 오류 페이지 확인
4. WAS(/error-page/500, dispatchType=ERROR) -> 필터(x) -> 서블릿 -> 인터셉터(x) -> 컨트롤러(/error-page/500) -> View


#### WebServerCustomizer 와 ErrorPages로 원하는 error page에 대해 요청을 처리해서 뷰를 표현할 수 있지만 스프링은 기본적으로 BasicErrorController에 포함되어있다.

### BasicErrorController
#### @RequestMapping("${server.error.path:${error.path:/error}}") 으로 기본 매핑되어 있어서 편하게 template를 만들어 에러를 표현해줄 수 있다.

#### BasicErrorController는 정보를 담아서 Model에 담아 뷰에 전달해준다. 

* timestamp: Fri Feb 05 00:00:00 KST 2021
* status: 400
* error: Bad Request
* exception: org.springframework.validation.BindException * trace: 예외 trace
* message: Validation failed for object='data'. Error count: 1 * errors: Errors(BindingResult)
* path: 클라이언트 요청 경로 (`/hello`)