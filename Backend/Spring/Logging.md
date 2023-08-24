# Logging

#### 스프링 부트 라이브러리를 사용하면 스프링 부트 로깅 라이브러리( spring-boot-starter-logging )가 함께 포함된다.
#### 스프링 부트 로깅 라이브러리는 기본으로 다음 로깅 라이브러리를 사용한다.
1. SLF4J
2. Logback

#### 무슨 차이가 있냐하면 로그 라이브러리는 Logback, Log4J, Log4J2 등등 수 많은 라이브러리가 있는데, 그것을 통합해서 인터페이스로 제공하는 것이 바로 SLF4J 라이브러리다.
#### 따라서 Logback 과 같은 구현체를 선택해서 구현하게 된다.
#### 실무에서는 스프링 부트가 기본으로 제공하는 Logback을 대부분 사용한다.

#### LogLevel은 5가지가 존재한다.
1. trace
2. debug
3. info
4. warn
5. error 

#### 여기서 보통 개발 서버는 debug, 운영 서버는 info로 배포하여 사용한다.