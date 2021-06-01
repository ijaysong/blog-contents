# Http
생활코딩 Http 강의,
인프런 '모든 개발자를 위한 HTTP 웹 기본 지식' 강의를 듣고!

## IP (인터넷 프로토콜)
인터넷 통신을 위해서 클라이언트와 서버는 각각 IP 주소를 가지고 있어야 한다.
인터넷 프로토콜은 IP 주소에 데이터를 전달하는 역할을 한다.
패킷(packet)이라는 통신 단위로 데이터를 전달한다.

### IP 패킷
IP 패킷에는 규칙이 있다.
보내고자 하는 데이터를 감싸는 바깥쪽에 출발지 IP와 도착지 IP, 기타 등등의 정보를 적어야 한다. 
패킷을 인터넷 통신망에 던지면, 노드는 패킷에 적혀있는 도착지 IP를 보고 해당 위치로 찾아간다.
서버에 도착한 뒤, 메세지를 받았다는 응답을 담은 새로운 패킷을 만들어서 되돌려준다.

### IP 프로토콜의 한계
* 비연결성
- 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송하고 이를 전혀 알지 못함.
- 대상 서버가 패킷을 받을 수 있는 상태인지 모름.
- ex) 편지를 보냈는데 해당 주소에 받을 사람이 살지 않음.

* 비신뢰성
- 패킷이 소실될 가능성이 있다. 중간에 패킷이 사라질 가능성이 있음.
- 패킷이 전송되는 중간에 특정 노드가 꺼져있거나 하면 소실 될 수 있는데 패킷이 소실되어도 이를 알지 못한다.
- ex) 광케이블을 야생동물이 끊어먹었다던지, 해저 케이블이 끊겼다던지...

- 패킷 전달 순서 문제가 발생한다. 패킷이 순서대로 안오는 경우가 있다.
- ex) 1번 패킷 : Hello, 2번 패킷 : world
- 1, 2번 패킷을 순서대로 전달해도 다른 경로로 노드를 거쳐 목적지 서버에 도착하기 때문에 
- 나의 의도와는 다르게 2번째 노드가 먼저 도착하는 경우가 있다.

프로토콜 만으로는 위와 같은 문제를 해결할 수 없다.
그래서 나온 것이 TCP/IP이다.

## TCP UDP


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


### Status Line
서버가 동작을 잘했는지, 안됐는지, 안됐다면 왜 안됐는지 등을 표시한다.
{Version} {status code} {phrase}를 표시한다.
ex) HTTP/1.1 200 OK

100번대 : 정보
200번대 : 성공
300번대 : Redirection(웹 브라우저가 다른 곳으로 바로 이동하는 것)
400번대 : 클라이언트 에러
500번대 : 서버 에러

### Response Headers
* Content-Type: 웹서버가 응답할 때 해당 양식으로 반환
* Content-Length : 컨텐츠의 사이즈(byte)
* Content-Encoding : 컨텐츠의 압축을 풀려면 해당 포맷으로
* Last-Modified : 해당 컨텐츠가 언제 마지막으로 수정되었는지 표시

## 관련 토픽
### HTTPS
HTTPS의 S는 Secure의 약자로, 안전한 이라는 뜻이다.
HTTP가 처음 나왔을 때는 그렇게 위험하지 않았다.
웹을 통해서 심각한 정보를 다루지 않았기 때문!

군사, 금융, 사생활을 웹을 통해서 주고 받고 있다.
오늘날과 같은 시대에 HTTP를 사용하면 누군가가 내 정보를 들여다 보고 있다고 생각해야 한다.
반면에 HTTPS는 외부에서 가로챈다고 한들, 내부 내용이 암호화 되어 있기 때문에 훔쳐볼 수 없다.

### Cache
어떠한 웹 페이지에 접속 할 때, 매회 다운 받지 않고 어딘가에 저장해두었다가 활용함으로서 웹의 성능을 높이는 기능이다. 
웹은 캐쉬가 새롭게 갱신되었더라도 이를 알아채지 못하는 단점이 있다.
cf) 다음은 강제로 캐쉬를 갱신하는 단축키이다.
- Windows : Ctrl + F5
- MacOS : Cmd + R
- Linux : F5

헤더에 cache-control, pragma 등을 지정함으로서 캐쉬와 관련해 제어할 수 있다.

### 쿠키
쿠키에 값을 설정해 놓음으로서 개인화를 가능하게 해준다.
쿠키값에 저장되어 있는 것을 서버에 전송함으로서 사용자의 상태를 유지하고, 사용자를 식별할 수 있다.
ex)
다음에 접속할 때에 자동 로그인.
로그인 하면 장바구니에 전에 내가 담아왔던 물건이 보임.

### 웹 스토리지
최근에는 쿠키보다 더 많은 정보를 저장할 수 있으면서, 보안에서도 더욱 우수한 웹 스토리지가 생겨났다.

### proxy
웹 서버와 웹 브라우저 사이에 중계서버라고 하는 프록시가 있다.
중간에 있는 서버가 캐쉬를 대신 해주거나, 보안과 관련한 기능을 대신 해주거나, 적당히 분산하여 여러 대의 서버가 기능을 담당하는 것과 같은 역할을 프록시 서버가 대신 해준다.

### Developer tools > Network
네트워크 모니터링 기능.

### Wire Shark
무료 오픈소스.
컴퓨터에서 일어나는 모든 네트워크 트래픽을 다 확인할 수 있음.