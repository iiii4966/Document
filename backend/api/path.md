# API Path

- API endpoint 는 가능한 명사를 사용하자.
    - **POST /v1/createPost `X`**
    - **POST /v1/posts `O`**
- API 리소스 사이에 관계를 표현하기 위해 nested resource path 를 사용하자.
    - **/posts/{postId}/comments**
- 가능한 리소스 고유 식별자를 통일하자. 별다른 이유가 없다면 DB primary key 로 설정하자.
    - **api/v1/posts/{postId}**
    - **api/v1/members/{memberId}**
- resource path 는 복수형을 사용하자.
    - **POST /v1/posts**