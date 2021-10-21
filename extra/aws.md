# AWS

생활코딩의 아마존 웹서비스(AWS) 강의를 듣고...

## 아마존 웹서비스와 클라우드 컴퓨팅

클라우드 컴퓨팅이란, 간단히 말해 자신의 컴퓨터가 아닌 인터넷으로 연결된 다른 컴퓨터로 처리하는 기술을 말한다.
로컬 컴퓨터를 (어딘가에 있는, 여러대의 컴퓨터가 연결되어 있는) 거대한 컴퓨터와 인터넷으로 연결하여
내 컴퓨터에서 처리하고자 하는 것을 거대한 컴퓨터에서 처리하고 그 결과값을 인터넷으로 내려받는 형식을 말한다.
핵심은 인터넷이며, 인터넷에 연결되어 있는 컴퓨터를 사용한다는 것이 본질이다.
인터넷으로 다른 거대한 컴퓨터와 연결되어 있는 것을 구름(클라우드)로 표현한 것이다.

아마존이 대표적으로 클라우드 컴퓨팅 서비스를 제공하고 있으며, 기반 기능과 IT 트랜드에 맞춰서 추가된 여러 기능들을 제공하고 있다.

## 다양한 클라우드 서비스 제공업체

- Amazon AWS
- Google
- Microsoft Azure
- Pivotal, Heroku, Digital Ocean
- 네이버, NHN Enter
- KT

## 대표적인 클라우드 컴퓨팅 리소스

- CPU, memory => 컴퓨팅
- 그래픽 카드 => GPU = 복잡한 계산 (렌더링, 머신 러닝, 딥러닝, ...)
- SSD (하드디스크) => 저장 장치
- 네트워크

## 컴퓨팅, 스토리지, 네트워크

클라우드 컴퓨팅 업체에서 기본적으로 제공해주는 기능으로
Infrastructre as a Service = IaaS(아이아스), 가상의 컴퓨터를 원하는 시간만큼 빌려올 수 있다.

## AWS에서 제공되는 PC의 구성

- EC2

* CPU + 메모리로 구성
* GPU가 포함된 경우도 있음

- EBS

* EC2에 연결해서 사용하는 SSD
* OS 및 필요한 프로그램과 데이터의 일부를 저장

- VPC

* EC2를 연결하기 위한 네트워크 망
* VPC와 인터넷을 연결해야 서비스 사용 가능

## 보다 저렴하게 AWS 구성하기

결제 옵션을 예약으로 구매하면 조금 더 저렴하다.
EC2 설정 시, 사용량 비율을 나눠서 일정 비율은 좋은 성능의 EC2에 할당하고 일정 비율은 저렴한 EC2가 실행되도록 사용량을 지정할 수도 있다.
저장 공간 할당 시, EBS의 크기를 줄이고 S3의 크기를 늘리는 방식으로 조금 더 저렴하게 구매할 수도 있다.
S3는 EBS(SSD 서비스)보다 저렴하다.
## 회원가입

아마존 웹 서비스는 기업용 서비스로서 비용이 지불되는 서비스이므로 비밀번호는 신중하게 입력할 것!
해킹의 위험이 있기 때문에 평소에 사용하지 않는 어려운 비밀번호로 지정할 것!!

## 보안설정 - 2단계 인증

루트계정에서 MFA 활성화를 한다.
MFA는 다요소 인증(Multi-factor Authentication)의 줄임말이다. ex) OTP, TOTP 등...
MFA를 활성화 하면 로그인 시 비밀번호를 입력하고 추가로 다른 방식으로 인증을 해야 로그인이 가능하다.

IMA > 보안 자격 증명 > 멀티 팩터 인증(MFA) > MFA 활성화 버튼 클릭

인증 방법으로
Google OTP 추천 : 안드로이드와 ios에서도 사용 가능 ex) Google OTP, Google Authentication으로 검색

다만, GoogleOTP로 추가 인증을 하고 있다면, 핸드폰을 바꿀 때 MFA를 삭제하고 초기화 할 것!!
그렇지 않으면 AWS 쪽에 직접 문의를 해야함. (기기 변경, 분실, 손상)
id/pw로 로그인하면 오른편에 문의하기 버튼이 있음.
복원하려면 절차가 복잡하니 2단계 인증은 관리를 잘 할 것!
(강사님의 설명대로라면 몇시간~하루 뒤에 구글에서 전화가 옴. aws에 가입한 이메일 계정으로 코드를 하나 보냈으니 해당 코드를 말해달라고 함. 모든건 영어로 대화가 이루어짐.)

## IAM
사용자가 리소스를 사용하려고 할 때 권한을 허용할지 세부적으로 조정하는 서비스이다.
보안을 위해서 루트를 사용하기 보단 IAM 사용자를 생성해서 사용하는 것이 권장된다.

먼저 IAM 그룹을 생성한다.
- 그룹 이름 : IAM 그룹 이름
- 정책 연결 : IAM 정책을 검색하여 설정할 수 있다. ex) AdministratorAccess

IAM 사용자를 생성한다.
- 사용자 이름 : IAM 사용자 이름
- AWS 액세스 유형 선택 : AWS 액세스 방법을 선택하는 것이다.
   ex)
       프로그래밍 방식 엑세스 : 개발 할 때 사용
       AWS Management Console 액세스 : AWS 관리 콘솔에서 작업할 때 사용

