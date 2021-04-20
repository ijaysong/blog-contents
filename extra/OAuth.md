# OAuth 2.0
사용자가 가입된 서비스의 API에 접근하기 위해서는 사용자로부터 권한을 위임 받아야 한다. 
이 때 사용자의 패스워드 없이도 권한을 위임 받을 수 있는 방법이 필요한데,이를 위해서 고안된 기술이 OAuth이다. 
오늘날 많은 API들이 OAuth를 통해서 상호 연동을 지원하고 있다. 
다른 서비스로 로그인 하기 기능을 구현하는데도 필수적으로 필요한 기능입니다. 
ex) 구글로 로그인 하기, 네이버로 로그인 하기

## OAuth의 세 가지 주체
1. 나의 서비스
2. 유저
3. 나의 서비스가 연동하려는 외부 서비스 ex) Google, Facebook, Twitter

예를 들어, 
유저가 내 서비스를 통해서 Facebook이나 Twitter에 글을 쓰고 싶다고 해보자.
그러면 내 서비스는 외부 서비스에 가입되어 있는 유저의 id와 password를 입력 받아서 가지고 있다가,
외부의 서비스에 접근하려고 할 때 사용할 수 있다.
이것은 외부 서비스의 모든 기능을 사용할 수 있기 때문에 아주 강력하다고 할 수 있다.

하지만 이것은 유저의 입장에서 매우 불안한 일이다. (특정 서비스가 내 ID와 PW를 가지고 있는 셈이기 떄문에!)
나의 서비스의 입장에서도 고객의 정보를 지켜야 한다는 부담감이 있고, 보안에 더 신경써야 한다.
외부의 서비스 입장에서도 ID와 PW를 제 3자가 가지고 있다는 것이 불만족스러울 것이다.

oAuth를 사용하면 이러한 과정을 더욱 안전하게 만들 수 있다.
나의 서비스는 유저의 ID와 PW 정보를 받는 것이 아니라 외부 서비스로 부터 Access Token을 받는다.
외부 서비스에 접근할 때 Access Token을 사용해 회원을 식별하고, 제한된 기능만 사용할 수 있게 된다.

## 역할
OAuth의 3가지 주체에 대한 명확한 용어는 다음과 같다.

1. Resource Server
나의 서비스가 연동하려는 외부 서비스
즉, 나의 서비스가 제어하고자 하는 자원을 가지고 있는 서버를 뜻한다.

2. Resource Owner
유저이며, Resource Server의 자원을 가지고 있는 소유자를 뜻한다.

3. Client
나의 서비스(애플리케이션)이다.
Resource Server에 접속하여 자원을 사용하려 하는 주체이므로 Client라고 한다.

4. Authorization Server
OAuth의 공식 메뉴얼을 보면 3가지 주체 이외에 하나가 더 있다.
Resource Server는 데이터를 가지고 있는 서버이며,
Authorization Server는 인증과 관련된 처리를 전담하는 서버이다.
간략하게 Authorization Server를 생략하여 3가지 주체로 표현하곤 한다.

## 등록
OAuth를 이용해서 Resource Server에 접속하기 위해서는 우선 Resource Server에 등록하는 과정이 필요하다.
Client가 Resource Owner의 정보를 받기 전에 미리 Resource Server에 허가를 받는 것을 등록(register)이라고 한다.

Client를 등록하면 Resource Server에 다음과 같은 정보가 생성된다.

1. Client ID 
클라이언트를 식별하는 식별자 아이디이다. ex) 1

2. Client Secret 
Client ID에 대한 비밀번호이다. 절대로 외부에 노출되면 안되는 정보이다. ex)2

3. Authorized redirect URIs 
Resource Server가 Client에게 권한을 부여하는 과정에서 Authorized Code를 전달하는데, 
그때 해당 주소로 전달해 달라고 지정한 것이다. 이외의 주소로 접근하면 무시한다.
ex) https://client/callback

### OAuth로 Facebook 사용하기
1. Facebook for developer 페이지 우 상단에 MyApps라는 카테고리 클릭
2. Add New App > Create a new App ID
3. Facebook Login을 클릭
4. 연동하려는 Client의 URL주소를 입력한다.
5. Settings > Redirect URI to Check에 https://client/callback 임시 등록

