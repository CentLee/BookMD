# ExistentialType ( Swift 5.6 ~ ) 

  - 프로토콜을 구현할 때 예전부터 사실상 사용해왔지만 Static Dispatch vs Dynamic과 관련해서 비교적 차이가 있어서 기록함.
  - 실제로 Swift 6부턴 2) 구현에 대해서 에러가 날 것이므로 ExistentialType에는 반드시 any를 명시해야 한다.
 
  프로토콜 구현 예시
  
    Protocol Pet {
      func feed()
    }
    
    Struct Dog: Pet {
      func feed() { print("먹이를 주다") }
    }
    
    1) 
    func feedToPet<T: Pet>(to pet: T) { pet.eat() }
    // 해당 프로토콜을 준수하는 concreteType만 받을 수 있다.
    
    let dog = Dog() // Good
    
    vs
    
    let dog: Pet = Dog() // Error 이 경우 Pet은 ExistentialType이다.
    
    Error가 발생하는 이유는 프로토콜을 준수하는 타입만 받기로 되어 있으나, 프로토콜 그 자체로 넘겨졌기 때문이다.
    제대로 실행이 되는 코드는 프로토콜을 준수하는 타입을 받아서 Dog의 feed함수를 직접적으로 호출하게 된다.
    즉, 컴파일타임에 어떤 구현을 할 지 알기에 Static Dispatch에 속하고 최적화된 코드가 된다.
    
    
    2)
    func feedToPet(to pet: Pet) { pet.eat() }
    
    let dog: Pet = Dog(()
    컴파일 때 어떤 구현을 하는 지 알 수 없게 되므로 dynamic Dispatch가 된다.
    
    Generic을 사용하지 않고 2) 코드처럼 ExistentialType을 사용해서 구현하게 되면 
    Dynamic Dispatch가 되어 제네릭보다 비용이 많이 들기 때문에 최적화를 위해 제네릭을 사용해서 구현하는 것이 좋다.
    
    Swift 6 Impl
    let dog: any Pet = Dog()
    
# 참고 
  - ZeddiOS님 블로그