IAM 그룹에 사용자를 등록한다.
그러면 IAM 사용자의 엑세스 정보가 CSV 파일로 출력이 되는데,
해당 파일에 어떤 링크로 접속해서 어떤 아이디와 패스워드로 접속하면 되는지가 적혀있다.
파일의 내용대로 하면 IAM 계정으로 접속할 수 있다.
정책에 따라서 접근 가능한 서비스가 제한되어 있지만, IAM 계정 자신의 정보 등은 수정이 가능하다.

### IAM 로그인 URL 변경
IAM 계정으로 로그인을 하기 위해선 계정 번호가 포함된 URL에 접속을 해야 한다.
~~~
https://{계정 번호}.signin.aws.amazon.com/console
ex) https://962895253643.signin.aws.amazon.com/console
~~~
하지만 계정 번호가 포함된 URL을 매번 입력하는 것이 어렵기 때문에 사용자가 지정한 URL로 접속할 수 있도록 변경할 수 있다.
IAM 메인 페이지 > IAM 사용자를 위한 로그인 URL > 사용자 지정 ex) aws-test
~~~
https://aws-test/signin.aws.amazon.com/console
~~~

지정한 별칭으로 IAM 계정으로 로그인을 할 수도 있다.
- 계정 ID(12자리) 또는 계정 별칭 : aws-test
- 사용자 이름 : IAM 계정 ID
- 암호 : IAM 계정 PW

## IAM Policy
- IAM User
   - 그룹의 IAM Policy에 따라 권한을 부여받는다.
   - 사용자에게 직접 Policy를 추가할 수도 있다.
   - IAM User의 인증방식과 사용용도
       - ID/PW : 관리 콘솔에서 사용
       - AccessKey ID / Secret Access Key : CLI, SDK, Web API에서 사용
   - 영구 자격 증명(Long Term Credential)이라고도 한다.

- IAM Group
   - 공통 권한을 가지는 사용자들의 집합
   - 그룹 생성 후 IAM Policy 연결
   - 그룹에 사용자 추가
   - 그룹 내 사용자는 그룹과 연결된 Policy의 권한을 부여받는다.

- IAM Policy
   - AWS 서비스의 접근 권한을 세부적으로 관리하기 위해 사용
   - JSON 포맷의 문서
   - Group, User, Role 등에 적용 가능

- Role
   - 임시 자격 증명 ex) 1시간, 3시간 동안
   - AWS 내부의 서비스들이 인증하고자 할때 사용

## 지역과 가용구역

AWS의 인프라가 위치하고 있는 공간에 대해 지역(Region)과 가용구역(avaliability zone)으로 구분할 수 있다.

### 지역(Region)

아마존 웹 서비스가 보유하고 있는 컴퓨터가 어디에 위치하고 있는가를 의미한다.
사이트를 사용하는 고객이 위치하고 있는 곳과 가상 컴퓨터의 위치가 멀면 멀수록 네트워크 속도가 느려지기 때문에 웹 사이트를 접속하는 고객이 주로 어느 위치에 있는가가 Region을 선택하는 중요한 고려 사항이 될 수 있다.

+) 참고
서울 Region은 2016년에 개설되었다.
현재 기준으로 (2021년 2월) 가용영역은 총 4개가 존재한다.

+)
한국을 기준으로 aws 각 region과의 네트워크 속도를 측정할 수 있는 사이트이다.
서울 > 오사카 > 도쿄 순으로 속도가 빠른 것을 알 수 있다.
http://www.cloudping.info

+)
각 region 마다 같은 상품을 사용해도 가격이 다르다는 점이다.
투자의 문제일 수도 있고, 환율의 문제일 수도 있으니 지역을 선택하기 전에 꼭 확인해보아야 한다.
그러므로 지역은 중요한 이슈 중 하나이다.

### 가용 영역(avaliability zone)

자연재해 발생 시 백업의 용도로 하나의 region에 여러 az가 존재한다.
하나의 지역 안에는 여러 가용영역으로 나뉘어져 있으며, 각 건물들 간에 인터넷 보다 더 빠른 전용 선으로 직접 연결되어 있다.
마치 같은 건물에 있는 것 처럼 빠른 속도로 데이터를 주고 받을 수 있다.

같은 지역 안에 존재하는 서로 다른 가용 영역끼리 데이터를 주고 받을 수 있지만, 서로 다른 지역에 있는 것들과는 데이터를 주고 받을 수 없다.
아예 주고 받을 수 없는 건 아니지만 인터넷 선을 통해서 느리게 주고 받을 수 있다.

ex)

region 명             az 명  연결           az 명
--------------------  -----  -------------  -----
region1 : 도쿄        az1    <- 전용 선 ->  az2  
<- 인터넷 선 ->                                  
region2 : 캘리포니아  az1    <- 전용 선 ->  az2  

## AWS EC2

EC2(Elastic Compute Cloud)는 독립된 컴퓨터를 임대해주는 서비스이다.

### EC2 생성 및 삭제

