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
### 인터넷 프로토콜 스택의 4계층
- 애플리케이션 계층 : HTTP, FTP
- 전송 계층 : TCP, UDP
- 인터넷 계층 : IP
- 네트워크 인터페이스 계층

## 프로토콜 계층
| 계층 | 장치 |
|-----|-----|
| 애플리케이션 | 웹 브라우저, 네트워크 게임, 채팅 프로그램 |
| | SOCKET 라이브러리 |
| OS | TCP |
| | IP (Internet Protocol) |
| 네트워크 인터페이스 | LAN 드라이버 |
| | LAN 장비 |

ex)
프로그램이 Hello, world! 라는 메세지를 클라이언트로 전송한다고 해보자.

1. 애플리케이션에서 메세지를 생성한다.
2. SOCKET 라이브러리를 통해서 메세지를 전달한다.
3. OS의 TCP에서 메세지를 TCP 정보로 한번 감싼다. (TCP 정보 생성, 메세지 데이터 포함)
4. IP에서 IP정보로 한번 더 감싼다. (IP 패킷 생성, TCP 데이터 포함)
5. 네트워크 인터페이스에서 LAN 카드를 통해서 나갈때 이더넷 프레임으로 한번더 감싼다. ()
6. 인터넷을 통해 서버로 전달된다.

#### 패킷이란?
패킷은 패키지(package; 수화물)과 버킷(Bucket; 덩어리)의 합성어이다.
택배 박스에 데이터를 넣는 것과 같은 이미지로 생각해보자.

### IP 패킷
출발지 IP, 목적지 IP, 기타...

### TCP 세그먼트
출발지 PORT, 목적지 PORT, 전송제어, 순서, 검증 정보...
(IP 프로토콜만으로 해결이 되지 않았던 것이 TCP 세그먼트의 전송제어로 인해 해결된다.)

### TCP 특징
전송제어 프로토콜(Transmission Control Protocol)

- 연결지향: TCP 3 way handshake (가상연결)
ex)
- SYN: 접속 요청 
- ACK: 요청 수락

TCP는 세번의 과정을 거쳐서 클라이언트와 서버와의 연결을 확인한다.
1. 클라이언트가 서버에게 접속 요청을 한다. (SYN)
2. 서버는 요청을 수락하며 접속 요청을 보낸다. (SYN + ACK)
3. 클라이언트는 서버에게 요청 수락을 보낸다. (ACK)
4. 데이터 전송
단점은 시간이 오래걸리고 TCP 세그먼트의 데이터를 다 담으면 용량이 커진다.
   
- 데이터 전달 보증
클라이언트에서 서버로 데이터를 보냈을 때, 서버는 클라이언트에게 잘 받았다고 결과를 보내줌.

- 순서 보장
ex) 클라이언트가 1, 2, 3번 패킷을 순서대로 보낸다고 해보자.
서버에서 1, 3, 2번의 순서대로 패킷을 받았다.
그러면 서버는 두번째 패킷부터 잘못 왔으니까 다시 보내달라고 한다. 
(TCP에는 전송제어 정보가 포함되어 있으므로 그것을 참고로 순서를 파악하는 것!)
그러면 클라이언트는 두번째 패킷부터 다시 보낸다.

- 신뢰할 수 있는 프로토콜
- 현재는 대부분 TCP 사용

### UDP 특징
사용자 데이터그램 프로토콜(User Datagram Protocol)

- 하얀 도화지에 비유(기능이 거의 없음)
- 연결지향: TCP 3 way handshake (가상연결)
- 데이터 전달 보증 X
- 순서 보장 X
- 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
- IP와 거의 같지만 PORT 체크섬 정도만 추가되었다.
- 애플리케이션에서 추가 작업이 필요하다.
- HTTP3가 등장하면서 3 way handshaking을 없애보자는 흐름이 생겨나며 UDP가 각광받고 있음.

#### 포트란?
하나의 IP에서 여러 애플리케이션이 사용하기 위해

## URI

Uniform: 리소스 식별하는 통일된 방식
Resource: 자원, URI로 식별할 수 있는 모든 것(제한 없음)
Idendifier: 다른 항목과 구분하는데 필요한 정보

리소스 식별자 URI는 로케이터(locator) 또는 이름(name) 크게 두가지로 분류될 수 있다.

- URL(Resource Locator) : 리소스의 위치
- URN(Resource Name) : 리소스의 이름

### URL

Uniform Resource Locator : 리소스가 있는 위치를 지정

ex)
foo://example.com:8042/over/there?name=ferret#nose

### URN

Uniform Resource Name : 리소스에 이름을 부여
위치는 변할 수 있지만, 이름은 변하지 않는다.

ex)
urn:example:animal:ferret:nose

URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음.
(URN으로 리소스를 찾을 수 없다고 보면 됨. 거의 사용 X)
ex)
urn:isbn:8960777331 (어떤 책의 isbn URN)

=> 그렇기 때문에 URI와 URL을 같은 의미로 봐도 무방하다.

### URL 전체 문법

- scheme://[userinfo@]host[:port][/path][?query][#fragment]
- https://www.google.com:443/search?q=hello&hl=ko

* https: 프로토콜
* www.google.com : 호스트 명
* 443 : 포트번호
* /search : 패스
* q=hello&hl=ko : 쿼리 파라미터

#### 스키마 (schema)

- 스키마는 주로 프로토콜을 사용
- 프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
 ex) http, https, ftp 등등
- http는 80 포트, https는 443 포트를 주로 사용, 포트는 생략 가능
- https는 http에 보안 추가 (HTTP Secure)

#### userinfo

- URL에 사용자 정보를 포함해서 인증할 때 사용
- 거의 사용하지 않음

#### 호스트 (host)

- 도메인 명 or IP 주소를 직접 사용 가능

#### 포트 (port)

- 포트는 생략 가능하다.
- 일반적으로 생략하며, 생략 시 http는 80, https는 443

#### 패스 (path)

- 리소스 경로이다.
- 계층적 구조로 되어 있다. (디렉토리처럼!)
 ex)
 /home/file1.jpg
 /members
 /members/100, /items/iphone12

#### 쿼리 (query)

- key=value의 형태.
- ?로 시작, &로 추가 가능
 ex)
 ?keyA=valueA&keyB=valueB
- query parameter, query string 등으로 불림.
 (숫자가 파라미터로 지정이 되어도 다 string으로 넘어가기 때문에 query string이라고 부름)
- 웹 서버에 제공하는 파라미터로 문자 형태.

#### 프레그먼트(fragment)

ex)
https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html#getting-started-introducing-spring-boot

- 웹 페이지 내부에서 특정 위치로 이동하는 북마크를 이용할 때
- html 내부 북마크 등에 사용
- 서버에 전송하는 정보 아님

## 웹 브라우저 요청 흐름

ex)
https://www.google.com:443/search?q=hello&hl=ko 에 접속해본다고 하자.

1. www.google.com의 DNS 서버를 조회하여 IP 주소를 알아낸다. (HTTPS PORT는 생략)
2. 애플리케이션 계층의 웹 브라우저가 HTTP 요청 메세지 생성
  ex)

~~~
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
~~~

3. SOCKET 라이브러리를 통해 전달
4. OS 계층의 TCP/IP로 데이터를 전달한다.
  TCP는 3 way handshake로 서버와 연결이 되어 있는지 확인을 한다.
  확인을 거치면 데이터에 패킷을 씌운다. (출발지, 목적지의 IP와 PORT, 전송제어, 순서)
5. 네트워크 계층을 통해서 LAN을 통해 서버로 데이터와 http 메세지, 패킷을 보낸다.
6. 서버에 요청이 잘 도착하면 HTTP 응답 메세지를 클라이언트에게 보내준다.
  ex)

~~~
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3423

<html>
 <body>...</body>
</html>
~~~

## Http 소개

HTTP(HyperText Transfer Protocol)는 HyperText 링크간에 연결이 가능한 html 전송을 목적으로 만들어졌다.
처음에는 html 전송을 위해 만들어졌지만, http 메세지에 거의 모든 형태의 데이터를 담아서 전송할 수 있게 되었다.

- HTML, TEXT
- IMAGE, 음성, 영상, 파일
- JSON, XML(API)
- 거의 모든 형태의 데이터 전송 가능
- 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용

웹브라우저와 웹서버가 컨텐츠(html, 이미지, 오디오, css, javascript 파일등)을 주고 받기 위해서 사용하는 통신규칙이다.
간단히 말해서 서버와 클라이언트가 서로 주고 받는 Request와 Response를 이해할 수 있는 메세지를 말한다.

