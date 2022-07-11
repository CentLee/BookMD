# XCTest

## XCTest Default 

### setUpWithError 
- 해당 메소드는 각각의 테스트 케이스 메소드를 호출하기 전에 셋업을 하는 함수인데, 예를 들어 api나 네트워크 테스트 시 Mock Data를 세팅하는 함수다.

### tearDownWithError
- 해당 메소드는 각각의 테스트 케이스 메소드를 호출한 후 동작하는 함수이다.



### Other
- 위 함수들을 제외하곤 테스트를 위한 데이터 셋업이 됐다면, 이제 커스텀 메소드를 만들어 테스트하면 된다.
```swift
func testMock() throws {
  ...
}
```


## XCTest Feature

### XCAssert* 
- given when 이후 then 때 확인할 수 있는 메소드들로 다양한 메소드가 존재하고, 테스트를 한 결과값이 예상한 결과값과 일치하는 지 여부를 다양한 메소드로 테스팅할 수 있다.
