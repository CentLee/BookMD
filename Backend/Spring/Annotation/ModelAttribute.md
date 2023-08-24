# `@ModelAttribute`

#### ModelAttribute가 있으면 특정 객체를 생성한다.
#### 요청 파라미터의 이름으로 특정 객체의 프로퍼티를 찾는다. 그리고 해당 프로퍼티의 setter를 호출해서 파라미터의 값을 입력(바인딩) 한다.

#### 스프링은 해당 생략시 다음과 같은 규칙을 적용한다.
#### String , int , Integer 같은 단순 타입 = @RequestParam
#### 그 외 타입은 ModelAttribute 로 처리된다. (argument resolver로 지정해둔 타입 외)
