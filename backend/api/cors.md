# CORS

- CORS 를 처리하기 위해 preflight 요청에 대비하자.
    - Origin request header 값, Access-Control-Allow-Origin 설정
    - Access-Control-Request-Method 허용
        - GET, POST, OPTION
- CORS 처리를 위해 잘 구현된 라이브러리가 존재한다면, 라이브리러를 사용하자
- Preflight 요청을 억제하자.
    - Simple request - 헤더에 Accept, Accept-Language, Content-Language 만 포함되는 GET, OPTION, POST 요청
    - POST 요청의 경우 Content-Type 헤더도 허용되지만 해당 값이 "application/x-www-form-urlencoded", "multipart/form-data" 또는 "text/plain"인 경우
    - Preflight 요청(OPTIONS 메서드를 사용하고 Access-Control-Request-Method header 포함)이라면
        - Simple Request Header 외 헤더 허용하기
        - Header 제한이 없다면 유저가 요청한 Header 그대로 반환하기
        - 유저가 요청한 Method, Access-Control-Allow-Methods 에 추가하기
- Preflight 요청이 유효한 시간을 설정하여 캐싱하자.
    - Access-Control-Max-Age 설정
    - 2592000(30일)과 같은 큰 값을 사용하는 것이 일반적이지만 많은 브라우저가 훨씬 더 낮은 제한을 자체적으로 적용하고 있다.