### OAuth로 Google 사용하기
1. Google Cloud Platform > select a project > new project
2. 좌 상단에 있는 햄버거 아이콘 > API Service > Credentials > Create Credentials
3. Create OAuth ID > Client ID와 Client Secret이 생성된다. (Client Secret은 잊어버리면 안된다!)

## Resource Owner의 승인
Client가 Resource Server에 등록을 하게 되면 양쪽 모두 다음과 같은 중요한 정보에 대해 알게 된다.

* Resource Server : Client ID, Client Secret, redirect URL
* Client : Client ID, Client Secret 

예를 들어,
Resource Server의 기능으로 A, B, C, D 가 있다고 해보자.
Client는 모든 기능이 필요한 것이 아니라 B와 C만 필요하다.
최소한의 기능 B와 C에 대해서 인증을 받는 것이 양쪽에게 현명한 선택이다. 
(Resource Server의 입장에서 제 3자가 사용하는 것이 달가운 일이 아니므로)

Resource Owner 가 Client를 통해서 Resource Server에 접속하고자 한다고 해보자.
ex) Client를 통해서 Facebook에 글을 쓰고 싶다던가!

OAuth의 첫번째 절차는 Resource Owner가 Resource Server에게 Client의 접근을 승인한다는 것을 알려줘야 한다.
ex) Login with Facebook, Login with Twitter, Loin with Google
버튼을 클릭하면 다음 URL이 실행되도록 한다.
~~~
// 승인요청 URL
https://resource.server?client_id=1&scope=B,C&redirect_uri=https://client/callback
~~~
* scope = Resource Server의 기능

1. 승인요청 URL로 Resource Server에 접속을 하는데
2. Resource Server는 Resource Owner가 로그인이 되어 있는지 아닌지를 확인하고
3. 로그인이 안되어 있으면, 로그인 화면을 보여주고
4. 로그인이 되어 있으면, 승인 요청 URL의 파라미터로 넘겨 받은 Client ID가 Resource Server에 등록되어 있는 것인지 확인한다.
5. 매칭되는 Client ID가 존재 한다면, 해당 Client ID의 redirect URL과 승인 요청 URL의 파라미터로 넘겨받은 redirect URL이 동일한지 확인한다.
6. 동일하지 않다면, 작업을 종료하고
7. 동일하다면, 승인 요청 URL의 파라미터로 넘겨받은 scope의 기능을 사용하도록 허가할 것인지 Resource Owner에게 확인을 받는다.
8. 허용을 받으면, Resource Server는 다음과 같은 정보를 저장한다.
- (기존 정보) Client ID : 1
- (기존 정보) Client Secret : 2
- (기존 정보) redirect URL : https://client/callback
- (해당 단계에서 새롭게 등록된 정보) user ID : 1
- (해당 단계에서 새롭게 등록된 정보) scope : b, c

## Resource Server의 승인
Resource Server는 Client가 등록된 Client가 맞는지 확인하기 위해서 Resource Owner을 통해서 Client에게 Authorization code를 전달한다. 
이 값을 받은 Client는 이 값과 Client secret의 값을 Resource Server로 전송해서 Client의 신원을 Resource Owner에게 증명한다.

해당 상태에서 Resource Server가 가지고 있는 정보
- Clinet id : 1
- Client Secret : 2
- redirect URL : https://client/callback
- user id : 1
- scope : b, c
- Authorization code : 3

Resource Server는 Resource Owner에게 다음과 같은 정보를 헤더에 담아 request를 보낸다.
리다이렉드 주소를 헤더에 담은 것이다.
code=3은 Authorization code가 3이라는 뜻이다.
- Location : https://client/callback?code=3

해당 request가 Resource Owner에 닿으면, 리다이렉드 주소(Client를 가리킴)에 의해서 Client에 Authorization code가 전달된다.
해당 상태에서 Client가 가지고 있는 정보
- Client id : 1
- Client Secret : 2
- Authorization code : 3

Client는 다음 주소로 Resource Server에 직접 접속한다.
~~~
https://resource.server/token?grant_type=authorization_code&code=3&redirect_uri=https://client/callback&client_id=1&client_secret=2
~~~
authorization_code와 client_secret이라는 두개의 비밀번호를 함께 전송한다.

그러면 Resource Server는 건네 받은 Authorization code의 값과 일치하는 정보를 찾아보고 값이 일치하는지 확인한다.
Clinet id, Client secret, redirect URL 등등...
해당 정보가 일치하면 Resource Server는 Access Token을 발급한다.