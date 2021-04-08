# Http
생활코딩 Http 강의를 듣고!

## Http 소개
HTTP(HyperText Transfer Protocol)란
웹브라우저와 웹서버가 컨텐츠(html, 이미지, 오디오, css, javascript 파일등)을 주고 받기 위해서 사용하는 통신규칙이다.
간단히 말해서 서버와 클라이언트가 서로 주고 받는 Request와 Response를 이해할 수 있는 메세지를 말한다.

HTTP는 추상적인 개념이지만,
크롬의 Developer tools를 사용하면 네트워크 탭에서 웹 서버가 통신하는 내용을 볼 수 있다. (네트워크 로그)

서버와 클라이언트는 다음과 같은 형식으로 헤더에 정보를 담아 요청/응답한다.
브라우저는 해당 내용을 뿌려주는 역할을 한다.

### Request
* Request Headers : Client가 Server에 요청한 내용
* View Source : 요청한 내용을 자세히 볼 수 있음

### Response
* Response Headers : Server가 Client에 응답한 내용
* HTTP/1.1 : Response Header의 제일 처음에는 이렇게 적혀있다. 해당 방식으로 통신할 것을 기재한 것.
* 200 OK : Response 상태
* Content-Length : 응답 내용의 길이
* Content-Type: text/html :해당 타입의 내용을 반환하겠다는 것