HTTP는 추상적인 개념이지만,
크롬의 Developer tools를 사용하면 네트워크 탭에서 웹 서버가 통신하는 내용을 볼 수 있다. (네트워크 로그)

서버와 클라이언트는 다음과 같은 형식으로 헤더에 정보를 담아 요청/응답한다.
브라우저는 해당 내용을 뿌려주는 역할을 한다.

### HTTP 시작
1990년 팀 버너스 리와 그의 동료들이 web을 처음 내놓았다.
그때 당시 웹은 크게 4가지로 구성되어 있었다.

1. HTML
- 원하는 웹 페이지를 그림

2. URL, URI
- 원하는 웹 페이지에 방문할 수 있도록 해주는 주소체계

3. Web Borwser, Web Server
- 페이지를 주소 받는 소프트웨어

4. HTTP
- Web Borwser, Web Server가 서로 통신을 할 때 사용하는 통신 규약

그 중에서도 HTTP는 웹을 넘어서 인터넷의 근간이라고도 할 수 있다.

초기 HTTP는 매우 간단한 데이터만을 전달했지만,
웹이 발전함에 따라 보안이나 안정성 등의 문제가 대두되면서 발전을 거치며 보완을 거듭했고,
텍스트 뿐만 아니라 그림과 오디오, 영상까지도 전달할 수 있다.

### HTTP 역사

- HTTP/0.9 1991년 : GET 메서드만 지원, HTTP 헤더 X
- HTTP/1.0 1996년 : 메서드, 헤더 추가
- HTTP/1.1 1997년 : 가장 많이 사용, 우리에게 가장 중요한 버전
  - RFC2068 (1997) -> RFC2616(1999) -> RFC7230~7235(2014)
- HTTP/2 2015년 : 성능 개선
- HTTP/3 진행 중 : TCP 대신에 UDP 사용, 성능 개선

#### 기반 프로토콜

- TCP : HTTP/1.1, HTTP/2
- UDP : HTTP/3
  - 현재 HTTP/1.1 주로 사용
  - HTTP/2, HTTP/3도 점점 증가
  - TCP는 3 way handshaking 및 담고 있는 데이터의 양이 많아 처리 속도가 느린 알고리즘
  - 성능 개선의 목적으로 UDP 도입

### HTTP 특징

#### 클라이언트 서버 구조

- Request Response 구조
- 클라이언트는 서버에 요청을 보내고, 응답을 대기
- 서버가 요청에 대한 결과를 만들어서 응답

#### 무상태 프로토콜(stateless), 비연결성

- 서버가 클라이언트의 상태를 보존 X (stateless)
  문맥을 보전하지 않는 것.

ex)
stateful 과 stateless의 차이

1. stateful (상태 유지)
   고객 : 노트북 얼마인가요?
   점원 : 100만원 입니다. => 노트북 상태 유지

고객 : 2개 구매하겠습니다.
점원 : 200만원 입니다. 신용카드, 현금 중에 어떤 걸로 구매하시겠습니까? => 노트북, 2개 상태 유지

고객 : 신용카드로 구매하겠습니다.
점원 : 200만원 결제 되었습니다. => 노트북, 2개, 신용카드 상태 유지

2. stateful (상태 유지), 중간에 점원이 계속 바뀌면??
   고객 : 노트북 얼마인가요?
   점원A : 100만원 입니다.

고객 : 2개 구매하겠습니다.
점원B : 무엇을 2개 구매하시겠습니까?

고객 : 신용카드로 구매하겠습니다.
점원C : 어떤 제품을 몇개 신용카드로 구매하시겠습니까?

3. stateless (무상태)
   고객 : 노트북 얼마인가요?
   점원 : 100만원 입니다.

고객 : 노트북 2개 구매하겠습니다.
점원 : 200만원 입니다. 신용카드, 현금 중에 어떤 걸로 구매하시겠습니까?

고객 : 노트북 2개를 신용카드로 구매하겠습니다.
점원 : 200만원 결제 되었습니다.

4. stateless (무상태), 중간에 점원이 계속 바뀌면??
   고객 : 노트북 얼마인가요?
   점원 : 100만원 입니다.

고객 : 노트북 2개 구매하겠습니다.
점원 : 200만원 입니다. 신용카드, 현금 중에 어떤 걸로 구매하시겠습니까?

고객 : 노트북 2개를 신용카드로 구매하겠습니다.
점원 : 200만원 결제 되었습니다.

- 장점 : 서버 확장성 높음(scale out)
- 단점 : 클라이언트가 추가 데이터 전송

==> 차이점 정리

- stateful (상태유지)
  중간에 다른 점원으로 바뀌면 서비스에서 장애가 발생한다.
  다른 점원으로 바뀌면 context, 문맥이 바뀌기 때문에 다른 점원으로 바뀔 때 상태 정보를 다음 사람에게 미리 알려줘야 한다.
  항상 같은 서버가 유지되어야 한다.

- stateless (무상태)
  중간에 다른 점원으로 바뀌어도 된다.
  고객이 점원에게 필요한 정보를 그때그때 다 전달하기 때문에 중간에 점원이 바뀌어도 장애가 발생하지 않는다.
  갑자기 고객이 증가해도 점원을 대거 투입할 수 있다. (= 갑자기 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다.)
  => 무상태는 응답 서버를 쉽게 바꿀 수 있다! (무한한 서버 증설 가능!!)
  => scale out, 같은 기능을 하는 서버군을 여러개로 늘리는 수평 확장에 유리하다.

==> 실무 한계

- 모든 것을 무상태로 설계할 수 있는 경우도 있고, 없는 경우도 있다.
- 무상태 ex) 로그인이 필요 없는 단순한 서비스 소개 화면
- 상태유지 ex) 로그인
- 로그인한 사용자의 경우, 로그인 했다는 상태를 서버에 유지
- 일반적으로 브라우저 쿠키와 서버 세션 등을 사용해서 상태 유지
- 최대한 무상태로 개발하고, 상태 유지는 최소한만 사용
- 데이터를 너무 많이 보내는 단점이 있음.

#### 비 연결성 (connectionless)

ex) 연결을 유지하는 모델

1. 클라이언트 1에서 요청이 오면 서버는 응답을 한다.
2. 클라이언트 2에서 요청이 오면 서버는 응답을 한다. 클라이언트 1과 서버의 연결은 여전히 유지되어 있다.
3. 클라이언트 3에서 요청이 오면 서버는 응답을 한다. 클라이언트 1과 클라이언트 2, 서버의 연결은 여전히 유지되어 있다.

=> 서버는 연결을 계속 유지, 서버 자원 소모가 많다.

ex)

1. 클라이언트 1에서 요청이 오면 서버는 응답을 한다. TCP/IP 연결을 즉시 종료한다.
2. 클라이언트 2에서 요청이 오면 서버는 응답을 한다. TCP/IP 연결을 즉시 종료한다.
3. 클라이언트 3에서 요청이 오면 서버는 응답을 한다. TCP/IP 연결을 즉시 종료한다.

=> 서버는 연결 유지 X, 최소한의 자원을 유지한다.

##### 특징

- HTTP는 기본이 연결을 유지하지 않는 모델이다.
- 일반적으로 초 단위 이하의 빠른 속도로 응답
- 1시간 동안 수천 명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십 개 이하로 매우 작다.
 ex) 웹 브라우저에서 계속 연속해서 검색 버튼을 누르진 않는다.
- 서버 자원을 매우 효율적으로 사용할 수 있다.

##### 한계와 극복

- TCP/ IP 연결을 새로 맺어야 한다. 3 way handshake 시간 추가
- 웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트, CSS, 추가 이미지 등 수 많은 자원이 함께 다운로드
- 지금은 HTTP 지속 연결 (Persistent Connections)로 문제 해결
- HTTP/2, HTTP/3에서 더 많은 최적화

##### 서버 개발자들이 어려워하는 업무! stateless!!

- 같은 시간에 딱 맞추어 발생하는 대용량 트래픽
 ex) 선착순 이벤트 (저녁 6:00 선착순 1000명 치킨 할인 이벤트) / 명절 KTX 예약 / 학과 수업 등록
- 첫 화면에 로그인 등이 필요없는 단순 표시 페이지를 두어서 유저들이 해당 페이지에서 조금 머물다가 트래픽에 접속할 수 있도록 설계하면 여러명이 한번에 몰리는 것을 막을 수 있음

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

## HTTP Method

### API 설계

API를 짜는데 있어서 리소스를 식별(URI)하는 것이 가장 중요하다.

