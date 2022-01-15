# 쿠키
웹이 발달함에 따라 개인화 대한 요구가 일어났다.
웹에 접속하는 유저에 맞는 서비스를 제공하고자 하는 것이다.

ex)
- 장바구니에 물건을 담아놓으면 다음에 접속했을 때도 장바구니에 물건이 그대로 담겨있음
- 한번 인증을 해놓으면 다시 접속해도 로그인이 유지됨

## 목적
쿠키는 대표적으로 다음 3가지의 목적을 가진다.

1. 세션 관리
- 로그인, 장바구니, 게임 점수 유지 등등 서버가 저장해야 할 것들을 관리한다.

2. 개인화
- 유저 취향, ui 테마, 여러 셋팅 등을 저장한다.

3. 트래킹
- 유저의 행동을 기록한다.

## 생성
http response 시 헤더에 `Set-Cookie` 값을 지정해주면 쿠키가 셋팅된다.
셋팅된 쿠키는 이후 http request 헤더에 `Cookie`로 실려 자동으로 전달된다.

~~~
Set-Cookie : <cookie-name>=<cookie-value>
~~~

ex)
yummy-cookie와 tasty-cookie 쿠키 값이 셋팅된다.
~~~
HTTP/1.0 200 OK
Content-Type : text/html
Set-Cookie : yummy-cookie=choco
Set-Cookie : tasty-cookie=strawberry

[page content]
~~~
