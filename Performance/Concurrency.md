# Threads & Concurrency in Swift
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
