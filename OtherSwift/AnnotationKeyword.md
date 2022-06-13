# Annotation KeyWord

# @IBDesinable
- IBInspectable과는 다르게 실시간으로 컴파일 타임에 변경을 감지해서 시각적으로 볼 수 있는 연산프로퍼티이다.
- 코드만을 사용하는 UI라면 굳이 사용하지 않아도 되지만, 현재처럼 SwfitUI의 Canvas를 사용하게 된다면, 커스텀 클래스인 뷰들을 실시간으로 Canvas로 보기 위하여 지정하여 사용하면 된다.
  ```swift
  @IBDesignable
  class ParticulateMatterCircleView: UIView
  ```
  
# @IBInspectable
- 예를 들어 원형 뷰를 만들 때 해당 UIVIew의 속성을 추가시켜서 구분하여(?) 사용하게 된다.
  ```swift
  @IBInspectable var ringColor: UIColor = UIColor.clear
  {
    didSet { print("bColor was set here") }
  }
  ```
- inspector에서 해당 인터페이스 요소의 속성을 변경할 수 있게 하는 연산 프로퍼티이다
- IBInspectable은 런타임에만 동작한다.