리소스의 의미는 무엇일까?

- 회원을 등록하고 수정하고 조회하는 것이 리소스가 아니다.
- 회원이라는 개념 자체가 바로 리소스이다.
- 등록, 수정, 조회의 행동을 제외하고 회원 리소스를 URI에 매핑한다.

URI는 리소스만 식별한다.
리소스와 해당 리소스를 대상으로 하는 행위를 분리한다.
행위는 Http 메서드로 표현한다.

- 리소스 : 회원
- 행위 : 조회, 등록, 삭제, 변경

| 기능           | 동작   | 리소스        |
| -------------- | ------ | ------------- |
| 회원 목록 조회 | GET    | /members      |
| 회원 조회      | GET    | /members/{id} |
| 회원 등록      | POST   | /members/{id} |
| 회원 수정      | PUT    | /members/{id} |
| 회원 삭제      | DELETE | /members/{id} |

### HTTP 메서드 종류

주요 메서드

- GET : 리소스 조회
- POST : 요청 데이터 처리, 주로 등록에 사용
- PUT : 리소스를 대체, 해당 리소스가 없다면 생성
- PATCH : 리소스 부분 변경
- DELETE : 리소스 삭제

기타 메서드

- HEAD : GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
- OPTIONS : 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명 (주로 CORS에서 사용)
- CONNECT : 대상 자원으로 식별되는 서버에 대한 터널을 설정
- TRACE : 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

### HTTP 메서드 - GET, POST

1. GET

- 리소스 조회
- 서버에 전달하고 싶은 데이처는 query(쿼리 파라미터, 쿼리 스트링)을 통해서 전달.
- 메세지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아 권장하지 않음.

2. POST

- 요청 데이터 처리
- 메시지 바디를 통해서 서버로 요청 데이터 전달
- 서버는 요청 데이터를 처리
- 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
- 주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용된다.

POST 요청 데이터를 어떻게 처리해야 할까?

- 대상 리소스가 리소스의 고유한 의미 체계에 따라 요청에 포함된 표현을 처리하도록 요청한다.
- 즉, 리소스 URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지 리소스마다 따로 정해야 한다. (정해진 것이 없음.)

POST는 저장의 기능만 하는 것이 아니다!

1. 새 리소스 생성(등록)

- 서버가 아직 식별하지 않은 새 리소스 생성

2. 요청 데이터 처리

- 단순히 데이터를 생성하거나, 변경하는 것을 넘어서 프로세스를 처리해야 하는 경우
 ex) 주문에서 결제완료 -> 배달 시작 -> 배달 완료 처럼 단순히 값 변경을 넘어 프로세스의 상태가 변경되는 경우
- POST의 결과로 새로운 리소스가 생성되지 않을 수도 있음
- 리소스로 URI를 표현하는데 한계가 존재한다. 그럴때 동사(컨트롤 URI)를 사용하여 구체적으로 표현하기도 한다.

ex) POST /orders/{orderId}/start-delivery (컨트롤 URI)

3. 다른 메서드로 처리하기가 애매한 경우
  ex) JSON으로 조회 데이터를 넘겨야 하는데, GET 메서드를 사용하기 어려운 경우
  애매하면 POST
  
### HTTP 메서드 - PUT, PATCH, DELETE

1. PUT

- 리소스를 대체 (완전히 대체)
 - 리소스가 있으면 대체
 - 리소스가 없으면 생성
 - 쉽게 이야기해서 덮어버림
   ex)
   서버에 저장된 데이터의 상태는 다음과 같다.

```
/members/100
{
 "username": "young",
 "age": 20
}
```

클라이언트에서 다음 내용으로 갱신을 하고자 한다.
(username 필드 없음)

```
PUT /members/100 HTTP/1.1
Content-Type: application/json
{
 "age": 50
}
```

클라이언트의 해당 API를 실행하면 서버에 기존에 저장되어 있던 내용은 삭제되고 전달 받은 데이터로 완전히 대체된다.

```
/members/100
{
 "age": 50
}
```

- 클라이언트가 리소스를 식별
 - 클라이언트가 리소스 위치를 알고 URI 지정
 - POST와 차이점
   ex)
   POST /members로 저장을 할 때, 저장을 하고 난 후, members의 id를 식별한다.
   POST는 전체 경로를 알지 못한다.
   PUT은 전체 경로를 안다는 점에서 POST와 다르다. (PUT의 경우에는 리소스를 식별하고 있다.)
   PUT /members/100

2. PATCH

- 리소스를 부분 변경한다.
- 일부 HTTP에서는 PATCH를 지원하지 않는 경우가 있는데, 이런 경우에는 POST를 사용하면 된다.
 ex)
 클라이언트에서 다음 내용으로 PATCH를 실행하면
 (username 필드 없음)

```
PATCH /members/100 HTTP/1.1
Content-Type: application/json
{
 "age": 50
}
```

서버의 데이터는 부분 변경된다.

```
/members/100
{
 "usernmae": "young"
 "age": 20
}
```

3. DELETE

- 리소스 제거

### HTTP 메서드의 속성

| HTTP 메소드 | 요청에 Body가 있음 | 응답에 Body가 있음 | 안전   | 멱등   | 캐시 가능 |
| ----------- | ------------------ | ------------------ | ------ | ------ | --------- |
| GET         | 아니오             | 예                 | 예     | 예     | 예        |
| HEAD        | 아니오             | 아니오             | 예     | 예     | 예        |
| POST        | 예                 | 예                 | 아니오 | 아니오 | 예        |
| PUT         | 예                 | 예                 | 아니오 | 예     | 아니오    |
| DELETE      | 아니오             | 예                 | 아니오 | 예     | 아니오    |
| CONNECT     | 예                 | 예                 | 아니오 | 아니오 | 아니오    |
| OPTIONS     | 선택사항           | 예                 | 예     | 예     | 아니오    |
| TRACE       | 아니오             | 예                 | 예     | 예     | 아니오    |
| PATCH       | 예                 | 예                 | 아니오 | 아니오 | 예        |

1. 안전 (Safe Methods)

- 호출해도 리소스를 변경하지 않는다.

2. 멱등 (Idempotent Methods)

- f(f(x)) = f(x)
- 한번 호출하든 두번 호출하든 100번 호출하든 결과가 똑같다.
- 멱등 메서드

 - GET : 한번 조회하든, 두번 조회하든 같은 결과가 조회된다.
 - PUT : 결과를 대체한다. 따라서 같은 요청을 여러번 해도 최종 결과는 같다. (기존에 있는 데이터를 삭제하고 완전 대체하기 때문)
 - DELETE : 결과를 삭제한다. 같은 요청을 여러번 해도 삭제된 결과는 똑같다.
 - POST : 멱등이 아니다!! 두번 호출하면 같은 결제가 중복해서 발생할 수 있다.

- 활용예시
 - 자동 복구 메커니즘
   ex) DELETE를 날렸는데 제대로 된 응답이 돌아오지 않아, 여러번 실행하는 경우 (멱등하기 때문에 여러번 실행해도 상관 없음)
 - 서버가 TIME OUT 등으로 정상 응답을 못 주었을 때, 클라이언트가 같은 요청을 다시 해도 되는지 판단이 되는 근거가 된다.

Q. 재요청 중간에 다른 곳에서 리소스를 변경해버리면?
사용자 1 : GET -> username: A, age: 20
사용자 2 : PUT -> username: A, age: 30
사용자 1 : GET -> username: A, age: 30 => 사용자 2의 영향으로 바뀐 데이터가 조회됨

==> 멱등은 외부 요인으로 중간에 리소스가 변경되는 것 까지는 고려하지 않는다.

3. 캐시가능 (Cacheable Methods)

- 응답 결과 리소스를 캐시해서 사용해도 되는가 (대용량의 데이터를 사용하는 경우 등등...)
- GET, HEAD, POST, PATCH 캐시 가능
- 실제로는 GET, HEAD 정도만 캐시로 사용
 - GET은 URL에 있는 쿼리 파라미터의 내용만 캐시 키로 고려하면 되지만
 - POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데, 구현이 쉽지 않음

## HTTP 메서드 활용

### 클라이언트에서 서버로 데이터 전송

데이터 전달 방식은 크게 2가지로 나뉜다.

1. 쿼리 파라미터를 통한 데이터 전송 : GET
  ex) 정렬 필터(검색어)

2. 메시지 바디를 통한 데이터 전송 : POST, PUT, PATCH
  ex) 회원가입, 상품주문, 리소스 등록, 리소스 변경