인스턴스란, 컴퓨터 한대라고 이해하면 된다. ex) 3대의 컴퓨터를 임대했다 == 인스턴스 3개를 만들었다.
원래대로라면 컴퓨터를 구매하고 설치했어야 할 과정이지만 단 1분만에 인스턴스를 만들 수 있다.
또한, 원격제어로 접속하여 미국 캘리포니아에 설치한 인스턴스를 내 자리에 있는 컴퓨터처럼 사용할 수도 있다.

- 인스턴스 생성 방법
 운영체제 선택 > cpu/memory 선택 > 인스턴스 갯수 설정(1개) > 저장장치 설정 (8GB) > 태그 인스턴스 (컴퓨터 이름 지정) > 컴퓨터 보안 설정 (보안 그룹 이름 설정) > 지정한 내용을 최종적으로 review하고 launch 버튼 > 비밀키 설정 (새로 만든 인스턴스에 접속하기 위한 비밀번호를 지정하기 위한 것임.) > key pair name을 지정하면 비밀번호가 파일로 다운받아짐.

- 인스턴스 일시 중지 및 삭제 방법
 아주 간단하게 인스턴스를 일시 중지 혹은 삭제할 수 있으며, 과금이 되지 않는다.
 EC2 > 삭제할 인스턴스 선택 > 오른쪽 클릭 > instance status > stop / terminate 선택
 
 ### EC2 인스턴스 타입

EC2 인스턴스는 가격과 관련이 있기 때문에 중요한 요소 중 하나이다.

- 운영체제 선택
 인스턴스를 생성할 때 지정하는 운영체제는 크게 두가지로 나뉜다.

* unix계열 : amazon linux, redhat , buse Linux, Ubuntu
* window : Windows Server 2012 R2 Base
 1년간 무료로 사용 가능하며, 이외의 것들은 유료이다.

- 인스턴스 타입 선택
 컴퓨터의 사양을 선택하는 것이라고 이해하면 된다.
 freetier만 1년간 무료로 사용할 수 있는 스펙이며, vCpus, Memory, Network Performance 등을 지정할 수 있다.
 
 ### EC2 가격정책

EC2의 가격정책에는 여러가지가 있으며, aws 페이지에서 가격을 미리 살펴볼 수 있다.
가격 정책은 시간당 계산하고 있으며, 자신의 상황에 따라서 현명하게 선택해야 한다.

- 온 디맨드 인스턴스
 필요할 때마다 켜고 끄는(온디맨드) 인스턴스이다.
 운영체제별로 가격 정책이 다름

- 예약 인스턴스
 할인권을 구매하는 것이라고 생각하면 된다.
 예를 들어 일년간 인스턴스를 한번도 끄지 않고 사용할 예정이라면 1년권을 구매할 수도 있고, 혹은 3년치 할인권을 살 수도 있다.
 일반 가격보다 훨씬 더 저렴하게 쓸 수 있으며, 최대 75% 할인된 가격으로 사용할 수 있다.
 물론 온디맨드 인스턴스처럼 켜고 끄는 것을 지정할 수 있다.
 다만, 인스턴스를 할인권 기간만큼 사용하지 않는다면 혜택을 못 누리기 때문에 잘 생각하고 사야된다.

- 스팟 인스턴스
 인스턴스를 여러개 생성한 유저에게 유리한 가격 정책이다.
 일지 중지 상태인 컴퓨터가 많을 때는 그 가격이 저렴해지지만, 가용중인 인스턴스가 많을 때는 일반 가격보다 더 비싸질 수 있다.
 요금이 주가처럼 가변적인 것이 특징이다.
 온디맨드 인스턴스처럼 켜고 끄는 것을 지정할 수 있다.

### EC2 인스턴스 장치 설정

몇개의 인스턴스를 설정할 것인지 지정 가능하다.
aws 초보자들이 실수를 많이 해서 생성할 수 있는 컴퓨터 갯수가 제한되어 있다.
서비스 론칭 등의 어떤 이벤트가 있거나 할때 aws 측에 요청하여 한도를 늘릴 수 있다.

- EC2 인스턴스 장치 설정 항목
  인스턴스 타입 지정 : 스팟 인스턴스 or not
  shutdown 시 event 설정 : 일시정지(stop) or 삭제(terminate)
  삭제 시 방지 대책 : 백업 사용 or not
  상세 모니터링 저장 유무 등등..

- 저장 장치 추가 (EBS: Elastic Block Store)
  CPU : 리눅스는 기본 8기가, 윈도우는 기본 30기가 (30GB까지 무료)
  IOPS : 저장장치의 속도
  Delete on Termination : 만든 인스턴스가 삭제가 되면 해당 저장장치도 함께 삭제 or not
  체크 시, 인스턴스가 삭제가 되면 저장장치도 함께 삭제 (내장하드)
  체트 해제 시, 인스턴스가 삭제되어도 저장장치는 남아있다 (외장하드) / 저장장치가 남아있어서 과금이 될 수도 있으므로 유의!

### EC2 태그와 보안그룹

- EC2 태그
  key-value 형식으로 기입한다.
  해당 인스턴스가 어떤 역할인지, 누가 관리하는지 등을 태그에 기록할 수 있다.

  ex)
  | key | value |
  |----|-------|
  | Name | Web Server |
  | 관리자 | Eunji Song |
  | Type | real |

