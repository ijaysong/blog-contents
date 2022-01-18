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

## 활용
ex) Mozilla (https://developer.mozilla.org/ko/docs/Mozilla)

모질라 페이지에서 로그인을 하면 쿠키에 sessionid가 생성 된 것을 볼 수 있다.
sessionid는 로그인 id와 pw를 전혀 담고 있지 않은 정보이지만, 
id (abcd)로 로그인해서 얻은 sessionid (1234)를 다른 브라우저의 쿠키에 셋팅하면 id abcd로 로그인 한 것으로 인식한다.

~~~
* key = sessionid
* value = 1234
~~~

sessionid가 유출되면 다른 사람이 허락 없이 내 아이디를 사용할 수도 있는 것이다.
쿠키는 그만큼 중요한 역할을 하고 보안사고가 일어나지 않도록 주의를 기울여야 한다!

## 종류
### 1. session 쿠키
- 웹 브라우저를 끄면 사라지는 쿠키 

~~~
set-cookie: yummy-cookie=choco
~~~

### 2. permanent 쿠키
- 영속적인, 지속적인
- 웹 브라우저를 꺼도 사라지지 않는 쿠키
- 쿠키 key, value 이외에 max-age나 expires에 대한 옵션을 지정해준다.

~~~
set-cookie: yummy-cookie=choco; Expires=Wed, 2 JAN 2022 07:28:00 GMT;
~~~

그렇다면 expires와 max-age는 어떻게 다른가!

expires는 만료되다 라는 뜻으로, 쿠키가 언제 사라질 것인가에 대한 것으로
구체적인 날짜라는 절대적 시점이 지정되어 있다.

max-age는 현재 시점을 기준으로 상대적으로 쿠키가 얼마동안 살 것인가를 표현한다. (초 단위)

## 옵션
### 1. Secure
웹 브라우저와 웹 서버가 https로 통신하는 경우만 웹 브라우저가 쿠키를 서버로 전송하는 옵션이다.

### 2. HttpOnly
자바스크립트의 document.cookie를 이용해서 쿠키에 접속하는 것을 막는 옵션이다.
XSS와 같이 악성 스크립트 실행하여 쿠키를 탈취하는 것을 막기 위한 방법이다.