데이터 전송을 4가지 케이스로 나누어 살펴보면

1. 정적 데이터 조회
  조회는 GET 사용
  정적 데이터는 일반적으로 쿼리 파라미터 없이 리소스 경로로 단순하게 조회 가능
  ex) 이미지, 정적 텍스트 문서

2. 동적 데이터 조회
  조회는 GET 사용
  GET은 쿼리 파라미터를 사용해서 데이터를 전달
  ex) 주로 검색, 게시판 목록에서 정렬 필터(검색어)

3. HTML Form을 통한 데이터 전송
  ex) 회원가입, 상품 주문, 데이터 변경

  1. POST 전송 - 저장

  ```
  <form action="/save" method="post">
   <input type="text" name="username" />
   <input type="text" name="age" />
   <button type="submit">전송</button>
  </form>
  ```

  웹 브라우저가 생성한 요청 HTTP 메시지

  ```
  POST /save HTTP/1.1
  Host: localhost:8080
  Content-Type: application/x-www-form-urlencoded

  username=kim&age=20
  ```

  form 데이터를 가공하여 request body에 담아 넘김. (쿼리 파라미터 형식으로)
  한글 같은 데이터가 넘어가는 경우가 있으므로 Content-Type은 urlencoded로 넘긴다.
  전송 데이터를 url encoding 처리 한다.
  ex)
  abc김 => abc%EA%B9%80

  2. GET 전송
     HTML Form은 GET 전송도 가능하다.
     form 데이터가 쿼리 파라미터에 담겨 서버로 보내진다.

  3. 첨부파일 전송 (multipart/form-data)

  ```
  <form action="/save" method="post" enctype="multipart/form-data">
    <input type="text" name="username" />
    <input type="text" name="age" />
    <input type="file" name="file1" />
    <button type="submit">전송</button>
  </form>
  ```

웹 브라우저가 생성한 요청 HTTP 메시지

   ```
   POST /save HTTP/1.1
   Host: localhost:8080
   Content-Type: multipart/form-data; boundary=----XXX
   Content-Length: 10457

   ------XXX
   Content-Disposition: form-data; name="username"

   kim
   ------XXX
   Content-Disposition: form-data; name="age"

   20
   Content-Disposition: form-data; name="file1"; filename="intro.png"
   Content-Type: image/png

   109238a9o0p3eqwokjasd09ou3oirjwoe9u34ouief...
   ------XXX--
   ```

   바운더리로 지정한 '----XXX'로 바디의 내용을 잘라서 데이터를 구분한다.
   다른 종류의 여러 파일과 폼의 내용을 함께 전송 가능하기 때문에 이름이 multipart이다.
   여러 타입의 데이터를 담아서 보낼 수 있다.(text, image 등등...)
   주로 바이너리 데이터를 전송할 때 사용한다.

4. HTTP API를 통한 데이터 전송
  ex) 회원 가입, 상품 주문, 데이터 변경
  서버 to 서버, 앱 클라이언트, 웹 클라이언트(Ajax)

### HTTP API 설계 예시

#### 회원 관리 시스템

1. API 설계 - POST 기반 등록

- 회원 목록 /members -> GET
- 회원 등록 /members -> POST
- 회원 조회 /members/{id} -> GET
- 회원 수정 /members/{id} -> PATCH, PUT, POST
- 회원 삭제 /members/{id} -> DELETE

POST 신규 자원 등록 특징 (컬렉션)

- 클라이언트는 등록될 리소스의 URI를 모른다.
 - 회원등록 /members -> POST
 - POST/members
- 서버가 새로 등록된 리소스 URI를 생성해준다.
 - HTTP/1.1 201 Created
   Location: /members/100
- 컬렉션(Collection)
 - 서버가 관리하는 리소스 디렉토리
 - 서버가 리소스의 URI를 생성하고 관리
 - 여기서 컬렉션은 /members

2. API 설계 - PUT 기반 등록

- 파일 목록 /files -> GET
- 파일 조회 /files/{filename} -> GET
- 파일 등록 /files/{filename} -> PUT
- 파일 삭제 /files/{filename} -> DELETE
- 파일 대량 등록 /files -> POST

PUT 신규 자원 등록 특징 (스토어)

- 클라이언트가 리소스 URI를 알고 있어야 한다.
 - 파일 등록 /files/{filename} -> PUT
 - PUT /files/star.jpg
- 클라이언트가 직접 리소스의 URI를 지정한다.
- 스토어(Store)
 - 클라이언트가 관리하는 리소스 저장소
 - 클라이언트가 리소스의 URI를 알고 관리
 - 여기서 스토어는 /files

대부분 POST 기반의 컬렉션을 많이 사용함.

3. HTML FORM 사용

- 회원 목록 /members -> GET
- 회원 등록 폼 /members/new -> GET
- 회원 등록 /members/new, /members -> POST
 (회원 등록 폼과 같은 URI를 쓰는 것을 추천. 등록 시, validation에서 걸려서 반환하거나 할때 URI가 같으면 깔끔하고 처리가 쉬움.)
- 회원 조회 /members/{id} -> GET
- 회원 수정 폼 /members/{id}/edit -> GET
- 회원 수정 /members/{id}/edit, /members/{id} -> POST
- 회원 삭제 /members/{id}/delete -> POST

HTML FORM은 GET, POST만 지원
컨트콜 URI

- GET, POST 만 지원하므로 제약이 있다.
- 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행
- 이런 제약을 해결하기 위해 동사로 된 리소스 경로 사용
- 동사 직접 사용
- POST의 /new, /edit, /delete가 컨트롤 URI
- HTTP 메서드로 해결하기 애매한 경우 사용(HTTP API 포함)

## HTTP 상태코드

클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능

- 1xx (Informational) : 요청이 수신되어 처리 중 (거의 사용하지 않음)
- 2xx (Successful) : 요청 정상 처리

 - 200 OK

 - 201 Created

   - 요청 성공해서 새로운 리소스가 생성됨
   - POST로 무언가를 등록했을 때 반환되는 상태코드
   - 생성된 리소스는 응답의 Location 헤더 필드로 식별한다.
     ex) POST /members -> /members/100

 - 202 Accepted

   - 요청이 접수 되었으나 처리가 완료되지 않음
   - batch 처리 같은 곳에서 사용되는 상태코드
     ex) 요청 접수 후 1시간 뒤에 배치 프로세스가 요청을 처리한다.

 - 204 No Content
   - 서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음
     ex) 웹 문서 편집기에서 save 버튼
     save 버튼의 결과로 아무 내용이 없어도 되고, save 버튼을 눌러도 같은 화면을 유지해야 한다.
   - 결과 내용이 없어도 204 메세지(2xx)만으로 성공을 인식할 수 있다.

