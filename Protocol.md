# Protocol

- vs Java Interface

* Swift의 Protocol은 파라미터에 기본 값을 지정할 수 없다.
  
* Swift의 Protocol의 Optional 메소드를 이용해서 필수 구현부가 아닌 메소드를 구분하여 선택적 구현 가능

* static 키워드를 사용한 멤버 변수 선언 가능


# Protocol 대표적인 용법 4가지

* Action enablers 각각의 주어진 타입에 정의된 동작을 하도록 함
  ```swift
  protocol Equatable {
    static func ==(lhs: Self, rhs: Self) -> Bool
  }
  
  동등한 지를 검사하는 프로토콜 
  이와 같이 주어진 타입에 대한 동작을 하는 용법
  ```
  
* Defining requirements 특정한 종류의 객체가 되기 위함
  ```swift
  Colorable -> ColorProvider
  protocol ColorProvider {
    var foregroundColor: UIColor { get }
    var backgroundColor: UIColor { get }
  }
  이와 같이 정보를 제공하는 컬러 객체 
  ```
  
* Type conversions 다른 값으로부터 convertible이 가능한 타입을 정의하는 프로토콜
  ```swift
  protocol ImageConvertible {
    func makeImage() -> UIImage
  }
  많은 양의 계산이 필요할 때는 프로퍼티보다 메소드에 더 용이하다. 
  ```

* Abstract Interfaces 여러 타입을 추상화하는 프로토콜
  ```swift
  protocol MTLDevice: NSObjectProtocol {
    var name: String { get }
    var registryID: UInt64 { get }
  ...
  }
  ```
