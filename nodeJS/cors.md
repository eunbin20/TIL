# CORS

브라우저는 기본적으로 동일 출처 정책(SOP:Same Origin Resource)를 지키기 때문에 다른 출처의 리소스 접근을 금지한다. 이를 통해 XSS나 XSRF 등의 보안 취약점을 노린 공격을 방어할 수 있다. 그러나 실제로 웹페이지에서는 다른 출처에 대한 리소스에 접근해야 하는 경우는 꽤 많다.

예를 들어 http://localhost:3000이라는 도메인 주소를 사용하는 웹페이지에서 http://localhost:8000이라는 api서버로 데이터를 요청한다면 이것은 동일 출처 정책을 위반한 것이다.

이때 이러한 다른 출처에 대해 리소스 공유를 가능하게 하는 것이 cors이다. 다른 출처의 리소스를 불러오려면 그 출처에서 올바른 cors 헤더를 포함한 응답을 반환해야 한다.

### 출처(origin)
출처는 protocol, host, port를 합친 것을 의미한다.

`http://localhost.com` 와 같은 출처라고 할 수 있는 것들은 다음과 같다.

- `http://localhost:80`
  80번 포트는 localhost의 기본 포트번호이다.
- `http://localhost/posts/create`
  /post/create는 location에 대한 정보로, 출처와는 무관하다.
