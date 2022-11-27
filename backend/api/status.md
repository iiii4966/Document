# Status code

## 200 OK
- API 정상 처리
- 일반적인 API 성공 처리

## 201 Created
- POST method
- 리소스 생성 성공

## 202 Accepted
- 요청 처리중, 완료되지 않음
- 비동기 처리 시

## 204 No Content
- 요청 처리 완료, 응답 없음
- 리소스 삭제, 수정 시

## 301 Move Permanently
- 요청 된 리소스가 Location header 에 설정된 URL 로 이동했다는 것을 알림
- 이후 브라우저에 따라 캐시 적용

## 302 Found
- 301 과 동일하나 임시 이동

## 304 Not Modified
- 캐시된 리소스를 재사용하기

## 400 Bad Request
- 클라이언트의 잘못된 요청

## 401 Unauthorized
- 인증 실패
- 만료, 유효하지 않은 토큰, 로그인 필요

## 403 Forbidden
- 인증은 되었으나 리소스에 접근 권한 없음

## 404 Not Found
- 요청한 리소스 없음

## 405 Method Not Allowed
- 허용되지 않는 리소스 요청

## 406 Not Acceptable
- Accept, Accept-Encoding, Accept-Language 에 설정된 값을 서버에서 처리할 수 없음

## 408 Request Timeout
- 사용되지 않는 커넥션 종료

## 409 Conflict
- 요청한 리소스 상태 충돌

## 429 Too Many Requests
- 제한된 리소스 요청 초과

## 500 Internal Server Error
- 서버에서 처리하지 못한 에러

## 502 Bad Gateway
- gateway, proxy 에서 서버 연결 실패

## 503 Service Unavailable
- 서버 점검 이유로 이용할 수 없음

