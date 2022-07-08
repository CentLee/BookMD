How to use Preprocessor Statement in Swift Project
- iOS 상에서 전처리 구문을 활용하는 방법에 대한 글이다.
- 전처리란 컴파일 타임 전에 미리 처리되는 것을 의미한다.

# Preprocessor Usecases in Swift

## Between Release and Debug
- 많이들 사용하는 방법으로 디버그와 릴리즈 모드 플래그를 두어 각 모드에 맞게 동작하게끔 사용하는 방법이다.
- 저 역시 Debug 프린트 문을 따로 디버그모드로 설정하여 어떤 파일 라인에서 출력되는지 등 라이브러리 개발 때도 유용하게 사용할 수 있다.
```swift
#if DEBUG
  print("print on debug environment only")
#endif
```

## Distinguish OS
- iOS tvOS WatchOS 등 다양한 OS 버전을 구분하는 방법이다.
```swift
#if os(iOS)
  print("print on iOS only")
#elseif os(macOS)
  print("print on macOS only")
#elseif os(watchOS)
  print("print on watchOS only")
#endif
``` 

### Custom Flag
- 그 외에 또 다른 플래그를 추가하고 싶다면 Build Setting 에서 CustomFlag에 디버그 릴리즈 모드에 맞게 추가해서 사용하면 된다.