- 3xx (Redirection) : 요청을 완료하려면 유저 에이전트(웹 브라우저) 추가 행동이 필요

 Redirection이란?
 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동 (리다이렉트)
 ex)
 이벤트 페이지를 다음과 같이 변경했는데 URL: /event => /new-event
 기존에 북마크를 해두었거나 공유가 많이 된 상태여서 유저들이 /event로 접속하는 상황이 일어날 가능성이 높으니까
 그럴 때 /event로의 접속을 /new-event로 변경하는 것이 리다이렉트이다.

 Redirection의 종류

 1. 영구 리다이렉션
    특정 리소스의 URI가 영구적으로 이동
    원래의 URL을 사용 X, 검색 엔진 등에서도 변경을 인지한다.
    상태코드: 301, 308
    ex) /members -> /users
    ex) /event -> /new-event

 2. 일시 리다이렉션
    일시적인 변경
    따라서 검색 엔진 등에서 URL을 변경하면 안된다.
    주문 완료 후 주문 내역 화면으로 이동
    상태코드 : 302, 307, 303
    PRG : POST/ Redirect / Get

    - 일시적인 리다이렉션
    - ex) POST로 주문 후, 웹 브라우저를 새로고침 하면?
      다시 요청이 되어서 POST 요청이 2번 실행, 중복 주문이 될 수 있다.
      PRG 이후 리다이렉트는 URL이 이미 POST -> GET으로 리다이렉트 된다.
      새로 고침 해도 GET으로 결과 화면만 조회된다.

    1. PRG 사용 전

    1) 요청

    - POST 사용

    ```
    POST /order HTTP/1.1
    Host: localhost:8080

    itemId=mouse&count=1

    ```

    2. 주문 데이터 저장 : mouse 1개

    3. 응답

    ```
    HTTP/1.1 200 OK
    <html>주문 완료</html>
    ```

    4. 결과 화면에서 새로고침
       URL: /order 주문완료

    5. 요청

    ```
    POST /order HTTP/1.1
    Host: localhost:8080

    itemId=mouse&count=1
    ```

    6. 주문 데이터 저장 : mouse 1개

    7. 응답

    ```
    HTTP/1.1 200 OK
    <html>주문 완료</html>
    ```

    2. PRG 사용 후

    1) 요청

    - POST 사용

    ```
    POST /order HTTP/1.1
    Host: localhost:8080

    itemId=mouse&count=1

    ```

    2. 주문 데이터 저장 : mouse 1개

    3. 응답

    ```
    HTTP/1.1 302 Found
    Location: /order-result/19
    ```

    4. 자동 리다이렉트

    5. 요청
       GET 사용

    ```
    GET /order-result/19 HTTP/1.1
    Host: localhost:8080
    ```

    6. 주문 데이터 조회 : 19번 주문

    7. 응답

    ```
    HTTP/1.1 200 OK
    <html>주문 완료</html>
    ```

    8. 결과 화면에서 새로고침
       GET /order-result/19 결과 화면만 다시 요청 (5번으로 이동)
       
 3. 특수 리다이렉션
    결과 대신 캐시를 사용 (캐시에 저장 되어있는 URL을 활용함)

 - 300 Multiple Choices

   - 거의 사용 안함

 - 301 Moved Permanently

   - 영구 리다이렉션
   - 리다이렉트 시, 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있다.
   - 첫 요청에서 작성된 메시지가 제거되기 때문에 리다이렉션 이후 폼 값 등을 다시 작성해야 한다.
   - 하지만 새로운 페이지가 작성되면 폼 값 등도 아예 다 바뀌기 때문에 현업에서는 308보다 301을 반환하여 GET으로 처리하는 경우가 많다.

   301의 흐름

   1. 요청
      POST를 사용해 요청을 보낸다.
      body 내부에 메시지도 존재한다.

   ```
   POST /event HTTP/1.1
   Host: localhost:8080

   name=hello&age=20
   ```

   2. 응답
      301을 반환하며 Location이 지정되어 있다.

   ```
   HTTP/1.1 301 Moved Permanently
   Location: /new-event
   ```

   3. 자동 리다이렉트

   4. 요청
      HTTP 메서드가 GET으로 변경된다.
      body 내부의 메시지도 제거된다.

   ```
   GET /new-event HTTP/1.1
   Host: localhost:8080
   ```

   5. 응답

 - 302 Found

   - 리다이렉트 시, 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있다.
     => 모호한 302를 대신하여 307, 303을 권장하지만 현실적으로 이미 많은 애플리케이션 라이브러리들이 302를 기본값으로 사용한다.
     자동 리다이렉션 시, GET으로 변해도 되면 그냥 302를 사용해도 큰 문제가 없다.

 - 303 See Other

   - 리다이렉트 시, 요청 메서드가 GET으로 변경된다.

 - 304 Not Modified

   - 캐시를 목적으로 사용한다.
   - 클라이언트에게 리소스가 수정되지 않았음을 알려준다.
   - 클라이언트는 로컬 PC에 저장된 캐시를 재사용한다. (캐시로 리다이렉트 한다.)
   - 304 응답은 응답에 메세지 바디를 포함하면 안된다. (로컬 캐시를 사용해야 하므로)
   - 조건부 GET, HEAD 요청 시 사용한다.

 - 307 Temporary Redirect

   - 리다이렉트 시, 요청 메서드와 본문을 유지한다. (요청 메서드를 변경하면 안된다! MUST NOT!!)

 - 308 Permanent Redirect

   - 영구 리다이렉션
   - 리다이렉트 시, 요청 메서드와 본문을 유지한다.(처음에 POST를 보내면 리다이렉트도 POST를 보낸다)

   308의 흐름

   1. 요청
      POST를 사용해 요청을 보낸다.
      body 내부에 메시지도 존재한다.

   ```
   POST /event HTTP/1.1
   Host: localhost:8080

   name=hello&age=20
   ```

   2. 응답
      308을 반환하며 Location이 지정되어 있다.

   ```
   HTTP/1.1 308 Permanent Redirect
   Location: /new-event
   ```

   3. 자동 리다이렉트

   4. 요청
      HTTP 메서드 POST 유지된다.
      body 내부의 메시지도 유지된다.

   ```
   POST /new-event HTTP/1.1
   Host: localhost:8080

   name=hello&age=20
   ```

   5. 응답

- 4xx (Client Error)

 - 클라이언트 오류, 잘못된 문법 등으로 서버가 요청을 수행할 수 없음
 - 오류의 원인이 클라이언트에 있다. ex) 요청 구문, 메시지 등등
 - 클라이언트는 요청 내용을 다시 검토하고 보내야한다.
 - 클라이언트가 이미 잘못된 요청, 데이터를 보내고 있기 때문에 똑같은 재시도가 실패한다(중요!!!)
   반대로 5xx 같은 경우에는 서버에서 발생한 에러이므로 클라이언트가 요청을 보내면 다른 결과(2xx)가 반환될 가능성이 있다.
   => 클라이언트에서 발생한 에러라고 명확하게 명시할 필요가 있음. (프론트 개발자가 validation을 추가로 등록할 수 있도록!)

 - 401 Unauthorized

   - 클라이언트가 해당 리소스에 대한 인증이 필요하다.
   - 인증 (Authentication) 되지 않음
   - 401 오류 발생 시 응답에 WWW-Authenticate 헤더와 함께 인증 방법을 설명
     - 인증(Authentication): 본인이 누구인지 확인(로그인)
     - 인가(Authorization) : 권한부여 (ADMIN 권한처럼 특정 리소스에 접근할 수 있는 권한, 인증이 있어야 인가가 있음)
     - 오류 메세지가 Unauthorized 이지만 로그인이 안됐다고 이해하면 된다.

 - 403 Forbidden 서버가 요청을 이해했지만 승인을 거부함

   - 주로 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우
     ex) 어드민 등급이 아닌 사용자가 로그인은 했지만, 어드민 등급의 리소스에 접근하는 경우

 - 404 Not Found

   - 요청 리소스를 찾을 수 없음
   - 요청 리소스가 서버에 없음.
   - 또는 클라이언트가 권한이 부족한 리소스에 접근할 때 해당 리소스를 숨기고 싶을 때

- 5xx (Server Error) : 서버 오류, 서버가 정상 요청을 처리하지 못함

 - 서버 문제로 오류 발생
 - 서버에 문제가 잇기 때문에 재시도 하면 성공할 수도 있음(복구가 되거나 등등)
   => 서버에서의 에러는 왠만하면 500에러로 처리하지 않는 것이 좋다.
   validation에 걸리거나, 20살 이상에게 판매하는 상품인데 15살이 들어온다거나 한 경우에는 따로 처리를 하고,
   실제 500에러는 서버 로직상의 에러, 예를 들면 널포인트 Exception이 발생하거나, 서버가 다운됐다거나 하는 에러의 경우 발행하는 것이 좋다.

 500 Internal Server Error

 - 서버 내부 문제로 오류 발생
 - 애매하면 500 오류

 503 Service Unavailable

 - 서비스 이용 불가
 - 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음
 - Retry-After 헤더 필드로 얼마뒤에 복구되는지 보낼 수도 있음

=>
모든 상태코드를 사용하는 것은 아니고, 개발 할 때 팀 내에서 몇개만 사용하자고 결정해서 주로 사용함.
상태코드가 다양하면 클라이언트에서 처리하기 복잡해지기 때문에.
ex) 200번대 라면, 200과 201 정도만 사용하고 나머지는 다 200으로 처리하자!

만약에 모르는 상태 코드가 나타나면??

클라이언트는 상위 상태코드로 해석해서 처리한다.
미래에 새로운 상태 코드가 추가되어도 클라이언트를 변경하지 않아도 된다.
ex)
299 ?? -> 2xx (Successful) / 200번대 상태 코드구나 이해하고 처리함.
451 ?? -> 4xx (Client Error)
599 ?? -> 5xx (Server Error)

## HTTP 헤더

### 일반 헤더 - 표현

표현헤더라고도 한다.
표현 헤더는 전송, 응답 둘 다 사용한다.

```
HTTP/1.1 200 OK
// 표현 헤더
Content-Type: text/html;charset=UTF-8
Content-Encoding: gzip
Content-Length: 3423

// 컨텐츠
lkj123sdfagwef12lksjflwkehfaglskj
```

