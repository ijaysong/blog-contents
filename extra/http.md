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

## HTTP Request message

### HTTP Request Format
Request Header의 형식은 다음과 같다.
~~~
// Request Line
GET /doc/test.html HTTP/1.1
// Request Headers
Host : test01.com
Accept: image/gif, image/jpeg, */*
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0
Content-Length: 35

// RequestMessage Body
bookId=12345&author=Hong+gildong
~~~

* Request Message Header = Request Line + Request Headers
* Request Message Header와 RequestMessage Body 사이에 한줄을 띄워 header와 body를 구분한다.

### Request Line
* GET : Request 메소드의 하나이다. GET 이외에 POST, PUT, DELETE 등이 있다.
* /doc/test.html : 웹서버에게 요청하는 정보이다.
* HTTP/1.1 : 웹 서버가 현재 사용하고 있고, 사용할 수 있는 HTTP 버전을 말한다.

### Request Header
* Host : 컴퓨터 한대 한대를 식별하는 정보이다. 접속하고자 하는 웹 서버의 주소라고 보면 된다.
* User Agent : 웹 브라우저의 다른 표현이다. 요청하는 웹 브라우저가 무엇인지를 말한다.
ex) 로봇으로 접속했다거나 하는 특정 방식으로 접속하는 것을 차단하는 용도로 사용 된다. 
* Accept-encoding : 통신하는 데이터 양이 많아 압축을 해서 전송하면, 웹 브라우저에서 압축을 풀어서 해석 할 수도 있다.
압축해서 보냄으로서 네트워크의 자원을 아낄 수 있다.
해당 브라우저는 어떠한 압축 방식을 지원한다 라는 정보를 표현하고 있다.
* If-Modified-Since : 웹 서버에 요청한 데이터를 요청 할 때마다 다운 받으면 비효율적이므로, 해당 정보를 웹 서버에 보내면
내가 해당 파일을 언제 다운 받았다는 정보를 전달하게 된다.
그러면 웹 서버는 자신이 가지고 있는 데이터와 비교해서 어떤 것이 더 최신인지 비교해서 더 최신이면 데이터를 다운 받고, 아니면 받지 않는다.
이를 통해 속도가 더 빨라질 수 있다.

## HTTP Response message

### HTTP Response Format
Response Header의 형식은 다음과 같다.
~~~
// Status Line
HTTP/1.1 200 OK
// Response Headers
Date: Sun, 08 Feb xxxx 01:11:12 GMT
Server: Apache/1.3.29 (Win32)
Last-Modified: Sat, 07 Feb xxxx
ETag: "0-23-4024c3a5"
Accept-Ranges: bytes
Content-Length: 35
Connection: close
Content-type: text/html

// Response Message Body
<h1>My Home Page</h1>
~~~

* Response Message Header = Status Line + Response Headers
* Response Message Header와 ResponseMessage Body 사이에 한줄을 띄워 header와 body를 구분한다.

