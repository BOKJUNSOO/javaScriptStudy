## AJAX (Asynchronous JavaScript And Xml)

`AJAX` 는 단순히 얘기하자면 서버와 통신하는 방법이다. 웹소켓과 같은 서버 통신의 방법도 존재한다.

`AJAX` 에는 4가지 방식 정도가 있다.
- `old api`
- `jQuery`
- `Axios`
- `New api - fetch`

### backEnd(Server) <-> FrontEnd(Client)

클라이언트와 서버가 통신을 할때 클라이언트가 `요청(Request)` 하면 서버는 이에 `응답(Response)`를 한다.

이때 요청에는 크게 두가지 `GET,POST` 방식이 있으며 `PUT`과`DELETE` 방식도 존재하지만 잘 사용하지 않는다.

이에 반드시 `GET`방식을 써야하는 경우`POST`를 써야만 하는 경우가 존재한다.

- 요청 데이터의 형태는 3가지이다. 이 형태를 맞춰서 요청을 해야 백엔드에서 처리할 수 있다.
  -  `?`를 시작으로한 `Query Parameter`
  -  `JS FormData` 생성
  -  `JSON 문자열` 생성

응답 방식에는 여러가지 방식이 존재한다 `JSON, HTML, ...`