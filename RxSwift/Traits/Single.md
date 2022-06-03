
# Single

- 1개의 element를 포함하는 Observable Sequence

- success(value) 이벤트 또는 error 이벤트를 한 번만 방출합니다.

- success = next + completed 로 볼 수 있습니다.

- 즉, success가 발생하면 single은 종료됩니다

- 파일 저장, 파일 다운로드, 디스크에서 데이터 로딩같이, 기본적으로 값을 산출하는 비동기적 모든 연산에도 유용합니다.

- 사용 예시로, 응답/오류만 반환할 수 있는 HTTP 요청을 수행하는 데 사용되지만 단일요소를 사용하기 때문에 무한 스트림 요소가 아닌 단일 요소만 관리하는 경우에 사용할 수 있습니다.

