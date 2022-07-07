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

* Escaping Closure 
  - non-escaping 클로저는 컴파일러가 클로저의 실행이 언제 종료되는지 알기 때문에, 때에 따라 클로저에서 사용하는 특정 객체에 대한 retain, release 등의 처리를 생략해서 객체의 라이프싸이클(life-cycle)을 효율적으로 관리할 수 있습니다. 
  - 반면 esacping 클로저는 함수 밖에서 실행되기 때문에 클로저가 함수 밖에서도 적절히 실행되는 것을 보장하기 위해, 클로저에서 사용하는 객체에 대한 추가적인 참조싸이클(reference cycles) 관리 등을 해줘야 합니다. 이 부분이 컴파일러의 퍼포먼스와 최적화에 영향을 끼치기 때문에 Swift에서는 필요할 때만 escaping 클로저를 사용하도록 구분해 두었습니다.
  - 그러므로 non-escaping이 default고 상황에 따라 외부의 변수를 캡쳐해서 클로저를 실행해야할 때 escaping을 사용할 수 있다.