- Content-Type : 표현 데이터의 형식

 - 표현 바디의 형식에 대한 것이다.
 - 미디어 타입, 문자 인코딩
   ex) text/html; charset=utf-8
   application/json
   image/png

- Content-Encoding : 표현 데이터의 압축 방식

 - 표현 데이터를 압축하기 위해 사용
 - 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
 - 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
   ex) gzip, deflate, identity(압축을 안한 상태, 동일한 상태)

- Content-Language : 표현 데이터의 자연 언어

 - 표현 데이터의 자연 언어를 표현
   ex) ko, en, en-US
 - 클라이언트에서 해당 데이터를 보고 언어를 파악해 서비스를 제공하는 것도 가능하다.
   ex) 응답이 영어(Content-Language: en)로 왔는데 화면에 한국어로 표현하고 싶어!

- Content-Length : 표현 데이터의 길이
 - 바이트 단위
 - Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안됨

### 일반 헤더 - 콘텐츠 협상

- 클라이언트가 선호하는 표현 요청
- 협상 헤더는 요청시에만 사용한다.

- Accept: 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
- Accept-Language: 클라이언트가 선호하는 자연 언어

ex)
한국어 브라우저에서 Accept-Language를 ko-KR로 지정하여 보냈다.

```
GET /event
Accept-Language: ko-KR
```

서버는 다중 언어를 지원한다. 기본 언어가 독일어(de)이고, 영어(en)도 지원한다.
하지만 해당 서버에서 한국어를 지원하지 않아 독일어가 반환되었다.

```
Content-Language: de

Hallo (독일어)
```

한국어가 없으면 영어 값을 받고 싶다면 어떻게 해야될까? (우선순위 지정)

#### 협상과 우선순위 1

- Quality Values(q) 값 사용
- 0~1 사이의 값을 표현, 클수록 높은 우선순위를 가진다.
- 생략하면 1이다.
 ex)
 Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
 1. ko-KR;q=1 (q 생략)
 2. ko;q=0.9
 3. en-US;q=0.8
 4. en;q=0.7

#### 협상과 우선순위 2

- Accept에서 미디어 타입을 지정할 경우, 해당 케이스에선 구체적인 것이 우선한다.
 ex)
 Accept: text/_, text/plain, text/plain;format=flowed, _/\*

1. text/plain;format=flowed
2. text/plain
3. text/\*
4. _/_

미디어 타입에 따라서 매치하는 것이 있을 경우 다음 표에 따라서 우선순위를 지정하기도 한다.
| 미디어 타입 | Quality |
|----------|---------|
| text/html;level=1 | 1 |
| text/html | 0.7 |
| text/plain | 0.3 |
| image/jpeg | 0.5 |
| text/html;level=2 | 0.4 |
| text/html;level=3 | 0.7 |

### 전송방식
1. 단순 전송
- Content-Length
- 컨텐츠의 길이를 알때 사용
- 한번에 요청하고 한번에 받는 것
~~~
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3423

<html>
  <body>...</body>
</html>
~~~

2. 압축 전송
- Content-Encoding
- gzip과 같은 형식으로 컨텐츠를 압축해서 전송하는 것
~~~
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Encoding: gzip
Content-Length: 521

lkjlglhjajkealitau3po4qk4j
~~~

3. 분할 전송
- Transfer-Encoding
- 컨텐츠를 덩어리로 보내는 것 (chunked)
- 한번에 보내면 시간이 오래 걸리기 떄문에 5바이트 씩 혹은 특정 바이트 씩 오는 대로 바로 표현하는 것
- 분할 전송 시에는 컨텐츠가 얼마나 올지 예상이 안되기 때문에 Content-Length 사용 X
~~~
HTTP/1.1 200 OK
Content-Type: text/plain
Transfer-Encoding: chunked

5
Hello
5
World
0
\r\n
~~~

4. 범위 전송
- 범위를 지정하여 해당 범위의 컨텐츠만 넘겨받을 수 있도록 하는 것
- 이미지를 전송 받다가 끊겼을 경우, 다시 처음부터 받는 것이 아니라 끊긴 부분 부터 받을 수 있다.
~~~
// 클라이언트 Request
GET /event
Range: bytes=1001-2000
~~~

~~~
// 서버 Response
HTTP/1.1 200 OK
Content-Type: text/plain
Content-Range: bytes 1001-2000 / 2000

qweretyuio12wasz32wesdxc45rtfgvc67yhbn
~~~

### 일반 정보
1. From: 유저 에이전트의 이메일 통보
- 일반적으로 잘 사용되지 않음
- 검색 엔진 같은 곳에서 주로 사용
  ex) 검색엔진을 크롤링 해가는 사람이 있는데 이 사람에게 크롤링 하지 말라고 하고 싶다. 
  이 사람에게 연락할 수단이 된다.
- request 시 사용

2. Referer: 이전 웹 페이지 주소
- 현재 요청된 페이지의 이전 웹 페이지 주소
- A -> B로 이동하는 경우, B를 요청할 때 Referer: A를 포함해서 요청
- Referer를 사용해서 유입 경로 분석 가능
- Request에서 사용
- cf) referer는 referrer의 오타! (HTTP에 이미 사용되버려서 고치기 힘들어 오타를 그대로 사용하게 되었다고..)

* User-Agent: 유저 에이전트 애플리케이션 정보
- user-agent: Mozila/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36
- 클라이언트의 애플리케이션 정보 (웹 브라우저 정보, 등등)
- 통계 정보
- 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
- Request에서 사용

* Server: 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
- Server: Apache/2.2.22 (Debian)
- server: nginx
- Response에서 사용

* Date: 메시지가 생성된 날짜
- Date: Wed, 23 JUN 2021 08:12:31 GMT
- Response에서 사용

### 특별한 정보
1. Host : 요청한 호스트 정보 (도메인)
- Request에서 사용
- 필수 헤더이다.
- 하나의 서버가 여러 도메인을 처리해야 할 때
- 하나의 IP 주소에 여러 도메인이 적용되어 있을 때
ex) 가상 호스트를 통해 여러 도메인을 한번에 처리할 수 있는 서버. 실제 애플리케이션이 여러개 구동 될 수 있다.
특정 api에 접속을 했을 때 해당 서버의 어떤 애플리케이션에서 api를 구동해야 할지 알 수 없기 때문에 host를 꼭 지정해주어야 한다.

~~~
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
~~~

2. Location : 페이지 리다이렉션
- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동한다. (리다이렉트)
- 201 (Created) : Location 값은 요청에 의해 생성된 리소스 URI
- 3xx (Redirection) : Location 값은 요청을 자동으로 리디렉션하기 위한 대상 리소스를 가리킨다.

3. Allow : 허용 가능한 HTTP 메서드
- 405 (Method Not Allowed) 에서 응답에 포함해야 한다.
- Allow : GET, HEAD, PUT

4. Retry-After : 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
- 503 (Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음
- Retry-After: Fri, 31 Dec 1999 23:59:59 GMT (날짜 표기)
- Retry-After: 120 (초단위 표기)

### 인증
1. Authorization : 클라이언트 인증 정보를 서버에 전달
- AUthorization: Basic xxxxxxxxxxxxxxx

2. WWW-Authenticate : 리소스 접근시 필요한 인증 방법 정의
- 리소스 접근 시 필요한 인증 방법 정의
- 401 Unauthorized 응답과 함께 사용
- WWW-Authenticate : Newauth realm="apps", type=1, title="Login to \"apps\"", Basic realm="simple"

### 쿠키
미 로그인 상태던, 로그인 상태던 GET /main API에 접속을 하면 서버는 해당 유저가 로그인을 했는지 안했는지 알 수가 없다.

HTTP는 무상태(Stateless) 프로토콜이기 때문이다.
클라이언트와 서버가 요청과 응답을 주고 받으면 연결이 끊어진다.
클라이언트가 다시 요청하면 서버는 이전 요청을 기억하지 못한다.
클라이언트와 서버는 서로 상태를 유지하지 않는다.

그 대안으로 쿠키를 사용하여 문제를 해결할 수 있다.

쿠키를 지정할 때 다음 두가지의 헤더를 사용한다.
1. Set-Cookie: 서버에서 클라이언트로 쿠키 전달(응답)
2. Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청 시 서버로 전달

~~~
// 웹 브라우저 => 서버
POST /login HTTP/1.1
user=홍길동

// 서버 => 웹 브라우저
HTTP/1.1 200 OK
Set-Cookie: user=홍길동

홍길동 님이 로그인했습니다.
~~~

쿠키 저장소에 저장됨
user=홍길동

~~~
// 로그인 이후 welcome 페이지 접근
// 웹 브라우저 => 서버
GET /welcome HTTP/1.1
Cookie: user=홍길동

// 서버 => 웹 브라우저
HTTP/1.1 200 OK
안녕하세요. 홍길동 님
~~~

모든 요청에 쿠키 정보가 자동 포함된다.
ex) set-cookie: sessionId=abcde1234; expires=Sat, 26-Dec 2020 00:00:00 GMT; path=/; domain=.google.com; Secure

