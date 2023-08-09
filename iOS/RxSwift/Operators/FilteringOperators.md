# Filtering Operators 

# IgnoreElements

   - `ignoreElements`는 `.next` 이벤트를 무시한다. `completed`나 `.error` 같은 정지 이벤트는 허용한다.

# ElementAt

   -  Observable에서 방출된 n번째 요소만 처리하려는 경우가 있을 수 있다. 이 때 `elementAt()`을 쓸 수 있다. 이 것은 받고싶은 요소에 해당하는 index만을 방출하고 나머지는 무시한다.
   
# Filter

  - 고차함수의 Filter와 유사하다.

# Skip

  - `skip` 연산자는 첫 번째 요소부터 n개의 요소를 skip하게 해준다. 


  - `skipwWhile`은 skip할 로직을 구성하고 해당 로직이 `false` 되었을 때 방출한다. `filter`와 반대다.


  - `skipUntil`은 다른 observable이 `.next`이벤트를 방출하기 전까지는 기존 observable에서 방출하는 이벤트들을 무시하는 것이다. 방출시키기 위한 trigger이 필요하다.

# Take

  - Skip의 반대 개념으로 몇 가지의 요소를 Take하게 해준다.

  - `takeWhile`은 `skipWhile`처럼 작동한다. 

  - `enumerated` 은 기존 Swift의 `enumerated` 메소드와 유사하게, Observable에서 나오는 각 요소의 index와 값을 포함하는 튜플을 생성하게 된다.

  - `skipUntil`처럼 `takeUntil`도 있다. 동작은 반대로 한다. 트리거가 발동했을 시점의 전의 값들만 취하게 된다.

# DistinctUntilChanged

  - 같은 값을 전달받지 않기 위해 사용한다.
