# AWS

생활코딩의 아마존 웹서비스(AWS) 강의를 듣고...

## 아마존 웹서비스와 클라우드 컴퓨팅

클라우드 컴퓨팅이란, 로컬 컴퓨터를 (어딘가에 있는, 여러대의 컴퓨터가 연결되어 있는) 거대한 컴퓨터와 인터넷으로 연결하여
내 컴퓨터에서 처리하고자 하는 것을 거대한 컴퓨터에서 처리하고 그 결과값을 인터넷으로 내려받는 형식을 말한다.
핵심은 인터넷이며, 인터넷에 연결되어 있는 컴퓨터를 사용한다는 것이 본질이다.
인터넷으로 다른 거대한 컴퓨터와 연결되어 있는 것을 구름(클라우드)로 표현한 것이다.

아마존이 대표적으로 클라우드 컴퓨팅 서비스를 제공하고 있으며, 기반 기능과 IT 트랜드에 맞춰서 추가된 여러 기능들을 제공하고 있다.

## 회원가입

아마존 웹 서비스는 기업용 서비스로서 비용이 지불되는 서비스이므로 비밀번호는 신중하게 입력할 것!
해킹의 위험이 있기 때문에 평소에 사용하지 않는 어려운 비밀번호로 지정할 것!!

## 보안설정 - 2딘계 인증

루트계정에서 MFA 활성화를 한다.
MFA는 다요소 인증(Multi-factor Authentication)의 줄임말이다. ex) OTP, TOTP 등...
MFA를 활성화 하면 로그인 시 비밀번호를 입력하고 추가로 다른 방식으로 인증을 해야 로그인이 가능하다.

IMA > 보안 자격 증명 > 멀티 팩터 인증(MFA) > MFA 활성화 버튼 클릭

인증 방법으로
Google OTP 추천 : 안드로이드와 ios에서도 사용 가능 ex) Google OTP, Google Authentication으로 검색

다만, GoogleOTP를 선택해서 기기를 변경했거나, 분실, 손상 됐을 경우에는 문의를 해야함.
id/pw로 로그인하면 오른편에 문의하기 버튼이 있음.
복원하려면 절차가 복잡하니 2단계 인증은 관리를 잘 할 것!
(강사님의 설명대로라면 몇시간~하루 뒤에 구글에서 전화가 옴. aws에 가입한 이메일 계정으로 코드를 하나 보냈으니 해당 코드를 말해달라고 함. 모든건 영어로 대화가 이루어짐.)