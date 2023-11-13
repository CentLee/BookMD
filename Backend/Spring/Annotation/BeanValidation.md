# BeanValidation

#### Validator 로 validation하던 것을 실제 데이터 클래스에 대해 `@NotNull` 과 같은 형태로 사용하여 검증 로직을 편하게 사용할 수 있는 검증 어노테이션의 인터페이스 모음이다.
#### 일반적으로 사용하는 구현체는 하이버네이트 Validator

#### 바인딩에 성공한 필드만 Bean Validation 적용 BeanValidator는 바인딩에 실패한 필드는 BeanValidation을 적용하지 않는다. 실패하면 FieldError 추가한다.

#### ObjectError는 `@ScriptAssert()` 를 사용해서 검증하면된다.

#### 동일한 모델 객체가 존재할 때 각각 다른 방식으로 검증을 해야한다면 groups를 사용하면 된다. 

#### 하지만 groups를 쓰면 복잡도가 올라가기때문에 다른 검증 방식에 필요한 데이터를 직접 만들어서 사용하도록 데이터 클래스를 분리하는 것이 좋다. 