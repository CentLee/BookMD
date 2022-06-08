# Combining Operators

# 1) 초기값의 여부 

1. startWith
   - 예를 들면 "현재 위치"나 "네트워크 연결 상태" 같이 "현재 상태"가 필요한 상황이 있다. 이럴 때 현재 상태와 함께 초기값을 붙일 수 있다.
2. concat
   - 이전 시퀀스를 다른 시퀀스 앞에 묶어서 serial하게 가져갈 수 있다.
   - 예를 들어 어떤 api의 값을 가져와서 그 값을 가지고 또 다른 api를 호출해야하는 상황이 일어날 때 사용할 수 있다.
  
3. concatMap
   - concatMap은 각각의 sequence가 다음 sequence가 구독되기 전에 합쳐진다는 것을 보증한다.

# 2) 병합

1. merge
   - 두 개의 Observable를 합친다.
   - merge는 도착한 순서대로 합치게 된다.
2. merge(maxConcurrent:)
   - 말 그대로 합칠 수 있는 시퀀스의 수를 제한하고, 최대 수까지 도달하기 전에는 계속 일어난다. 

# 3) 요소 결합

1. combineLatest
   - 어떠한 두 Observable를 결합하여 방출하게 되는데, 예를 들어 api 두 개를 각각 페치하여 관찰을 해야할 경우 사용하여 최종값들을 하나의 Observable로 방출한다.
2. zip
   - zip 같은 경우에는 두 Observable에서 방출되는 요소에 각각 대응하여 결합하게 되는데 한쪽에서 방출되고 다른 한 쪽에서 방출되지 않는다면, 그 시퀀스는 방출되지 않는 성질을 지닌다.
   
# 4) 시퀀스 내부 요소들간 결합
1. reduce 
   - Swift의 Reduce와 동일하다. 시퀀스 내부 요소들 간 결합을 한 후 그 최종값을 Observable로 만든다.
2. scan
   - scan은 scan(_:accumulator:)가 있고 그냥 스캔을 사용할 수 있다.
   - 일반적인 스캔을 사용할 땐 예를 들어 텍스트필드의 글자 수를 제한해야하는 경우에 이전 값과 새 값을 가져와서 연산을 통해 제한을 하는 데에 사용할 수 있다.
   - accmulator을 사용하게 될 땐 전 값과 새 값을 reduce와 비슷하게 작동하지만 요소 전 + 새 값을 더한 값을 Observable로 방출하게 된다.
   - 총합, 통계, 상태를 계산하여 제한 등 다양하게 사용할 수 있다.

# 5) Switches And Triggers
1. sample
   - withLatestFrom과 비슷하게 동작하지만, 한 번만 방출한다. 
2. withLatestFrom
   - 여러 개의 요소를 한 번에 받는 Observable를 다른 Observable가 최신 값을 통해 방아쇠처럼 다른 Observable의 시퀀스가 방출되게끔 해주는 연산자이다.

3. amb
   - 두 Observable 중 어떤 Observable를 받을 

4. switchLatest 
