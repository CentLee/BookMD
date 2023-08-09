# RunLoop

- RunLoop 객체는 소켓 파일 키보드 마우스 등의 입력 소스를 처리하는 이벤트 처리 루프이며, 스레드가 일해야할 때 일하고 일이 없으면 쉬게하는 목적으로 나오게 된 객체이다


## RunLoop Feature
- 스레드는 모두 각자의 RunLoop를 가질 수 있다.
- 스레드가 생성될 때 RunLoop가 자동으로 생성된다.
- 하지만, Main RunLoop를 제외하곤 생성되고 자동으로 실행되진 않는다.

```swift
DispatchQueue.global().async {
  Timer.scheduledTimer(withTimeInterval: 1, repeats: falst { _ in
    print("Timer Test") //1초 마다 이 출력문이 동작하게 하는 타이머
  }
}

이 경우에는 직접 run()을 통해 실행시켜주지 않으면 동작하지 않게 된다.
```

## RunLoop Principle of operation

- 내부적으로 한 사이클 동안 들어온 이벤트를 받아서 핸들링하는 역할을 하는데 고안된 목적에 맞게 한 사이클이 끝나면 자동적으로 대기하게 된다. 


```swift
DispatchQueue.global().async {
  let runLoop = RunLoop.current
  Timer.scheduledTimer(withTimeInterval: 1, repeats: falst { _ in
    print("Timer Test") //1초 마다 이 출력문이 동작하게 하는 타이머
  }
  
  runLoop.run() //이 실행 전에 부착된 입력 소스만 동작하게 된다.
  
  Timer.scheduledTimer(withTimeInterval: 1, repeats: falst { _ in
    print("Timer Test22") //이 타이머는 동작하지 않고 
  }
 
 
  runLoop.run() // 다시 여기서 부착해주는 수밖에 없다. 추가된 형태로 
}

실행은 run() 함수를 통해서 동작하는데,
이 run()을 실행시키기 전에 타이머나 여러 입력소스가 있으면 그것에 대해서 실행하는 것이다.
즉, run() 이후 다른 입력소스를 부착해도 리시버엔 전달되지 않는다.

위 방식을 해결하려면
run(until:) 을 사용하면 어떤 지정된 날짜까지 부착된 입력소스는 모두 동작하도록 사용할 수 있는 함수이다.
```
- 특별히 Main RunLoop는 currentMode가 소스나 타이머가 비어있는지 검사할때 안 비어 있는 식으로 처리합니다.