주 사용처
- 사용자 로그인 세션 관리
  상기 예에서는 로그인한 유저의 정보를 user=홍길동이라고 표현하였지만 이렇게 표현하는 것은 위험하다.
  로그인을 하면 서버에서 세션 키를 발행해 DB에 저장하고 해당 세션 id로 로그인 유무를 판단하는 것이 일반적이다.
- 광고 정보 트래킹

쿠키 정보는 항상 서버에 전송됨
- 네트워크 트래픽 추가 유발
- 최소한의 정보만 사용 (세션 id, 인증 토큰)
- 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지 (localStorage, sessionStorage) 참고

주의!
- 보안에 민감한 데이터는 저장하면 안됨 (주민번호, 신용카드 번호 등등)

#### 쿠키 - 생명주기 (Expires, max-age)
- Set-Cookie : expires=Sat, 26-Dec-2020 04:39:21 GMT
  - 만료일이 되면 쿠키 삭제
- Set-Cookie : max-age=3600 (3600초)
  - 0이나 음수를 지정하면 쿠키 삭제
- 세션 쿠키 : 만료 날짜를 생략하면 브라우저 종료시 까지만 유지
- 영속 쿠키 : 만료 날짜를 입력하면 해당 날짜까지 유지

#### 쿠키 - 도메인 (domain)
쿠키가 모든 도메인에서 사용되지 않도록 제한을 지정하는 것이다.
ex) domain=example.org

- 명시 : 명시한 문서 기준 도메인 + 서브 도메인 포함
  - domain=example.org를 지정해서 쿠키 생성
    - example.org는 물론이고, dev.example.org도 쿠키 접근

- 생략 : 현재 문서 기준 도메인만 적용
  - example.org에서 쿠키를 생성하고 domain 지정을 생략
    - example.org에서만 쿠키 접근
    - dev.example.org는 쿠키 미접근

#### 쿠키 - 경로 (path)
쿠키가 사용되는 범위를 도메인으로 지정을 하고 경로로 한번 더 필터를 한다.
ex) path=/home

- 이 경로를 포함한 하위 경로 페이지만 쿠키 접근
- 일반적으로 path=/루트로 지정
- ex) path=/home 지정
- /home -> 가능
- /home/level1 -> 가능
- /home/level1/level2 -> 가능
- /hello -> 불가능

#### 쿠키 - 보안 (Secure, HttpOnly, SameSite)
- Secure
  - 쿠키는 http, https를 구분하지 않고 전송
  - Secure를 적용하면 https인 경우에만 전송

- HttpOnly
  - XSS 공격 방지
  - 자바스크립트에서 접근 불가(document.cookie)
  - HTTP 전송에만 사용

- SameSite
  - XSRF 공격 방지
  - 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송

### 캐시와 조건부 요청
#### 캐시 기본 동작
1. 캐시가 없을 때
1) 요청 (웹 브라우저 -> 서버)
~~~
GET /star.jpg
~~~

2) 응답 (서버 -> 웹 브라우저)
~~~
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 34012

llkkjhgfuue,hlbhjvghykhlkjhqe92oq8ielwdkmmvfxbo5r9ptd
~~~
HTTP 헤더: 0.1MB
HTTP 바디: 1.0MB

3) 웹 브라우저에 이미지 표시
4) 두번째 요청이 있을 때, 1)~3)번의 흐름을 다시 되풀이 한다.

- 데이터가 변경되지 않아도 계속 네트워크를 통해서 데이터를 다운로드 받아야 한다.
- 인터넷 네트워크는 매우 느리고 비싸다.
- 브라우저 로딩 속도가 느리다.
- 느린 사용자 경험

2. 캐시 적용
1) 요청 (웹 브라우저 -> 서버)
~~~
GET /star.jpg
~~~

2) 응답 (서버 -> 웹 브라우저)
~~~
HTTP/1.1 200 OK
Content-Type: image/jpeg
cache-control: max-age=60
Content-Length: 34012

llkkjhgfuue,hlbhjvghykhlkjhqe92oq8ielwdkmmvfxbo5r9ptd
~~~
cache-control은 캐시를 제어하는 헤더
응답결과를 캐시에 저장하는데, 최대 60초동안 유효하도록 설정한 것

3) 웹 브라우저에 이미지 표시
4) 두번째 요청이 있을 때, 60초 이내라면, 캐시에서 데이터를 가져옴 (네트워크를 통할 필요가 없음)

- 캐시 덕분에 캐시 가능 시간 동안 네트워크를 사용하지 않아도 된다.
- 비싼 네트워크 사용량을 줄일 수 있다.
- 브라우저 로딩 속도가 매우 빠르다.
- 빠른 사용자 경험

3. 캐시 적용 / 캐시 시간 초과
캐시 시간이 초과되면 다시 서버에 요청을 한다.
캐시를 초기화 하고, 응답결과를 새로 캐시에 저장한다.

- 캐시 유효 시간이 초과하면, 서버를 통해 데이터를 다시 조회하고, 캐시를 갱신한다.
- 이때 다시 네트워크 다운로드가 다시 발생한다.

#### 검증 헤더와 조건부 요청
캐시 유효 시간이 초과해서 서버에 다시 요청하면 다음 두 가지 상황이 발생할 수 있따.
1) 서버에서 기존 데이터를 변경함
2) 서버에서 기존 데이터를 변경하지 않음

캐시 만료 후에도 서버에서 데이터를 변경하지 않는다.
생각해보면 데이터를 전송하는 대신에 저장해두었던 캐시를 재사용할 수 있다.
단, 클라이언트의 데이터와 서버의 데이터가 같다는 사실을 확인할 수 있는 방법이 필요하다.

1) 요청 (웹 브라우저 -> 서버)
~~~
GET /star.jpg
~~~

2) 응답 (서버 -> 웹 브라우저)
~~~
HTTP/1.1 200 OK
Content-Type: image/jpeg
cache-control: max-age=60
Last-Modified: 2020년 11월 10일 10:00:00
Content-Length: 34012

llkkjhgfuue,hlbhjvghykhlkjhqe92oq8ielwdkmmvfxbo5r9ptd
~~~
Last-Modified는 데이터 최종 수정일을 지정하는 헤더 (검증 헤더)
응답결과를 캐시에 저장하는데, 최대 60초동안 유효함

3) 웹 브라우저에 이미지 표시
4) 두번째 요청을 보냄
~~~
GET /star.jpg
if-modified-since: 2020년 11월 10일 10:00:00
~~~
if-modified-since는 만약 서버 리소스의 최종 수정일이 지정한 날짜로부터 변경되었으면 결과를 반환해달라는 것을 지정하는 헤더 (조건부 요청)
데이터 최종 수정일을 더하여 서버에 넘김

1) 서버에서는 리소스의 최종 수정일과 요청의 최종 수정일을 비교하여 응답을 해줌.
- 최종수정일이 동일할 경우
~~~
HTTP/1.1 304 Not Modified
Content-Type: image/jpeg
cache-control: max-age=60
Last-Modified: 2020년 11월 10일 10:00:00
Content-Length: 34012


~~~
HTTP Body가 없다.
HTTP Body를 전송하지 않기 때문에 헤더(0.1MB)만 전송된다.

6) 캐시에 저장되어 있는 응답 결과를 재사용 하고, 헤더 데이터를 갱신한다. (60초 유효 시간 갱신!)

- 캐시 유효 시간이 초과해도, 서버의 데이터가 갱신되지 않으면 304 Not Modified + 헤더 메타 정보만 응답한다. (바디 x)
- 클라이언트는 서버가 보낸 응답 헤더 정보로 캐시의 메타 정보를 갱신한다.
- 클라이언트는 캐시에 저장되어 있는 데이터를 재활용한다.
- 결과적으로 네트워크 다운로드가 발생하지만 용량이 적은 헤더 정보만 다운로드한다. 매우 실용적인 해결책이라고 할 수 있다.

