# Cookie
- 서버에서 읽기 목적으로 사용되는 브라우저 데이터 저장소

```http
HTTP/2.0 200 OK
Content-Type: application/json
Set-Cookie: cookie=choco
```

| Browser	| Cookie count limit per domain	| Total size of cookies |
| --- | --- | --- |
| Chrome | 180 | 4096 |
| Firefox |	150 |	4097 |
| Opera |	60	| 4096 |
| Safari |	600	| 4093 |

## Options

#### path
- Cookie 전송 가능한 URL 경로
- / 만 쓸 경우에 모든 하위 디렉토리 포함
```http
Set-Cookie: id=a3fWa; path=/;
```

#### httpOnly
- 서버사이드에서만 설정이 가능한 쿠키를 의미
- document.cookie API를 통해 접근 불가
```http
Set-Cookie: id=a3fWa; secure; httponly
```

#### secure
- https protocol 에서만 전송 가능한 쿠키
```http
Set-Cookie: id=a3fWa; secure;
```

#### domain
- 쿠키를 전송할 수 있는 서버 도메인
- 도메인을 설정하지 않으면 기본값은 쿠키를 설정한 서버 도메인
  - 서버 도메인이 https://api.example.com 이라면 쿠키 도메인 -> example.com 
  - 도메인을 설정하지 않으면 origin 도메인만 쿠키 전송 가능.
    - example.com 쿠키 전송 가능
    - www.example.com 서브 도메인 쿠키 전송 불가 
- 도메인 설정시 서브 도메인 모두 전송 가능
  - example.com 설정 시 쿠키 전송 가능 도메인
    - example.com
    - www.example.com 
    - www.abc.example.com
  - 불가 도메인
    - google.com
    - example.co.kr 

#### sameSite
- same, cross-site 기준 쿠키를 저장, 전송할 수 있는 기준
- CSRF 요청 보호 목적
- cross-site 판별 기준
  1. public suffix, registrable domain 기준
    - public suffix
        - 공용 레지스트리에 의해 관리되는 도메인 (https://publicsuffix.org)
        - example.com의 public suffix -> com (TLD)
        - example.github.io 의 public suffix -> github.io
    - registrable domain
        - public suffix 포함 '.' 좌측에 위치한 도메인
        - example.com 의 registrable domain -> example.com
    - public suffix, registrable domain 이 같으면 same-site, 둘 중 하나라도 다르면 cross-site
  2. scheme, host, port 기준
      - scheme이 다를 경우 cross-site 요청
        - client scheme 이 http 이고 서버와의 통신은 https 라면 cross-site 요청 
      - host 는 1번 항목과 동일
        - example.com 과 www.example.com 간 요청은 same-site 
        - example.github.io 는 github.io 가 public suffix 이므로
          - www.example.github.io 간 요청은 same-site
          - abc.github.io 간 요청은 cross-site
      - port 가 다른 경우 cross-site 요청, 같으면 same-site 요청
- 설정 값
  - strict
    - cross-site 요청 시 쿠키 전송 불가
    - same-site 요청, origin 에만 쿠키 전송 가능
  - lax
    - strict 와 동일하나 cross-site 요청이면서 third-party 쿠키라면 아래의 경우 전송 가능
      - Top Level Navigation
      - window.location.replace 등으로 인해 자동으로 이뤄지는 navigation
      - 302 리다이렉트를 이용한 navigation
      - 안전한 메서드 요청 (GET, HEAD, OPTIONS, TRACE)
    - 기본값
  - none
    - cross-site, same-site 모두 쿠키 전송 가능
    - secure 옵션을 설정하지 않으면 쿠키 설정, 전송 불가
```http
Set-Cookie: mykey=myvalue; samesite=lax
```

#### expires / max-age
- expires 는 만료 일시 지정 
```http
Set-Cookie: id=a3fWa; expires=Thu, 31 Oct 2021 07:28:00 GMT;
```

- max-age 는 쿠키가 유효한 시간(s)
```http
Set-Cookie: id=a3fWa; max-age=86400;
```
- Session Cookie
  - 브라우저를 닫으면 삭제되는 쿠키
  - Expires, Max-Age 를 설정하지 않은 Cookie
- Permanent Cookie
  - Expires 나 Max-Age 에 지정한 값에 특정된 시점에 삭제되는 쿠키
  - 해당 시점 전까지 삭제되지 않고 보존
- Expires와 Max-Age 속성이 둘 다 설정 된 경우, Max-Age가 우선권을 갖음
- IE6, 7, 8 은 max-age 를 지원하지 않음
