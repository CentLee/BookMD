# DispatcherServlet Structure

#### 스프링 MVC도 프론트 컨트롤러 패턴으로 구현되어 있다.
#### 스프링 MVC의 프론트 컨트롤러가 바로 디스패처 서블릿(DispatcherServlet)이다. 그리고 이 디스패처 서블릿이 바로 스프링 MVC의 핵심이다.
#### DispacherServlet도 부모 클래스에서 HttpServlet 을 상속 받아서 사용하고, 서블릿으로 동작한다.

#### 스프링 부트는 DispacherServlet 을 서블릿으로 자동으로 등록하면서 모든 경로( urlPatterns="/" )에 대해서 매핑한다. 더 자세한 경로가 우선순위가 높다. 그래서 기존에 등록한 서블릿도 함께 동작한다. 

### 요청 흐름    
1. 서블릿이 호출되면 HttpServlet 이 제공하는 serivce() 가 호출된다.
2. 스프링 MVC는 DispatcherServlet 의 부모인 FrameworkServlet 에서 service() 를 오버라이드 해두었다.
3. FrameworkServlet.service() 를 시작으로 여러 메서드가 호출되면서 DispacherServlet.doDispatch() 가 호출된다.
