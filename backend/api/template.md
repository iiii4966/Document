# API Template
###### API 설계 효율화를 위해 template

## Summary
###### API 기능, 목적을 간략히 설명

## Path
###### API 실행 경로
- method: POST
- host: https://site.co.kr
- path: /api/v1/posts

## Authentication
###### API 인증 방식
- method: COOKIE  
- value: server encrypted token

## Permission
###### API 사용 권한 / 서비스별 인증 권한, 인증방식
- 

## Query parameter
###### GET 요청의 경우 쿼리 파라미터 정보
| key | type | required | default | constraint | example |
| --- | --- | --- | --- | --- | --- |
| name | string | x | x | x | james |

## Request body
###### POST, PATCH, PUT, DELETE 요청의 경우 요청 데이터 정보
Content-Type = multipart/form-data

| field | type | required | default | description |
| --- | --- | --- | --- | --- |
| content | string | o | empty string | 포스트 내용 |
| image | file | x | x | 포스트 이미지 |

## Response body
###### API 성공 응답 데이터
Content-Type = application/json

| field | type | nullable | description | example |
| --- | --- | --- | --- | --- |
| content | string | x | 포스트 내용 | Hello world! |
| createdAt | datetime | x | 작성일시 | 2022-10-10T00:00:00Z |

## Exception response
###### API 에러 응답
Status code = 401
Content-Type = application/json

| field | type | value |
| --- | --- | --- |
| code | string | NOT_AUTHENTICATED |
| message | string | Invalid access token |

## Execution
###### API 를 바로 호출해볼 수 있는 명령어 집합
```bash
> curl -i -H "Accept: application/json" --cookie "acc=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibWJFbWFpdCI6IaskbWluQGJyZWFrLmNvLmtyIiwiaWF0IjoxNTE2MjM5MDIyfQ.8WaEO0lUKenb2x0FV-0iKIdjvu2Q_FDzZGthp5RkTxc" -X POST https://site.co.kr/api/v1/posts
```