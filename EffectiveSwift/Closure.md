# Closure

* Closuer vs Block 
  - 두 가지 모두 익명함수를 뜻한다.
  - 클로저와 Block의 차이는 외부 변수를 캡쳐하는 방식이 차이가 있다.
  ```swift
    1. Closure
       var num = 10
       let closure = { print(num) }
       
       num = 20
       print(num)
       closure() // 클로저 실행 

  ```
  - 실제 출력값은 20 과 20 으로 Swift의 클로저는 캡쳐할 변수가 Value/Reference Type인지 여부와 상관없이 참조 타입으로 캡쳐하게 된다.
  - Value Type으로 캡쳐를 하고 싶다면 [num1, num2] in 이런식으로 캡쳐해서 사용한다.
  - Block의 경우는 Value Reference Type에 맞게 각각 캡쳐를 하게 되므로 Value( Int, Double, Struct ) 등을 캡쳐하면 const Value로 캡쳐한다.
