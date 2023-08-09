# App LifeCycle

* 어플리케이션의 생명주기
  - iOS 13 이상에서는 Scene과 SceneDelegate가 생겼는데, 사실상 iPhone 앱만 개발할 거라면 MultiWindow 가 지원되지 않는 아이폰 앱은 Scene을 manifest에서 지우고 사용해도 무방하다.
 
* [사용자가 앱을 클릭했을 때]
- 사용자가 앱 아이콘을 클릭한다
- UIApplication 객체가 생성된다.
- 이후 @UIApplicationMain or @Main 이 있는 곳을 찾아 AppDelegate 객체를 생성한다.
- 그리고 Main Event Loop 실행

* [앱 실행 이후]
- 사용자는 앱과의 상호작용을 하는데,
- 터치 혹은 포커스와 같은 이벤트가 발생하면 오퍼레이팅 시스템을 통해 이벤트 큐로 들어가게 되는데
- 이벤트 큐에서 이벤트 소스가 메인 런루프에 매핑되고 
- UIApplication 객체가 이벤트의 우선 순위를 결정해 다시 오퍼레이팅 시스템을 통해 앱에 전달하게 된다.

* 일반적인 App-Based의 LifeCycle (State)
  - Not Running 실행되지 않았거나, 시스템에 의해 종료된 상태
  
  - Foreground
    - InActive 활성화는 되어있으나, 실질적인 Event를 받지는 않는다.
    - Active 활성화가 되어있으며, Event 또한 받는다.
    
  - Background 
    - suspend 앱이 백그라운드 상태에서 메모리만 점유하고 있는 프로세스 대기 상태이며, 메모리가 부족할 시 시스템에서 강제종료 시킨다.
    
  - Terminate 앱 종료직전 실행
