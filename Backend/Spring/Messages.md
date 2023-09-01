# Messages 

#### 메시지 관리 기능을 사용하려면 스프링이 제공하는 MessageSource 를 스프링 빈으로 등록하면 되는데, 스프링 부트를 사용하면 자동으로 MessageSource를 빈으로 등록해준다. 

#### 추가로 messages_언어.properties 를 사용해서 국제화를 사용할 수 있다.

#### 스프링은 언어 선택 시 기본적으로 클라이언트 측의 http 요청 헤더의 Accept-language 값을 기본적으로 사용해서 국제화 메시지를 선택한다.

#### 만약 Locale 선택 방식을 변경하려면 Locale Resolver를 사용한다.


## Locale Resolver
### AcceptHeaderLocaleResolver
#### 웹 브라우저가 전송한 Accept-Language 헤더로부터 Locale 선택한다. setLocale() 메서드를 지원  하지 않는다.

### CookieLocaleResolver
#### 쿠키를 이용해서 Locale 정보를 구한다. setLocale() 메서드는 쿠키에 Locale 정보를 저장한다.

### SessionLocaleResolver
#### 세션으로부터 Locale 정보를 구한다. setLocale() 메서드는 세션에 Locale 정보를 저장한다.

### FixedLocaleResolver
#### 웹 요청에 상관없이 특정한 Locale로 설정한다. setLocale() 메서드를 지원하지 않는다.