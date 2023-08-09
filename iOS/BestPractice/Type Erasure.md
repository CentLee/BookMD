# Opaque Type And Type Erasure
- Swift 5.1에서 추가된 Opaque Type 과 Type Erasure에 대한 설명

## Opaque Type
- Swift 프로토콜을 반환할 때, 프로토콜이 아닌 해당 프로토콜을 따르는 타입을 반환하면 에러가 발생함
```swift
func aaa() -> Comparable {
  return 1
}
이런 식으로 구현하면 프로토콜을 준수하는 Int 타입을 반환하므로 에러가 발생

return Type을 T로 변경을 해도 1 as! T 라고 명시를 해야됨

이걸 더 간결하게 표현하기 위해 some라는 Opaque Type을 사용하면 

func aaa() -> some Comparable {
  return 1
} 
으로 표현이 가능

고로 SwiftUI 의 some View도 같은 방식임
```
- 하지만 이런 방식에서 분기처리와 같은 형식으로 여러 타입을 분기 처리하게 된다면 에러가 발생
- 이로 인해 SwiftUI 에서 사용하는 AnyView AnyPublisher eraseToAnyPublisher() 와 같은 타입 지우기 방식을 사용

## Type Erasure

```swift
private protocol TypeErasedBox {
  var value: Any { get }
}

private struct ComparableTypeErased<T: Comparable>: TypeErasedBox {
  let origin: T
  var value: Any { self.origin }
}

struct AnyCompare: Comparable {
  private var eraser: TypeErasedBox

  public init<T>(_ value: T) where T : Comparable {
    eraser = ComparableTypeErased(origin: value)
  }

  static func < (lhs: AnyCompare, rhs: AnyCompare) -> Bool {
    return false
  }
  static func == (lhs: AnyCompare, rhs: AnyCompare) -> Bool {
    return false
  }
}

func aaa() -> some Comparable {
  if true { return AnyCompare(1) }
  else { return AnyCompare("a") }
}
이런 방식으로 AnyCompare를 사용해서 Comparable 프로토콜을 따르는 타입을 숨길 수 있음.
```

- 더 많은 프로토콜을 사용하고 케이스들을 접해야 익숙해질 기법으로 생각됨. 
출처: 민소네님 블로그