- EC2 보안그룹
  어떤 방식의 접속만 허용할 것인지, 방화벽과 같은 역할을 한다.
  자신이 어떤 인스턴스를 만들지에 따라 보안 정책이 달라진다.
  시큐리티 그룹 내 그룹 명과 설명이 중복되면 안된다!

Assing a security group (택 1) : Create new security group(선택) / Select an existing security group
security group name : web
Description : for web server
Type :

- SSH(Secure Shell) : 리눅스계열의 원격제어 방식
- HTTP : 웹 브라우저를 통해서 접속하는 방식

Port :
Source :

- My IP (내가 현재 접속한 IP로만 접속이 됨)
- Anywhere (어떤 IP라도 접속이 됨)

### EC2 인스턴스 비밀번호 생성

인스턴스의 네트워크를 통해서 접속할 때 사용할 비밀번호를 지정하는 것이다.
비밀번호의 이름을 지정하고 Download key pair 버튼을 클릭하면 아마존에서 비밀번호(private key)를 랜덤하게 생성하여 파일로 다운로드 한다.
비밀번호 다운로드가 완료되면 생성한 인스턴스에도 동일한 비밀번호(public key)를 생성한다.
그리하여, 해당 인스턴스에 접속하려면 다운로드 한 비밀번호를 가지고 접근해야 한다.
문제는 파일로 저장된 비밀번호는 탈취될 가능성이 있으므로, 해당 비밀번호 파일을 잘 관리해야 한다는 점이다.
비밀번호를 분실하면 다시 복구해주지 않으므로 소중하게 관리해야 한다.

### EC2 리눅스 인스턴스 접속 (OSX)

인스턴스 오른쪽 클릭 > connect > A standalone SSH client 선택
아래에 적혀있는 메뉴얼 대로 실행하면 됨.

1. terminal 오픈
2. 비밀번호 파일의 권한을 지정한다. (특정 사용자만 접근하여 읽을 수 있도록 지정하는 것)

```
chmod 400 {파일 path}
```

3. AWS에서 인스턴스의 ip와 접속 커맨드를 제공해준다.
  인스턴스의 ip에 접속하려면 id와 password가 필요한데, ubuntu가 id, aws_password.pem파일을 password로 사용한다.
  (ubuntu는 인스턴스를 작성할 때 자동으로 생성되는 id이며, ubuntu로 인스턴스를 만들지 않았다면 ec2-user 일 것)

```
// 인스턴스 접속
ssh -i "aws_password.pem" ubuntu@{인스턴스가 위치하고 있는 ip}
```

### 리눅스 인스턴스에서 웹서버 사용

apt-get: osx homebrew 같이 어떤 프로그램을 설치하도록 도와주는 프로그램

```
// apache2 설치
sudo apt-get install apache2
```

인스턴스를 누르면 페이지 아래쪽에 인스턴스에 대한 상세 내용과 함께 DNS가 표시됨.
해당 DNS로 접속하면 페이지(./var/www/html/index.html)가 보여짐.

security group에 web이 설정되어 있음. (방화벽 설정)

### EC2 AWS Marketplace (Wordpress)

AMI란, 아마존 머신 이미지(Amazon Machine Image)의 약자로, 소프트웨어 환경설정 내용, OS, 애플리케이션 서버, 애플리케이션 등이 포함된 템플릿이다.

- My AMIs : 내가 만든 인스턴스를 이미지화 한 것
- AWS Marketplace, Community AMIs : 다른 사람이 작성한 인스턴스 이미지를 다운받을 수 있는 곳

<AWS Marketplace에서 다운받은 이미지로 인스턴스 만들기 >
AWS Marketplace에서 Wordpress(HVM)을 선택 > region 선택 후 continue 클릭 > 상세 조건 선택(region, instance type, security group) > Launch with 1 click 클릭

### EC2 Scalability - Scale Up

#### 가상머신

가상머신이란, 소프트웨어로 만든 기계를 말한다.
우리가 일반적으로 사용하는 컴퓨터는 물리적 기계 위에 운영체제를 세운 것이라면,
가상머신은 일반 컴퓨터의 운영체제 위해 가상머신을 세워 새로운 운영체제를 설치해 운영한다.
ex) 맥북(mac os)에서 은행업무를 보기 위하여 가상머신으로 window를 설치하는 케이스

가상머신 : VMWare, Virtual Box, Parallels

start-up : 저렴한 인스턴스를 생성해서 사용할 수 있음 (물리적인 컴퓨터를 쪼개서 가상머신을 설치)
대기업 : 스펙이 좋은 인스턴스를 생성해서 사용할 수 있음 (물리적인 컴퓨터 여러대를 연결하여 가상머신을 설치)

한대의 컴퓨터에 딱 맞는 프로그램을 만든다면 직접 컴퓨터에 설치하는 것이 비용이나 처리 측면에서 효율적일 수 있다.
하지만 위의 케이스처럼 여러대의 컴퓨터를 사용해야 한다던지 한다면, 클라우드 컴퓨팅을 사용하는 것이 더 낫다.
클라우드 컴퓨팅 모델은 수요에 따라서 빠르게 대응할 수 있다.

#### Scale Up

인스턴스의 수요가 변화하면 그에 맞추어서 자동으로 Scale Up을 하거나 Scale Down을 한다.
인스턴스의 수요 : 유저 접속 수 (트래픽)

