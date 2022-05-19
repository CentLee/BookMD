# OCP ( Open-Closed Principle ) 확장 폐쇄 원칙
 
- 확장에는 열려있고, 변경에는 닫혀야한다.
- 확장이라는 것은 기능을 추가하고 변경하는 것에 유연해야하고, 
- 변경이라는 것은 기능을 추가하기 위해서 모듈 내부의 코드를 줄줄이 수정하지 않아야한다는 것이다.

- 가장 대표적인 위반 사례가 IF/Switch 분기문이다.
- 대부분의 SOLID 원칙 위반 사례는 Protocol로 처리를 할 수 있다.
```swift 
enum Animal {
    
    enum Size {
        case small
        case medium
        case large
    }
    
    case dog
    case cat
    case cow

    var size: Size {
        switch self {
        case .dog:
            return .medium
        case .cat:
            return .small
        case .cow:
            return .large
        }
    }
    
}
이러한 코드가 있다고 가정했을 때
```


```swift
enum AnimalSize {
  case small
  case medium
  case large
}

protocol Animal {
  var animalSize: AnimalSize { get }
}
struct Dog: Animal {
  var animalSize = AnimalSize.medium
}

이러한 방식으로 중복된 코드들을 줄일 수 있고 확장에는 유연하게 변경에는 많은 코드를 수정하지 않게 할 수 있다.
```
