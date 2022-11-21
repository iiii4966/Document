# API Collection

- filtering, sorting, pagination 기능을 제공하자.
- framework, library 기능을 활용하자.
- filtering, sorting, pagination 기능이 모두 제공되어 사용하는 경우 filtering → sorting → pagination 순으로 로직을 처리하자.

## Pagination

- pageSize 는 서비스에 적합한 기본 사이즈를 제공하자.
- pageSize 는 기본값은 가능한 작게 설정하자.
- 서버에서 설정한  pageSize 보다 큰 값을 제공하는 경우 기본값으로 설정된 데이터만 반환하자.
- Collection 총 갯수를 반환하자.
    ```json
    "count": 100
    ```
- Collection 총 갯수가 필요하지 않다면 query parameter 로 옵션을 제공하자.
    ```
    ?count=false
    ```
- 다양한 pagination option 을 검토하자.
    - Offset pagination
        - GET /items?limit=20&offset=100 
    - Cursor pagination
        - GET /items?limit=20&cursor=bNAtbMNgl3wbg

## Sorting

- 기본 sorting 제공하여 항상 일관된 정렬 데이터를 제공하자.
- 정렬 방식, 정렬 대상 속성을 선택가능하도록 Query parameter 로 기능을 제공하자.
    ```
    sort=createdAt:desc
    sort=id:desc&sort=createdAt:asc
    ```

## Filtering

- filter 속성은 다음을 준수하자.
    - filtering 대상
    - filtering 조건
    - filtering 값
- 위 기준을 바탕으로 Query parameter 로 기능을 제공하자.
    ```
    price:gte=10000&price:lte=50000
    ```