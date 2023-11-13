# Transaction 

# 데이터베이스 작업의 논리적 단위

### 트랜잭션 추상화

-  스프링 트랜잭션 추상화의 핵심은 PlatformTransactionManager 인터페이스이다. (org.springframework.transaction.PlatformTransactionManager)
- JDBC JPA 하이버네이트 등 트랜잭션 인터페이스를 추상화한 인터페이스를 제공하기때문에 이 부분을 사용하고
- 스프링 5.3부터는 JDBC 트랜잭션을 관리할 때 DataSourceTransactionManager 를 상속받아서 약간의 기능을 확장한 JdbcTransactionManager 를 제공한다. 둘의 기능 차이는 크지 않으므로 같은 것으로 이해 하면 된다.


#### 스프링이 제공하는 트랜잭션 매니저는 크게 2가지 역할을 한다. 
1. 트랜잭션 추상화
2. 리소스 동기화


#### 트랜잭션 동기화 매니저 동작 방식을 간단하게 설명하면 다음과 같다.
1. 트랜잭션을 시작하려면 커넥션이 필요하다. 트랜잭션 매니저는 데이터소스를 통해 커넥션을 만들고 트랜잭션을 시작한다.
2. 트랜잭션 매니저는 트랜잭션이 시작된 커넥션을 트랜잭션 동기화 매니저에 보관한다.
3. 리포지토리는 트랜잭션 동기화 매니저에 보관된 커넥션을 꺼내서 사용한다. 따라서 파라미터로 커넥션을 전달하지 않아도 된다.
4. 트랜잭션이 종료되면 트랜잭션 매니저는 트랜잭션 동기화 매니저에 보관된 커넥션을 통해 트랜잭션을 종료하고, 커넥션도 닫는다.


* DataSourceUtils.releaseConnection() 을 사용하면 커넥션을 바로 닫는 것이 아니다. 
* 트랜잭션을 사용하기 위해 동기화된 커넥션은 커넥션을 닫지 않고 그대로 유지해준다.
* 트랜잭션 동기화 매니저가 관리하는 커넥션이 없는 경우 해당 커넥션을 닫는다.



#### 다른 서비스에서 트랜잭션을 시작하려면 try , catch , finally 를 포함한 성공시 커밋, 실패시 롤백 코드 가 반복될 것이다.
#### 이 문제를 해결하려면 템플릿 콜백 패턴을 사용하면 해결되는데 스프링은 TransactionTemplate를 제공하기때문에 해결가능하다. 

```java
    public class TransactionTemplate {
      private PlatformTransactionManager transactionManager;
      public <T> T execute(TransactionCallback<T> action){..}
      void executeWithoutResult(Consumer<TransactionStatus> action){..}
  }

  execute() : 응답 값이 있을 때 사용한다. 
  executeWithoutResult() : 응답 값이 없을 때 사용한다.

  내부 구조를 확인해보면 트랜잭션을 수행하고 Rollback과 Commit을 대신 수행해준다.
```


#### 비즈니스 로직을 처리하는 서비스에서 문제를 해결했지만, 남은 문제는 서비스 로직 외에 트랜잭션 코드가 어쩔 수 없이 포함되게 된다. 
#### 이 문제를 해결하려면 트랜잭션 AOP (`@Transactional`) 를 활용하여 해결할 수 있고 프록시를 도입하여 해결할 수 있다. 
#### Transaction Proxy 라는 것으로 트랜잭션을 대신 처리해주는데 어노테이션을 해당 함수에 적용만 하면 이 프록시를 스프링은 인식해서 해결해준다.

#### 어노테이션을 활용하려면 스프링 컨테이너가 필요함으로 테스트 시에는 SpringBootTest 어노테이션을 테스트 클래스에 사용하여 테스트해야 트랜잭션이 제대로 동작한다.

### 선언적 트랜잭션 관리(Declarative Transaction Management)
#### @Transactional 애노테이션 하나만 선언해서 매우 편리하게 트랜잭션을 적용하는 것을 선언적 트랜잭션 관리라 한다.
- 선언적 트랜잭션 관리는 과거 XML에 설정하기도 했다. 이름 그대로 해당 로직에 트랜잭션을 적용하겠 다 라고 어딘가에 선언하기만 하면 트랜잭션이 적용되는 방식이다.

#### 프로그래밍 방식의 트랜잭션 관리(programmatic transaction management)
- 트랜잭션 매니저 또는 트랜잭션 템플릿 등을 사용해서 트랜잭션 관련 코드를 직접 작성하는 것을 프로 그래밍 방식의 트랜잭션 관리라 한다.

