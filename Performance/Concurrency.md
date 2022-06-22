# Threads & Concurrency And Multithreding in Swift
- 언제 어떤 큐를 사용해야하는 가? 
- Concurrent 란 같은 시간 혹은 유사한 시간에 일어나는 것

1. Serial Queue
   - 하나의 작업 이후 다른 하나가 동작해야할 때 ( Fetch - Store - Read - Display 와 같은 작업류 )
   - 작업의 우선순위가 중요할 때 


2. Concurrent Queue
   - 동시에 작업해야할 때
   - 어떤 작업이 먼저 끝날 지 확실하지 않을 때
   - 작업의 우선 순위가 중요하지 않을 때
   - 예를 들어 백그라운드 스레드에서 데이터를 계속해서 가져오고 있는 와중 UI는 다른 업데이트가 진행된다면, Concurrency하게 동작시킬 수 있다 
   - 예를 들어 URL로 부터 이미지 데이터를 받아와서 이미지를 보여줘야할 때 해당 뷰가 테이블 셀 안의 이미지 뷰라면 어떤 셀의 이미지가 먼저 로딩될 지 모른다. 이또한 Concurrency


# MultiThreading

![thread](https://user-images.githubusercontent.com/35019052/172067057-8c711494-33e3-4cbf-b0fc-100d0d0a8d7b.png)

- DispatchQueue Main과 Background를 통해서 멀티스레드 작업을 구현할 수 있다.



## GCD

### Background  
      we can use this when a task is not time-sensitive or when the user can do some other interaction while this is happening.
      Like pre-fetching some images, loading, or processing some data in this background. This work takes significant time, seconds, minutes, and hours.
* 태스크의 시간이 민감하지 않다( 실시간이 아닌? ) 경우 혹은 다른 상호작용(UI Event)등이 일어나고 있을 때 사용할 수 있으며, 예를 들어 이미지 프리페칭, 로딩, 데이터 처리 등이 있다.


### Utility 
      long-running task. Some process what the user can see. For example, downloading some maps with indicators. When a task takes a couple of seconds and eventually a couple of minutes.
 * 긴 실행시간의 태스크. 유저가 보고 있는 것에 대한 처리, 예를 들어 지도가 인디케이터와 함께 다운로딩되는 화면 등이 있다.


### userInitiated 
      when the user starts some task from UI and waits for the result to continue interacting with the app. This task takes a couple of seconds or an instant.
 * UI로 부터 특정 태스크를 시작했고 앱과 계속해서 상호작용한 결과를 기다린다.

 
### userInteractive 
      when a user needs some task to be finished immediately to be able to proceed to the next interaction with the app. Instant task.
* 유저가 앱이 다음 상호작용을 처리가능하도록 즉시 특정 태스크를 처리해야할 때 사용할 수 있다.


## DispatchGroup
      “A group of tasks that you monitor as a single unit.” 
      한 모니터 단위로써 그룹의 태스크를 모니터링한다.
* 여러 비동기 프로세스를 진행해야하고 그 비동기 프로세스들이 모두 끝났을 때를 감지하고 싶을 때 사용할 수 있다.

## DispatchSemaPhore
      여러 실행 컨텍스트에서 리소스에 대한 액세스를 제어하는 개체
* 흔히 운영체제 단계에서 학습할 때 배웠던 전통적인 세마포어 
* 예를 들어, 사용했던 사례로는 영상을 합성해야할 때 비디오 오디오를 같이 촬영을 하고 촬영한 두 가지를 합성 시 끝났음을 signal을 통해서 신호를 전달 하면 그때 결과값을 가지고 다음 단계 작업을 할 수 있도록 제어하는 데에 용이할 수 있다.
* DispatchSemaphore(value: 1) 이런 식으로 사용하고 wait을 걸어놓으면 0이 돼서 접근이 불가하고 신호를 다시 받아야 그 개체에 대해 접근 가능

## DispatchWorkItem
      RxSwift의 textField.rx.text.debounce와는 다르게 특정 작업 아이템을 만들어놓고 GCD에서 일정 간격으로 실행되게 사용할 수 있는 디스패치 아이템? 
      
## DispatchBarrier
      This makes thread-unsafe objects thread-safe
* 예를 들어 특정 파일이 안전하게 저장되고 사용되길 바랄 때, 사용하면 작업이 진행되고 저장되고 배리어가 동작하고 그 이후 큐 내부에서 그 리소스를 활용할 수 있게 도와준다.
![DispatchBarrier](https://user-images.githubusercontent.com/35019052/175030787-f4eed109-f10a-4df2-b2da-8a7ce7cb88c6.png)

## OperationQueue 
* task의 실행, 정지, 대기와 같은 실행 상태를 알 수 있고 이를 통해 Operation들을 취소, 순서 지정이 가능
* 진행 상황과 종속성을 추적하면서 여러 클래스에 대한 책임을 분리할 수 있는 방법

## GCD vs OperationQueue
* 일반적으로 OperationQueue는 내부적으로 GCD를 기반으로 사용한다. 
* 하지만 단순하게 사용하지는 않고, 작업 간에 종속성 추가, 재사용, 취소, 일시 중지가 가능하며, Task를 기반으로 한다.
* 종속성 추가란 B.addDependency(A) 이렇게 사용을 하며 A 작업이 끝난 후 실행되게끔 할 수 있다. RxSwift의 until류 사용 사례와 비슷하다고 생각한다.
* GCD는 그에 반해 종속성 관리가 어렵고 동시에 실행될 작업 단위를 나타내는 방법이다.

## Async/Await 
* Completion Handler를 직접적으로 날려버릴 수 있는 방법이며, Await을 사용해 데이터 결과물을 기다려서 받고 다음 작업을 유도할 수 있다. JS TS의 await과 유사
* Async/Await에서 TaskGroup을 사용할 수 있는데 이는 DispatchGroup과 똑같고 async 세계에서 사용하는 그룹이다.

### Actor 
      “Actors allow only one task to access their mutable state at a time.”
* 변경가능한 상태에 대해서 어떠한 시간에 한 태스크만 접근하도록 허가하게 만드는 class, Reference Type들을 Thread-Safe하게 만들어주는 객체이다.


참고자료 - https://betterprogramming.pub/the-complete-guide-to-concurrency-and-multithreading-in-ios-59c5606795ca
