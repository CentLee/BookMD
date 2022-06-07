# RxSwift Traits

- UI처리에 특화된 Observable (MainThread에서 실행, Error이벤트가 없음)
- Traits를 구독하는 모든 구독자는 동일한 시퀀스를 공유 (share연산자가 내부적으로 사용된 상태)

# Single

- 1개의 element를 포함하는 Observable Sequence

- success(value) 이벤트 또는 error 이벤트를 한 번만 방출합니다.

- success = next + completed 로 볼 수 있습니다.

- 즉, success가 발생하면 single은 종료됩니다

- 파일 저장, 파일 다운로드, 디스크에서 데이터 로딩같이, 기본적으로 값을 산출하는 비동기적 모든 연산에도 유용합니다.

- 사용 예시로, 응답/오류만 반환할 수 있는 HTTP 요청을 수행하는 데 사용되지만 단일요소를 사용하기 때문에 무한 스트림 요소가 아닌 단일 요소만 관리하는 경우에 사용할 수 있습니다.

# Completable

- completed 이벤트 또는 error 이벤트를 방출

- 어느 element도 방출하지 않고 에러나 완료만 가능한 Observable의 변형

- 어떠한 operation의 성공적인 완료여부만 알고싶을 경우 사용할 수 있습니다.

- Single, Maybe와 다르게 Observable을 Completable로 바꿀 수 없습니다.

----------------- 
# RxCocoa Traits

# Driver vs Signal


* UI 레이어에 reactive 코드를 작성하는 직관적인 방법을 제공하거나 애플리케이션에서 데이터 스트림을 모델링하는 모든 경우를 위한 것.
* UI 레이어 계의 PublishSubject와 BehaviorSubject 라고도 불린다.

- 에러를 발생시키지 않는다.

- 메인 스케줄러에서 동작하며, 사이드 이펙트를 공유하는 특성을 지녔다.

- Signal은 새로운 구독자에게 replay 해주지 않는다.
   (Driver 처럼 구독하는 순간 초기값이나 최신값을 주지 않는다. 구독한 이후에 발행되는 값을 받음. 위의 사진 참고)

- Signal은 emit함수로 이벤트 처리 / Driver는 drive함수로 이벤트 처리 
