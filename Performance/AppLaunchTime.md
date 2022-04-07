# Reduce App Launch Time

  - 앱 런치 타임을 줄이기 위한 방법론

* Remove Heavy Tasks from AppDelegate
  - 메인 스레드에서 동기적으로 동작함에 따라 시작 시간이 지연되게 됩니다.
  - 따라서 AppDelegate에는 가벼운 작업들로 구성하고 런치 이후 작업들을 배치한다.

* Reduce the Complexity of Your Initial Views
  - 초기 뷰는 가장 중요한 한 가지인데, 렌더 혹은 디자인되는 객체를 피해야한다.
  - 좌표나 색상 계산, 이미지 디코딩, 뷰의 일정 부분을 그리는 부분 등
  
* Use Placeholders until your data is loaded
  - 백그라운드에서 무거운 작업들을 수행할 때, 데이터가 로드될 때까진 스켈레톤 뷰 형태를 구현해서 플레이스홀더들을 배치해놓고 데이터가 로드 되고 난 후 데이터만 변경하는 것으로 업데이트한다.