#### 검증 헤더
- 캐시 데이터와 서버 데이터가 같은지 검증하는 데이터
- Last-Modified : Thu, 04 Jun 2020 07:19:24 GMT
- ETag: "v1.0", ETag: "asdfgh234fg"

#### 조건부 요청 헤더
- 검증 헤더로 조건에 따른 분기
- If-Modified-Since, If-Unmodified-Since: Last-Modified 사용
- If-Match, If-None-Match: ETag 값 사용
- 조건이 만족하면 200 OK
- 조건이 만족하지 않으면 304 Not Modified

ex) If-Modified-Since : 이후에 데이터가 수정되었으면?
  - 데이터 미변경 예시
    - 캐시 : 2020년 11월 10일 10:00:00 vs 서버 : 2020년 11월 10일 10:00:00
    - 304 Not Modified, 헤더 데이터만 전송 (BODY 미포함)
    - 캐시로 리다이렉션 된다. (300번대 HTTP Response Status)
    - 전송 용량 0.1M (헤더 0.1M, 바디 1.0M)
  - 데이터 변경 예시
    - 캐시 : 2020년 11월 10일 10:00:00 vs 서버 : 2020년 11월 10일 11:00:00
    - 200 OK, 모든 데이터 전송 (BODY 포함)
    - 전송 용량 1.1M (헤더 0.1M, 바디 1.0M)

##### Last-Modified, If-Modified-Since 단점
- 1초 미만(0.x초) 단위로 캐시 조정이 불가능
- 날짜 기반의 로직 사용
- 데이터를 수정해서 날짜가 다르지만, 같은 데이터를 수정해서 데이터 결과가 똑같은 경우 (A -> B -> A)
- 서버에서 별도의 캐시 로직을 관리하고 싶은 경우
  ex) 스페이스나 주석처럼 크게 영향이 없는 변경에서 캐시를 유지하고 싶은 경우

#### ETag (Entity Tag)
- 캐시용 데이터에 임의의 고유한 버전 이름을 달아둠
  ex) ETag: "v1.0", ETag: "a2hgjhk3"
- 데이터가 변경되면 이 이름을 바꾸어서 변경함 (Hash를 다시 생성)
  ex) ETag: "aaaaa" => ETag: "bbbbb"
- 진짜 단순하게 ETag만 보내서 같으면 유지, 다르면 다시 받기

1) 요청 (웹 브라우저 -> 서버)
~~~
GET /star.jpg
~~~

2) 응답 (서버 -> 웹 브라우저)
~~~
HTTP/1.1 200 OK
Content-Type: image/jpeg
cache-control: max-age=60
ETag: "aaaaaaaa"
Content-Length: 34012

llkkjhgfuue,hlbhjvghykhlkjhqe92oq8ielwdkmmvfxbo5r9ptd
~~~
캐시에 ETag "aaaaaaaa"를 등록

3) 웹 브라우저에 이미지 표시
4) 두번째 요청을 보냄
~~~
GET /star.jpg
If-None-Match: "aaaaaaaa"
~~~

5) 응답 (서버 -> 웹 브라우저)
- ETag의 값이 일치하는 경우
~~~
HTTP/1.1 304 Not Modified
Content-Type: image/jpeg
cache-control: max-age=60
ETag: "aaaaaaaa"
Content-Length: 34012


~~~
HTTP Body가 없다.
HTTP Body를 전송하지 않기 때문에 헤더(0.1MB)만 전송된다.
캐시에서 조회하여 이미지를 화면에 표시한다.

=> Summary
- 진짜 단순하게 ETag만 서버에 보내서 같으면 유지, 다르면 다시 받기!
- 캐시 제어 로직을 서버에 완전히 관리
- 클라이언트는 단순히 이 값을 서버에 제공 (클라이언트는 캐시 메커니즘을 모름)
  ex) 서버는 배타 오픈 기간인 3일 동안 파일이 변경되어도 ETag를 동일하게 유지
      애플리케이션 배포 주기에 맞추어 ETag 모두 갱신

#### 캐시 제어 헤더
1. Cache-Control : 캐시 제어
- Cache-Control : max-age
  - 캐시 유효 시간, 초 단위로 표시
- Cache-Control : no-cache
  - 데이터ㅓ는 캐시해도 되지만, 항상 원(origin) 서버에 검증하고 사용
  - If-Modified-Since나 Last-Modified 등의 헤더를 활용하여 검증을 체크한다.
- Cache-Contorl :  no-store
  - 데이터에 민감한 정보가 있으므로 저장하면 안됨 (메모리에서 사용하고 최대한 빨리 삭제)
  
2. Pragma : 캐시 제어 (하위 호환)
- Pragma : no-cache
- HTTP 1.0 하위 호환

3. Expires : 캐시 유효 기간 (하위 호환)
- expires: Mon, 01 Jan 2021 00:00:00 GMT
- 캐시 만료일을 정확한 날짜로 지정
- HTTP 1.0부터 사용
- 지금은 더 유연한 Cache-Control: max-age 권장
- Cache-Control: max-age와 함께 사용하면 Expires는 무시

#### 프록시 캐시
한국에 있는 클라이언트가 미국에 있는 원서버에 접근해서 이미지를 다운받으려고 한다고 해보자.
요청/응답(한국 -> 미국 -> 한국) 과정이 한번에 0.5초 (500ms)가 걸린다.
=> 원서버 접근 : 0.5초

한국 어딘가에 프록시 캐시 서버를 세워서 프록시 캐시를 도입해보자.
CDS 서비스라고도 한다.
미국에 있는 원 서버에 첫 요청을 하면 프록시 캐시 서버에 캐시가 기록된다.
그러면 다음 요청부터는 원 서버를 거치지 않고 프록시 캐시 서버로부터 캐시를 받아오기 때문에 0.1초(100ms)가 걸린다.
원 서버에 직접 접근 할 때 보다 시간이 현저하게 줄어든다.
=> 프록시 캐시 서버 : 0.1초

- public 캐시 : 공용으로 사용하는 프록시 캐시
- private 캐시 : 내 웹 브라우저나 로컬의 캐시

#### 프록시 캐시 관련 캐시 지시어 (Cache-Control)
- Cache-Control: public 
  - 응답이 public 캐시에 저장되어도 됨
- Cache-Control : private
  - 응답이 해당 사용자만을 위한 것임, private 캐시에 저장해야 함 (기본 값)
- Cache-Control: s-maxage
  - 프록시 캐시에만 적용되는 max-age
- Age: 60 (HTTP 헤더)
  - 오리진 서버에서 응답 후 프록시 캐시 내에 머문 시간(초)

#### 캐시 무효화
개인 정보나 민감한 정보가 포함되어 있는 페이지가 있다.
해당 페이지에서 캐시를 저장하지 않도록 아래 내용을 모두 지정해주면 절대로 캐시가 저장되지 않는다!

- Cache-Control : no-cache, no-store, must-revalidate
- Pragma : no-cache
  - HTTP 1.0 하위 호환

1. Cache-Control: no-cache
   - 데이터는 캐시해도 되지만, 항상 원 서버에 검증하고 사용 (이름에 주의)
2. Cache-Control: no-store
   - 데이터에 민감한 정보가 있으므로 저장하면 안됨
   - (메모리에서 사용하고 최대한 빨리 삭제)
3. Cache-Control: must-revalidate
   - 캐시 만료 후, 최초 조회 시 원 서버에 검증해야 함
   - 원 서버 접근 실패시 반드시 오류가 발생해야 함 (504 Gateway Timeout)
   - must-revalidate는 캐시 유효 시간이라면 캐시를 사용함
4. Pragma: no-cache
   - HTTP 1.0 하위 호환해서 적용해 줌

ex) no-cache 기본 동작
1. 캐시 서버 요청 (웹 브라우저 -> 프록시 캐시): no-cache + ETag
2. 원 서버 요청 (프록시 캐시 -> 원 서버) : no-cache + ETag
  - 순간적으로 네트워크가 단절되어 원 서버 접근이 불가한 경우
    - 옛날 데이터라도 전송할 수 있다. (200 응답 반환)
    - must-revalidate가 포함되어 있는 경우, 항상 오류를 반환한다. (504 Gateway Timeout을 반환)

3. 원 서버 검증
4. 응답 (원 서버 -> 프록시 캐시) : 304 Not Modified
5. 응답 (프록시 캐시 -> 웹 브라우저) : 304 Not Modified
6. 캐시 데이터 사용 : no-cache / ETag: "aaa"

## 관련 토픽
### HTTP 스펙
- RFC 2616 : 보면 안됨!!
- RFC 7230-7235 : 이걸로 모두 개정됨.

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
