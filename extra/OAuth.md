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