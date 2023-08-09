# Refactoring Chapter 1 Summary 

## 1.2
- 프로그램이 잘 작동하는 상황에서 굳이 코드가 지저분하다(분기 처리 및 많은 변수 사용 등)라는 이유로 코드를 수정해야한다고 불평하는 것은 옳지 않다.
- 따라서 수 백줄의 코드를 수정해야하는 상황이라면 구조를 먼저 수정을 하고 원하는 기능을 구조에 맞춰 추가한다.

## 1.3 
- 리팩토링의 첫 단계는 리팩토링할 영역에 대한 테스트 코드 작성(TDD) 마련하기다.
- 리팩토링을 할 때 버그를 줄여줄 수 있는 여지를 최대한 마련하기 위해서이다.

## 1.4
- 큰 함수를 쪼개는 방법은 보편적으로 큰 함수 안에 존재하는 분기처리 (switch , if-else)와 같은 구문을 별도의 함수로 추출하는 Method Extract를 진행하는 것이 기본적인 방법이다.
- 함수를 추출할 때 변하지 않는 함수를 매개변수로 전달하고 해당 함수 안에서 값이 변하는 변수를 최종적으로 리턴한다.
- 그리고 매개변수의 역할이 뚜렷하지 않을 때는 a/an 부정 관사를 붙여서 변수명을 개선한다.
- 매개 변수로 전달이 되는 변수들 중에서 한 구조체의 인스턴스로 존재하는 변수라면, 이또한 임시 변수를 질의함수로 변경하는 방법을 취해 개선하고 테스팅을 마치고 이상이 없다면 변수 인라인까지 적용을 한다.
- 그 외에 반복문 쪼개기, 문장 슬라이드 등의 방법이 존재하며, 챕터 5부터 본격적으로 나온다하니 그 때 다시 정리.
- 핵심은 최상위 함수를 단 몇 줄의 코드 라인으로 보조함수를 통해서 줄이는 방법이다.

## 1.6
- 계산 함수와 반복문 쪼개기 중복 내용

## 1.8
- 다형성을 활용해 계산 함수 및 분기 처리 적용하기
- Swift를 예로 들면 Protocol과 Enum 등을 활용해서 적용할 수 있다.
