# Property Wrapper
- Property Wrapper는 반복되는 로직들을 프로퍼티 자체에 연결할 수 있다.

- Example
```swift

@propertyWrapper
struct UserDefault<T> {
  let key: String 
  let defaultValue: T
  
  var wrappedValue: T {
    get { UserDefaults.standard.object(forKey: self.key) as? T ?? self.defaultValue }
    set { UserDefaults.standard.set(newValue, forKey: self.key) }  
  }
}

final class UserManager {
    @UserDefault(key: "isLoggedIn", defaultValue: false)
    static var isLoggedIn: Bool
    
    @UserDefault(key: "isOnboarding", defaultValue: false)
    static var isOnboarding: Bool    
}

```
- 원래라면 get/set을 각각 프로퍼티에 로직 작성을 해줘야했지만 결국 반복되는 로직이므로 이러한 방식으로 활용할 수 있다.
- 사용사례 추가 예정