Scale Up : 더 좋은 스펙의 컴퓨터로 교체하는 것
Scale Down : Scale Up의 반대

#### 스트레스 테스트 준비

```
// 부하 발생기 다운로드
sudo apt-get install apache2-utils
```

#### 스트레스 테스트 시작

ab : apache bench라는 프로그램을 실행하겠다
-n : 몇명이 접속할 것인가
-c : 동시접속
접속주소 : 접속할 주소의 URL, 뒤에 꼭 슬래쉬를 붙여줘야 함

```
ab -n 400 -c 1 {접속 주소}/
```

부하가 커질 수록(트래픽이 높아질수록) 처리속도가 느려지는 것이 확인 되었다. (프로그램의 퀄리티가 떨어짐)

#### Elastic IP

AWS에서 Public IP는 인스턴스를 껐다 다시 켜면 변화한다.

Elastic IP란, 고정 아이피를 말한다.
Elastic IP를 부여받으면 IP가 변화하는 문제를 해결할 수 있다.
Elastic IP는 유료임!!

- Elastic IP 생성 : Elastic IPs > Allocate New Address
- Elastic IP 부여 : Elastic IPs 오른쪽 클릭 > Associate Address > 인스턴스 선택 > Associate
- Elastic IP 해제 : Elastic IPs 오른쪽 클릭 > Release Addresses

### EC2 Scalability - Scale Out (ELB)

#### Scale Out 이란?

Scale Out 이란, 여러 대의 컴퓨터가 서로 협력해서 목표를 달성하는 것을 말한다.

#### Scale Out의 흐름

일반적인 웹 애플리케이션은 다음과 같은 흐름으로 진행된다.
Web Server -> Middle Ware(웹 애플리케이션이 동작하는 logical한 부분을 담당) -> Database

Scale Out에서는 이러한 흐름 가운데 일부를 떼어내 다른 컴퓨터에서 수행한다.
예를 들어, 다음과 같이 말이다.

- 컴퓨터 A : Web Server -> Middle Ware
- 컴퓨터 B : Database

사용자의 입장에서는 바뀐 점이 없지만, 이렇게 함으로서 컴퓨터의 입장에서는 Scalabiltiy가 좋아졌다.
협동해서 일하기 때문에 성능상으로 더 좋아졌지만 복잡해졌다는 단점이 있다.

ex) Database의 속도가 느려졌다면, Database Server를 더 늘리면 된다.

- 컴퓨터 A : Web Server
- 컴퓨터 B : Middle Ware
- 컴퓨터 C : Database
- 컴퓨터 D : Database

ex) 이번엔 Middle Ware에서 속도가 느려졌다면, Middle Ware를 더 늘리면 된다.

- 컴퓨터 A : Web Server
- 컴퓨터 B : Middle Ware
- 컴퓨터 C : Middle Ware
- 컴퓨터 D : Database
- 컴퓨터 E : Database

다만 Web Server는 여러개로 늘릴 수 없다.
단일 DNS, 단일 IP로 이용자가 접속할 수 없기 때문이다. (DNS는 전화번호부와 같아서 DNS로 검색하여 연결되어 있는 IP를 찾아내 접속한다.)
하지만, DNS 서버의 설정을 변경해서 특정 이용자가 접속했을 때는 특정 IP로 접속하게끔 해서 Web Server를 확장할 수 있다.

ex) DNS 서버의 설정을 변경해 복수개의 IP와 연결을 했다면

- DNS 두개의 IP와 연결
- 컴퓨터 A : Web Server / 첫번째 IP (UserId : ~5000)
- 컴퓨터 B : Web Server / 두번째 IP (UserId : 5001 ~)
- 컴퓨터 C : Middle Ware
- 컴퓨터 D : Middle Ware
- 컴퓨터 E : Database
- 컴퓨터 F : Database

Load Balancer를 사용해서 복수의 Web Server에 부하를 분산시킬 수 있다.
이때 유저가 접속하는 IP는 Load Balancer의 IP임.

#### ELB 사용시 주의 사항

ELB란, Elastic Load Balancer의 약자이다.

예를 들어 ELB를 통해 다음과 같은 흐름으로 작업이 수행된다고 해보자.
ex)
ELB -> 컴퓨터 A (Web Server -> Middle Ware -> Database)
ELB -> 컴퓨터 B (Web Server -> Middle Ware -> Database)

유저 A는 ELB에 의해 컴퓨터 A에 접속하여 글을 남겼고,
유저 B는 ELB에 의해 컴퓨터 B에 접속하여 글을 남겼다.

여기서 문제는 컴퓨터 A와 B는 같은 애플리케이션인데 입력한 값이 각기 달리 표시된다는 점이다. (다른 Database를 가지고 있기 때문에)
Scale Out을 사용하여 Database를 따로 분리하여 컴퓨터 A와 B가 단일 Database를 바라보도록 하면 문제는 해결된다!

ex)
ELB -> 컴퓨터 A (Web Server -> Middle Ware) -> 컴퓨터 C (Database)
ELB -> 컴퓨터 B (Web Server -> Middle Ware) -> 컴퓨터 C (Database)

### EC2 Scalability - Auto Scaling

#### Amazon EC2 AutoScaling 소개
AutoScaling은 트래픽이 늘어나면 자동으로 컴퓨터를 생성해서 사용하다가, 트래픽이 낮아지면 컴퓨터를 삭제하여 과금이 물리지 않도록 하는 기능이다.

