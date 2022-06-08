# Transforming Operators

# 요소들을 변환해주는 변환 연산자
- 조합을 하기 위한 방법으로 자주 사용된다.

# 1) 변환 연산자의 요소들

1. toArray
   - 말 그대로 Observable의 독립적 요소들을 Array형태로 조합해준다. 
2. map
   - swift의 map과 동일한 동작
3. enumerated
   - 객체를 튜플 형태로 반환해준다. index , value


# 2) 내부의 Observable 변환하기 

1. flatMap
   - Observable의 각 요소를 시퀀스에 반영하여 변환시킨 값을 방출하여 구독자에게 전달한다.

2. flatMapLatest
   - flatMap의 동작에서 가장 최신 값만을 방출하여 구독자에게 전달한다.

# 3) 이벤트 관찰하기

1. materialize
   - 방출되는 이벤트 자체를 이벤트의 Observable로 바꿔주는 역할을 한다. 1이라는 요소가 방출될 때 next(1) 이런 식으로.

2. dematerialize
   - materialize됐던 요소를 다시 원 요소로 변환한다.
