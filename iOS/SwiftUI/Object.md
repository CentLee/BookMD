# @StateObject vs @ObservedObject

* @StateObject: @ObservedObject + State
(ObservedObject와 State는 변경사항이 있을때 뷰를 다시그리는 점에 있어서 같은역할이지만 이름이달라서 합쳐놓은듯한 느낌임)

- View를 다시 랜더링할때 실수로 취소되는것을 방지해주면서, 가장 큰 차이점은 소유라고함

*StateObject*는 `라이프사이클에 의존하지 않고` 다시그려지거나 네비게이션으로 넘어가서 화면이사라졌다가 나타나도 재사용되도록 유지되는 반면에

*ObservedObject*는 `라이프사이클에 의존해서` 뷰가 그려질때 다시 생성하게되어 값이 초기화되서 무거운작업 이있다면 성능에 영향이 있을수 있음

observedObject는 published 변수가 변경되면 뷰를 다시그리도록 해줍니다.
하지만 뷰가 그려질때 다시 생성되는 문제 발생