ELB에 인스턴스를 붙일 때도 이미지를 인스턴스화 해서 붙였듯이 AutoScaling도 동일하게 이미지를 인스턴스화 하여 붙인다.

* Launch Configurations : 인스턴스를 이미지로 생성하는 기능
* Auto Scaling Groups : Auto Scaling 정책에 의해서 컴퓨터를 생성하는 기능

AWS 내에서 다음과 같은 흐름으로 Launch Configurations을 지정한다.

1. Create Launch Configuration 클릭
2. Auto Scaling에 사용할 이미지를 선택한다. (My AMIs : 내가 생성한 이미지들) 
3. Name 지정 
4. 저장장치 크기 지정 
5. Security Group 지정 (해당 컴퓨터에 접속할 수 있는 네트워크 그룹) 
6. 지정한 내용 review 
7. 비밀번호 지정

#### AutoScaling(Launch Configuration) 생성

AutoScaling에서는 두가지의 핵심 설정이 있다.
첫번째, 자동으로 만들어지는 인스턴스는 어떤 이미지를 기반으로 하여 만들어지는가 (Launch Configurations)
두번째, 언제 자동으로 만들어질 것인가 (Auto Scaling Groups)

다음과 같은 흐름으로 Auto Scaling Groups 지정한다.

1. Create Auto Scaling Group 클릭 (앞서 설정한 인스턴스를 어떠한 조건에서 자동으로 생성할 것인지 지정한다.)
2. Group name 지정
3. Group size 지정 (처음에 몇개의 인스턴스로 시작할 것인가)
4. Subnet 지정 (특정 지역 내 가용구역을 지정하는 것인다. 인스턴스를 생성하면 해당 가용구역 내에 생성된다.)
5. Advanced Details > Load Balancing (어떤 ELB에 붙여서 사용할 것인지 지정)
6. Next: Configure Scaling Group 클릭
7. 인스턴스의 숫자 유지 방법 선택

- Keep this group at its initial size
  ex) Group size를 10으로 지정했는데, 인스턴스 10개 중에서 1, 2개가 죽어버렸다.
  Keep this group at its initial size를 선택하면 Group size에서 지정한 인스턴스 갯수 10개를 유지한다.

- Using scaling policies to adjust the capacity of this group
  컴퓨팅의 필요에 따라서 인스턴스를 늘리고 줄인다. (지정한 스케일 범위 내에서)

* Increase Group Size : Auto Scailing을 사용할 때 어떤 때에 인스턴스를 증가시킬 것인가를 지정하는 정책
  create alarm : 특정 상황에서 알람이 울리도록 설정. ex) CPU 점유율이 60% 이상일 때, 알람 설정
  take the action : 특정 상황에서 실행하도록 설정. ex) CPU 점유율이 60% 이상일 때, 인스턴스 1개 더 생성

* Decrease Grop Size : 어떤 때에 인스턴스를 감소시킬 것인가를 지정하는 정책
  create alarm : 특정 상황에서 알람이 울리도록 설정. ex) CPU 점유율이 30% 이하일 때, 알람 설정
  take the action : 특정 상황에서 실행하도록 설정. ex) CPU 점유율이 30% 이하일 때, 인스턴스 1개 삭제

8. Next : Configure Scaling Notifications 클릭

- Send a notification for : 알람 목적?을 기재
- With these recipients : 어디로 알람을 받을 것인지 이메일 지정
- Whenever instances : 언제 이 상태를 통보받을 것인지

9. Create Auto Scailing Group 클릭

## AWS를 제어하는 방법

AWS 컴퓨터를 제어하는 방법에 다음과 같은 것들이 있다.
Console, CLI, SDK, API

- Management Console : GUI(Graphical User Interface) 방식, 직관적이고 눈에 보이는 대로 사용하면 됨.

- CLI (Command Line Interface) : 명령어를 사용해 terminal에서 컴퓨터를 제어

- SDK (Software Development Kit) : AWS를 프로그래밍적으로 제어하기 편리하도록 제공되는 라이브러리들을 의미함.
  언어별로 다양한 라이브러리를 제공하고 있기 때문에 자신에게 맞는 라이브러리를 선택해서 사용하면 된다.
  JavaScript, Python, Java, Ruby 등등 다양한 프로그래밍 언어로 AWS 인프라 제어가 가능하다.

- API (Application Programming Interface) : 웹을 통해서 AWS를 제어하는 방식. 특정 언어를 가리지 않고 수행할 수 있음.
  AWS 서버를 켜두고 API(AWS에서 제공함)를 실행시키면 XML 형태로 값이 반환됨. 해당 값을 분석하여 사용할 수 있음.
  직접 이용하기에는 상당히 복잡하고 불편함.

## AWS의 스토리지 서비스

- EBS : EC2와 연결해서 사용하는 SSD 같은 서비스로 Block Device라고도 한다.
- S3 : 드롭박스처럼 파일 업로드 / 다운로드가 가능한 인터넷 저장 서비스

## AWS S3

