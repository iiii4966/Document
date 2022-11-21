# API Async Operation

- 처리하는데 장시간이 걸리는 API 는 비동기로 처리하자.
- 단, 비동기 요청 처리에 대한 응답은 동기로 제공하지 않고 상태 확인 가능한 API 를 제공하자.
- 상태 확인 API 는 아래 데이터를 제공하자.
    - 최초 요청 시간
    - operation 상태
        - NotStarted
        - Running
        - Succeeded. Terminal State.
        - Failed. Terminal State.
        - Cancelled
        - Partially Completed
    - 각 상태로 진입한 시간
    - 완료 예상 시간
- 비동기 처리에 대해서 가능한 취소 기능을 제공하자.
- 비동기 처리 완료 시 가능하다면 알림 기능을 제공하자.