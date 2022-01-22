# Session Auth

`express-session`이라고 하는 middleware를 활용하는 것을 기본으로 한다.

~~~
npm install express-session
~~~

## 세션 탄생의 흐름
쿠키의 탄생은 개인화와 인증 과정의 발전을 이끌었다.
쿠키를 통해 개인별 맞춤 설정을 제공할 수 있게 되었고, 유저의 로그인 정보를 담아 인증을 확인할 수 있었다.
하지만 쿠키는 탈취되거나 조작될 가능성이 있어 보안 취약점을 가지고 있다.
이를 해결하고자 등장한 것이 세션이다.

## 세션이란?
세션은 쿠키의 단점을 보완하기 위해 탄생했다.
유저가 로그인을 하면 sid(session_id)가 쿠키에 저장된다.
유저가 ui 조작을 할때마다 api는 쿠키에 담긴 sid를 싣고 서버로 가서 인증된 유저의 요청인지를 확인한다. 
즉, 쿠키에선 브라우저에 담고 있던 개인정보를 서버 db나 파일로 이동해서 확인하는 것이다.
정보 보안 측면에 있어서 더욱 안전한 방법을 택했다고 할 수 있다. 