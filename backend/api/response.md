# API Response

- 응답 포맷으로 JSON 을 사용하자.
    - **Content-Type = application/json;**
- API 응답 포맷을 통일하자.  
    **Success**

    ```json
    {
        "code": "0",
        "message": "Success",
        "data": {"name": "lim gapgi"},
    }
    ```

    **Error**

    ```json
    {
        "code": "40001",
        "message": "Expired token"
        "data": {
            "details": [
                {
            "code": "NullValue",
            "target": "PhoneNumber",
            "message": "Phone number must not be null"
            },
            ],
            "innerError": {
                "trace": "",
            }
        },
    }
    ```
    - code
        - 응답 상태 코드 정보
        - string type
        - 정상적으로 요청이 처리된 경우 → `0` 또는 `OK`
        - 에러가 발생한 경우 → `40001` 또는 `TOKEN_EXPIRED`
    - message
        - 응답 상태 상세 메시지
        - string type
        - 디버깅 및 로깅 목적 메시지
        - 사용자에게 노출되는 메시지가 아니어야 한다.
        - 사용자 언어별로 제공하지 않는다.
    - data
        - 응답 데이터
        - 요청 성공 시 리소스 데이터, API 성공 처리 여부, 반환값이 없는 경우 null 반환
        - 요청 실패 시 에러 상세 메시지, 개발환경에서만 확인 가능한 에러 정보 반환
- framework 에서 제공되는 응답 형식이 존재한다면 해당 형식을 사용하자.
- API 응답으로 Datetime format 데이터를 제공하는 경우 ISO 8601 UTC 형식을 사용하자.
    - Datetime - 2020-11-16T04:25:03Z
    - Date - 2020-11-16
    - Time / Interval - 04:30:00