# API Versioning

- API versioning 을 제공하자.
- API versioning 방식은 여러개가 있다. 별다른 이유가 없다면 path versioning 을 사용하자.
    - path versioning - `/v1/api`
    - header versioning - `X-API-VERSION=1.0`
    - query parameter versioning - `/api?api-version=1.0`
- API version 은 다음의 경우 올릴 수 있다.
    - API, 요청 파라미터 이름이 변경되거나 삭제된 경우
    - API 기능, 동작방식이 변경된 경우
    - 잘못된 정보, 에러 코드가 변경되는 경우
    - [Principle of Least Astonishment](http://en.wikipedia.org/wiki/Principle_of_least_astonishment) 을 위반하는 경우
- 하위 호환을 유지할 수 있는 변경은 API version 을 올리지 않아도 된다.
    - request data 추가
    - request data 기본값 설정
- 하위 버전의 API 는 상위 버전 배포, 연동 후 사용하지 않는 것을 확인해서 제거하자.