S3는 AWS의 파일서버 서비스로, Simple Storage Serivce의 약자이다.
객체 저장소(Object Storage)로 파일 단위로 저장한다.
파일을 저장하는 서비스라고 간단하게 이해해도 된다.
99.999999999% 내구성(데이터가 안전하게 저장되는지)을 가지고 있으며, 높은 가용성(서비스가 항상 사용 가능한지)을 가진다.

### S3 콘솔을 통한 기본 조작 방법

Bucket 생성
* 버킷이란? S3의 최상위 컨테이너이며, 파일을 담는 그릇이라고 생각하면 된다.

1. Create Bucket 클릭 (버킷은 컴퓨터의 하드디스크나 SSD와 같은 저장장치를 말한다.)
2. Bucket Name, Region을 설정
   - Bucket Name : AWS 전체에서 지정하지 않은 이름을 사용해야 함. 유니크 해야 함.
   - Region : 서비스 하고자 하는 지역과 가까운 곳에 지정하는 것이 좋음.
3. 폴더 만들기
4. 폴더에 파일 업로드 (클라우드 저장소 이기 때문에 자유롭게 파일을 업로드, 다운로드 하면 됨.)

Bucket에 파일 업로드

1. Update 클릭
2. Add Files 클릭

업로드 된 파일을 클릭하면 오른쪽에 파일의 상세 정보가 표시된다.
업로드 한 파일을 public으로 설정을 하면 객체 URL이 제공된다. 해당 URL로 외부에서 해당 파일로 접속이 가능하다.
Link : 외부에서 해당 파일에 접속가능한 URL이다. (접속가능 권한을 주어야 접속이 가능함.)

### S3 장점

1. 내구성
   파일이 유실되지 않고 저장되므로 중요한 데이터를 저장할 수 있다.
   데이터가 여러 시설과 각 시설의 여러 디바이스에 중복 저장된다.

2. 저렴한 비용
   사용하는 만큼 비용을 내면 되기 때문에 진입장벽이 낮다고 할 수 있다.
   자주 사용하는 파일 혹은 거의 사용하지 않는 파일은 각각에 맞는 비용 정책을 설정하여 저렴한 비용으로 저장할 수 있으며,
   저작권 등의 이유로 예를 들어 5년간 저장하고 삭제해야 되는 파일 등은 다른 타입의 저장 방식을 사용하여 저렴한 비용 정책을 적용할 수 있다. (수명 주기 관리)

3. 응시 가능
   파일이 서비스 되는 기간은 연중 아주 짧은 시간을 제외하고 어느 때 가능하다.

4. 보안
   파일을 주고받을 때 SSL을 통해 데이터 전송과 데이터 업로드 후 자동 암호화를 지원한다.

5. 확장 가능
   S3에 파일을 올려도 S3 서버가 죽거나 할 가능성이 낮기 때문에 걱정하지 않아도 된다는 뜻이다.

6. 이벤트 알림 전송
   S3에 파일을 업로드 하면 다른 서비스에 이를 알려서 동작할 수 있도록 하는 기능이 있다. (트리거의 역할)
   스토리지와 연계된 다른 프로그램과 자동화 할 수 있다.

7. 고성능
   AWS의 리전을 선택해서 데이터를 빠른 시간에 전송할 수 있다.
   Amazon CloudFront을 통해 컨텐츠를 사용자에게 더 빨리 배포하도록 지원한다.
   Amazon CloudFront는 CDN(Content Delivery Network)이라고도 한다.

   AWS의 전세계 Region보다 더 많은 edge location라는 것이 있다.
   edge location에 설치되어 있는 각각의 컴퓨터로 S3에 접속해 파일을 전송한다.
   사용자들이 접속했을 때 S3에서 직접 사용자에게 서비스를 제공하는 것이 아니고 그 사용자에게 가장 가까운 컴퓨터에 저장되어 있는 파일을 서비스 한다는 뜻이다.
   지연시간이 가장 낮은 엣지 로케이션으로 요청이 반환되므로 최고의 성능으로 서비스를 제공한다.

### S3의 용도

1. 컨텐츠 저장 및 배포
  웹에서 사용자들이 업로드한 파일을 저장하고, 다운로드 할 파일을 내려준다.

2. 빅 데이터 분석
  빅 데이터를 분석하기 위해서는 거대한 파일을 빠르고 안전하게 보관할 필요성이 있다.
  S3는 그런 역할을 하는 저장장치를 제공한다.

3. 클라우드 네이티브 애플리케이션 데이터

4. 재해 복구
  백업 저장장치로도 사용할 수 있다.
  
## AWS RDS

RDS는 관계형 데이터베이스를 제공하는 서비스로, Relational Database Service의 약자이다.
MySQL, MariaDB, PostgreSQL, SQL Server, ORACLE 등을 직접 운영하지 않고 AWS에 대행할 수 있다.

### RDS 소개

Relational Database를 직접 설치해서 사용하는 것은 그렇게 어렵지 않을 수도 있다.
하지만 데이터가 늘어나고, 사용량이 늘어나면 DB를 안정적으로 유지하고 관리하는 것이 어려워진다.
AWS에서는 이러한 기능을 위임하여 관리해 주는 서비스를 제공하는데 이를 RDS라고 한다.

대표적인 관계형 데이터 베이스

