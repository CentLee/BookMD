# App LifeCycle

* 어플리케이션의 생명주기
  - iOS 13 이상에서는 Scene과 SceneDelegate가 생겼는데, 사실상 iPhone 앱만 개발할 거라면 MultiWindow 가 지원되지 않는 아이폰 앱은 Scene을 manifest에서 지우고 사용해도 무방하다.
 
* 일반적인 App-Based의 LifeCycle
  - Not Running 실행되지 않았거나, 시스템에 의해 종료된 상태
  
  - Foreground
    - InActive 활성화는 되어있으나, 실질적인 Event를 받지는 않는다.
    - Active 활성화가 되어있으며, Event 또한 받는다.
    
  - Background 
    - suspend 앱이 백그라운드 상태에서 메모리만 점유하고 있는 프로세스 대기 상태이며, 메모리가 부족할 시 시스템에서 강제종료 시킨다.
    
  - Terminate 앱 종료직전 실행
