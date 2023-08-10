# Bean Life Cycle

### 스프링은 의존관계 주입이 완료되면 스프링 빈에게 콜백 메서드를 통해서 초기화 시점을 알려주는 다양한 기능을 제공한다. 또한 스프링은 스프링 컨테이너가 종료되기 직전에 소멸 콜백 을 준다.

#### 스프링 빈의 이벤트 라이프사이클은 다음과 같이 진행된다.
#### 스프링 컨테이너 생성 -> 스프링 빈 생성 -> 의존관계 주입 -> 초기화 콜백 -> 사용 -> 소멸전 콜백
- 초기화 콜백: 빈이 생성되고, 빈의 의존관계 주입이 완료된 후 호출 
- 소멸전 콜백: 빈이 소멸되기 직전에 호출


### 스프링은 크게 3가지 방법으로 빈 생명주기 콜백을 지원한다
1. 인터페이스(InitializingBean, DisposableBean) 
2. 설정 정보에 초기화 메서드, 종료 메서드 지정 
3. @PostConstruct, @PreDestroy 애노테이션 지원


### 인터페이스(InitializingBean, DisposableBean) 
* implements InitializingBean, DisposableBean 을 사용하여 초기화 콜백 및 소멸 콜백에 대한 함수를 오버라이딩해서 의존관계 주입 이후 데이터베이스 연결 혹은 소켓 연결 등의 행위를 하게끔 지원한다.
    - `InitializingBean` 은 `afterPropertiesSet()` 메서드로 초기화를 지원한다. 
    - `DisposableBean` 은 `destroy()` 메서드로 소멸을 지원한다.

### 빈 등록 초기화, 소멸 메서드 지정
* `@Bean(initMethod = "init", destroyMethod = "close")` 이런 식으로 실제 빈 수동 등록 시에 지정하여 사용한다. 
    - 메소드 이름을 자유롭게 사용 가능
    - 스프링 코드에 의존하지 않는다. 
    - Configuration을 사용하기 때문에 외부 라이브러리에도 지정해서 사용할 수 있다. 

* destoryMethod는 기본적으로 inferred으로 등록되어 있어 메소드를 추론하게 되는데 대부분 외부 라이브러리가 close, shutdown같은 종료 메소드를 사용하기 때문에 등록해두면 추론기능을 사용하고 
* destoryMethod를 공백으로 두면 추론을 사용하지 않는다.

### `@PostConstruct` `@PreDestroy` 사용
* 최신 스프링 버전에서 권장하는 기능


#### 외부 라이브러리에 빈 생명주기 콜백을 지원하고 싶다면 메소드 지정 방법을 사용하고 그 외엔 어노테이션을 간단히 사용하는 방식을 채택한다. 