- MySQL : 무료, Oracle에서 유지보수
- MariaDB : MySQL 창업자가 만든 DB, MySQL과 호환 됨
- Aurora : AWS에서 직접 만든 DB, MySQL과 호환 됨, 개발된 기간이 길지 않음
- PostgreSQL
- Oracle
- SQL Server : 마이크로소프트 사에서 개발

### RDS 서버 생성

지역을 선택을 하고 서버를 생성하는 것임.

1. Launch DB Instance 클릭
2. DB 선택 (MariaDB)
3. DB Purpose 선택

비용의 차이가 있음.

- Production : 배포용, 데이터가 서로다른 데이터 센터에 저장됨. 어느 한쪽 가용구역이 문제가 생겨도 다른 쪽의 데이터 센터를 통해 서비스를 제공할 수 있음
- Dev/Test : 개발용, 가용구역 서비스를 제공하지 않음

4. Specify Database Details 지정
5. Configure Advanced Settings 지정
6. Database Options, Backup 지정
7. Launch DB Instance 클릭

DB Instance는 일반 EC2보다 생성되는데 시간이 좀 걸림

### RDS 백업 & 복원

- Take Snapshot
 (DB 인스턴스를 오른쪽 클릭하여 해당 기능을 실행할 수 있다.)
 현재 상태의 DB 인스턴스를 얼려두어 어딘가에 두는 것이다.
 장애 발생 시, Snapshot을 찍어뒀을 때의 상태로 복원될 수 있다.

- Restore DB Instance
 snapshot을 오른쪽 클릭하여 실행.
 복원을 실행하면 새롭게 DB Instance가 실행된다.
 기존의 장애가 발생한 DB 인스턴스와 복원된 DB 인스턴스 2가지가 되는 것이다.

- Restore to Point in Time
 snapshot을 오른쪽 클릭하여 실행.
 어떤 특정한 시점으로 복원하는 기능이다. 특정 시점의 백업 데이터를 불러오는 것이다.

### RDS Scale up & out

Scailablity 는 두가지 전략을 가지고 있다.

- Scale Up : 데이터 베이스에 접속이 늘었을 때 컴퓨터의 성능을 강력하게 만들어 처리할 수 있도록 하는 것.
- Scale Out : 접속이 너무 많이 늘다보면 컴퓨터 한대로 처리하기에 한계에 도달하는 경우가 있음. 이럴 때 여러 대의 컴퓨터에 처리를 분산하여 수행하도록 함.

데이터베이스는 두가지 작업을 한다.
읽기 : select (데이터에 변화가 없음)
쓰기 : insert, update, delete (데이터에 변화가 있음)

Slave 1 : 읽기 , 많은 경우 쓰기보다 읽기를 더 많이 수행하므로, 여러 Slave DB에서 읽기 작업을 수행하는 것이 속도가 빠름.
Slave 2 : 읽기
Slave 3 : 읽기
Master : 쓰기, Master의 데이터가 변화하면 Slave에 해당 내용을 반영하는 동기화의 속성을 가지고 있음.

Sharding
id가 1~100번까지는 A 데이터를 제공, 100~200번까지는 B 데이터를 제공... 등등 데이터를 쪼개서 제공하는 기능을 말한다.
상당히 복잡하고 어려운 개념임.

DB Instance를 클릭하고 Instance Actions를 선택.
Create Read Replica를 선택.


## AWS Route 53
AWS에서 제공해주는 DNS 서비스
저렴하고 100% 가용성을 보장해준다. (다운되지 않는다!)

CF(Cloud Front) : AWS에서 제공하는 CDN 서비스 중 하나.
CDN(Content Delivery Network) : 전세계 컨텐츠(동영상, 이미지등)를 제공해주는 서버
PoP(Point of Presents) : 전세계에 흩어져 있는 작은 인프라 센터들이 CDN을 구성하고 있음.

## AWS VPC(Virtual Private Cloud)
AWS에서 서비스를 개발 및 제공하기 위한 가상 사설 네트워크
하나의 서비스에 하나의 VPC로 시작
VPC는 인터넷과 연결됨
VPC는 다시 용도에 따라 subnet으로 나눔
각각의 subnet 에서 웹 서버, DB 등이 연결됨
Public subnet : 웹 서버, 메일 서버 등
private subnet : 데이터베이스, 보안 데이터, 백업 데이터 등 

## AWS 주요 서비스들

* 계정관리
- IAM : 어떤 이용자에게 어떤 권한을 줄지 설정

* 컴퓨팅
- EC2 : 서버
- Lambda : 서버리스 플랫폼, 서버가 없이 서버가 있는 것처럼 사용할 수 있게 해 줌, 서버 관리의 부담을 줄여줌
- ECS : 도커와 컨테이너를 사용할 수 있게 해주는 플랫폼 

* 네트워크
- VPC
- Routee53
- CloudFront (CDN) : 이미지나 동영상 같은 컨텐츠를 전세계에 빠르게 전송할 수 있도록 하는 기능. ex) 넷플릿스, 왓챠...

* 저장 : S3

* 데이터베이스
- RDS

* 모니터링
- CloudWatch
- CloudTail

* 기타
- SNS (Simple Notification Service) : SNS 알림 서비스
- SES (Simple Email Service) : 이메일 알림 서비스 
- SQS (Simple Queue Service) : 큐 알림 서비스 
- CloudFormation : DevOps를 쉽게 할 수 있도록 도와주는 서비스
