# Chapter 9 데이터 조직화
- 하나의 변수가 여러 목적으로 사용된다면 변수 쪼개기를 하는 것이 혼란을 방지할 수 있다.

## 9.1 변수 쪼개기
- 두 가지 이상의 역할을 하는 변수 = 두 번 이상 다른 값들이 대입된다는 뜻과 유사
- 이런 경우에 변수를 쪼개는 방법을 적용한다.
- 쪼갤 때는 let 와 같이 불변하는 변수로 쪼개서 원 변수랑은 다르게 쪼갤 수 있다. JS에선 원 변수는 let, 쪼개진 변수는 const ( 특정 조건 안에서 동작한다든지 이미 사용한 값에 대해서 다시 다른 값이 대입된다든지의 경우)

## 9.2 필드 이름 바꾸기
- 데이터 테이블에 