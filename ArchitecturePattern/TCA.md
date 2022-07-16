# The Composable Architecture

- TCA의 기본 개념: 큰 기능들을 분리해 구조적인 모듈로 나누고 이를 이용하는것


## TCA Advantages
- Point-Free에서 구현된 상태 관리 기반 아키텍쳐이며, SwiftUI 또한 UIKit과는 다르게 상태 기반 UI 프레임워크이기 때문에 적용하기에 적합하다.
- SwiftUI, UIKit 등 범용성 높은 프레임워크
- 뷰의 변화를 크고 작은 기능을 붙여 작은 도메인으로 나누어 보여줄 수 있음
- ReactorKit과 유사하지만 mutate 같은 작업을 한 번 더 하지않아도 된다.

## TCA Composition

 - State: 기능 수행 및 UI 렌더링을 위한 데이터 타입

 - Action: 사용자 작업, 알림, 이벤트 소스 기능에서 발생할 수 있는 모든 작업을 나타내는 타입

 - Environment: API 클라이언트, 분석 클라이언트 등과 같이 기능에 필요한 종속성을 보유하는 타입

 - Reducer: 액션으로 상태 업데이트를 해주는 로직 함수로 모든 결과가 Effect 타입으로 반환

 - Store: 실제로 기능을 구동하는 런타임으로 스토어가 리듀서와 이펙트를 실행하도록 사용자의 액션을 스토어에 보내고 스토어에서 상태
 
## TCA Flow
 
![TCA Flow](https://user-images.githubusercontent.com/35019052/179349182-e0e28804-ae6f-4797-9865-876ac2b0c930.png)

1. 필요한 View 정의

2. Store를 사용하여 작업 전달: 액션으로 핸들러 및 작업을 전달

3. Reducer에서 비지니스 로직 코드 처리

4. 사이드 이펙트 및 종속성 처리: Effect 처리 및 Environment를 통해 주입

5. 상태 업데이트: 자동으로 동기화하여 State에 따른 View 업데이트
