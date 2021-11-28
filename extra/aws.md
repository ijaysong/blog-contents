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

### IAM Policy의 종류
- AWS 관리 정책 : AWS가 미리 만들어 놓은 정책으로 사용자는 편집 불가능
- 사용자 관리 정책 : 사용자가 직접 생성한 정책으로 기존 정책으로부터 생성, 수정, 직접 생성 가능 / GUI 편집기 혹은 JSON 편집기 모두 사용 가능
- Inline 정책 : 1회성 정책

< AdministratorAccess Policy >
~~~
{
   "Version": "2012-10-17",
   "Statement": [
       {
           "Effect": "Allow",
           "Action": "*",
           "Resource": "*"
       }
   ]
}
~~~
=> 모든 자원에 대한 모든 행동이 허용된다.

< Power User Policy >
~~~
{
   "Version": "2012-10-17",
   "Statement": [
       {
           "Effect": "Allow",
           "NotAction": "iam:*",
           "Resource": "*"
       }
   ]
}
~~~
=> 모든 자원에 대한 iam의 액션이 거부된다. (iam 유저의 패스워드 변경마저 안된다는 단점이 있음)

< S3 Full Permission >
~~~
{
   "Version": "2012-10-17",
   "Statement": [
       {
           "Effect": "Allow",
           "Action": "s3:*",
           "Resource": "*"
       }
   ]
}
~~~
=> 모든 자원에 대한 S3와 관련된 액션만 허용된다. (ec2, rds 등등의 다른 서비스는 사용할 수 없다)

예시) 직접 작성한 Policy

< S3 특정 버킷 읽기 전용 정책 >
~~~
{
   "Version": "2012-10-17",
   "Statement": [
       {
           "Effect": "Allow",
           "Action": [
               "s3:Get*",
               "s3:List*"
           ],
           "Resource": [ "arn:aws:s3:::mydata", "arn:aws:s3:::mydata/*" ]
       }
   ]
}
~~~
=>  AWS S3의 mydata 버킷과 mydata/*에 저장된 데이터에 대한 읽기 전용(Read Only) 액션만 허용된다.

## IAM Role
특정 개체(IAM 사용자, AWS 서비스, 다른 계정, AWS 관리 계정)에게 리소스의 접근 권한을 부여하기 위해 사용
임시 자격 증명(Short Term Credential)이라고도 한다.
주로 AWS 서비스들이 직접 다른 AWS 서비스를 제어하기 위해 사용한다.
사용자나 응용 프로그램에서 일시적으로 AWS 리소스에 접근 권한을 얻을 때도 사용한다.

### IAM Role의 구성요소
- Role ARN : 역할을 호출하기 위해 필요, role을 식별할 수 있는 주소
- IAM Policy : 이 역할이 어떤 권한을 부여할 수 있는가
- 신뢰관계 : Role을 아무나 사용하면 안된다. 어떤 개체가 IAM Role을 호출할 수 있는가, assume 할수 있는가
- 그 외 유지 시간, 이름 등도 필요

### IAM Role 사용예
EC2 role
- EC2 인스턴스에게 AWS 서비스 접근 권한을 부여
Lambda Execution Role
- 람다에서 S3로부터 파일을 읽고 싶을 때 role에 권한 지정
- 다른 계정의 사용자에게 내 계정의 DynamoDB에 임시 접근 권한 부여
- 안드로이드 앱이 S3로 직접 동영상을 업로드할 때 사용

ARN(Amazon Resource Name) : 아마존에서 리소스를 유일하게 식별할 수 있는 구분자
~~~
arn:partition:service:region:account-id:resource-id
arn:partition:service:region:account-id:resource-type/resource-id
arn:partition:service:region:account-id:resource-type:resource-id
~~~
- partition : aws 밖에 없음
- region : 글로벌 서비스의 경우 생략 가능 ex) iam, s3
- account-id : 계정과 관계 없는 서비스의 경우 생략 가능

ex)
~~~
arn:aws:iam::123456789012:user/honux
Arn:aws:s3:::my-bucket/folder1/file1
~~~

### Switch Role 만들기
IAM > 역할 > 역할 만들기 클릭
- 신뢰할 수 있는 유형의 개체 선택
- 이 역할을 사용할 수 있는 계정 ID 지정
- 정책 연결

IAM > 역할 > 신뢰관계 편집 클릭
~~~
{
   "Version": "2012-10-17",
   "Statement": [
       {
           "Effect": "Allow",
           "Principal": {
               "AWS": "arn:aws:iam::123456789012:user/aws-tester1"
           },
           "Action": "sts:AssumeRole",
           "Condition": {}
       }
   ]
}
~~~
- principal : iam 계정인 aws-tester1의 arn을 등록함으로서 해당 role에 대해서 신뢰할 수 있는 개체임을 등록한다.

### Switch Role 사용하기
우 상단에서 계정명을 클릭하면 role 전환 버튼이 있다.
신뢰관계로 등록된 계정이라면 작성한 policy를 assume하여 switch role을 할 수 있다.
반면에 등록이 안된 계정이라면 switch role을 할 수 없다.
동일한 방법으로 role 전환을 해제할 수 있다.
맨위로



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

#### Multi AZ란?
둘 이상의 AZ를 활용해서 서비스를 구축하는 것이다.
두 대 이상의 서버가 필요하다.
주로 ELB(Elastic Load Balancer)를 이용해서 서버를 연결해서 사용한다.

## AWS EC2

EC2(Elastic Compute Cloud)는 독립된 컴퓨터를 임대해주는 서비스이다.

### EC2 관련 서비스들
1. EC2
- 서버, CPU에 해당한다.

2. EBS (Elastic Block Storage)
- EC2의 블록 저장장치, SSD, AZ 서비스

3. VPC (Virtual Private Cloud)
- EC2가 연결되는 사설 네트워크 망
- 리전 기반

4. Subnet
- VPC의 하위망
- AZ 서비스로 EC2sms subnet에 위치함

5. ENI (Elastic Network Interface)
- 가상 네트워크 인터페이스, 렌카드, AZ 서비스

6. Security Group
- EC2의 방화벽, 포트 접근 제어

7. ELB (Elastic Load Balancer)
- 트래픽 분산을 위해 사용

8. Auto Scaling
- EC2의 확장성을 위해 제공되는 서비스
- 매우 유명!!

9. EBS Snapshot
- EBS의 백업 데이터

10. AMI (Amazon Machine Image)
- EC2의 백업 이미지
- EC2를 시작할 때 사용
- AWS에서 제공하는 AMI를 이용해서 EC2 시작
- 사용자가 원하는 시점에 AMI를 생성하고 이를 통해 EC2 시작 가능

## EC2 생성 및 삭제

인스턴스란, 컴퓨터 한대라고 이해하면 된다. ex) 3대의 컴퓨터를 임대했다 == 인스턴스 3개를 만들었다.
원래대로라면 컴퓨터를 구매하고 설치했어야 할 과정이지만 단 1분만에 인스턴스를 만들 수 있다.
또한, 원격제어로 접속하여 미국 캘리포니아에 설치한 인스턴스를 내 자리에 있는 컴퓨터처럼 사용할 수도 있다.

< 인스턴스 생성 방법 >
1. (1단계) AMI: Amazon Machine Image 선택 ex) Amazon Linux, Ubuntu Server...

2. (2단계) 인스턴스 유형 선택
- 사용 사례에 맞게 컴퓨팅 요건이 맞는 인스턴스 유형을 선택한다

3. (3단계) 인스턴스 세부 정보 구성
- 인스턴스 갯수 설정 ex) 1개
- 구매 옵션 ex) 스팟 인스턴스 : 경매 방식으로 가격을 매기는 것
- 네트워크(vpc)
- 서브넷 : az 갯수 만큼 존재함
- 퍼블릭 IP 자동 할당 : 활성화 하지 않으면 ssh에 접속할 수 없음
- 고급 세부 정보 > 사용자 데이터 : EC2가 생성될 때 한번만 실행되는 script를 작성할 수 있음 (EC2 생명 주기 동안 딱 한번만 실행 됨)

4. (4단계) 스토리지 추가
- 크기(GB)
- 볼륨 유형

5. (5단계) 태그 추가
반드시 추가해야 하는 것이 `Name` 태그 임!
서버에 스티커를 붙이는 느낌으로 DevOps 할 때 편하게 사용할 수 있따.
- 키 ex) Name, Environment, Team
- 값

6. (6단계) 보안 그룹 구성
어떤 IP에 어떤 포트를 열어줄지 지정하는 것

7. (7단계) 인스턴스 시작 검토
지정한 내용을 최종적으로 review한다.
launch 버튼 클릭하면 기존 키 페어 선택 또는 새 키 페어 생성을 시작할 수 있다.
key pair name을 지정하면 비밀번호가 파일로 다운받아지는데, (새로 만든 인스턴스에 접속하기 위한 비밀번호를 지정하기 위한 것임.)
비밀번호를 잃어버리면 영영 해당 EC2에 접속할 수 없다.

< 인스턴스 일시 중지 및 삭제 방법 >
아주 간단하게 인스턴스를 일시 중지 혹은 삭제할 수 있으며, 과금이 되지 않는다.
- 중지
 - 컴퓨터를 끈 것과 동일한 상태
 - 중지 중에도 디스크나 서버는 남아있으므로 요금이 부과된다.
 - 중지 후 재시작하면 IP가 변경된다. (고정 IP가 필요하다면 Elastic IP를 사용하자)
- 종료
 - 서버를 완전 삭제한 상태

1. EC2 > 삭제할 인스턴스 선택 > 오른쪽 클릭 > instance status > stop / terminate 선택
2. EC2 > 삭제할 인스턴스 선택 > 인스턴스 상태 comboBox > 인스턴스 중지 선택

#### Mac 및 Linux에서 ssh로 접속하기
1. ssh 클라이언트를 연다

2. 프라이빗 키 파일을 찾는다. 키에 접속할 수 있도록 권한을 준다.
~~~
chmod 400 pem파일.pem
~~~

3. 퍼블릭 DNS를 사용하여 인스턴스에 연결한다.
~~~
ssh -i pem파일.pem ec2-user@public-ip
~~~

cf) 연결이 안된다면 다음 두가지를 확인해보자!
- public IP가 열려 있어야 한다.
- 보안 그룹의 인바운드 규칙에 SSH가 등록 되어 있어야 접속된다

#### Windows에서 ec2 접속하기

두가지 방법이 있다.
첫번째 방법은 mac에서 ec2에 접속하는 것과 동일하다.

1. ssh 클라이언트를 연다
2. 프라이빗 키 파일을 찾는다. 키에 접속할 수 있도록 권한을 준다.
3. 퍼블릭 DNS를 사용하여 인스턴스에 연결한다.

두번째 방법은 putty를 사용해서 Windows에서 Linux 인스턴스에 접속하는 것이다.
putty.exe와 puttygen.exe 파일을 다운 받아야 한다.
puttygen을 통해서 pem파일을 putty가 사용할 수 있는 형식으로 변환한다.

1. puttygen을 실행시킨다.
- gem 파일을 import하여 save private key를 실행한다. (pem파일.pem -> pem파일-ppk.ppk)

2. putty에 접속 정보를 입력하고, ppk 파일을 연결한다.

3. 저장 후, 실행하면 된다.
 
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

### EC2 Role
EC2 인스턴스가 다른 AWS 리소스를 제어할 때 사용하는 IAM Role
EC2 안에서 CLI 설정처럼 할 수 있지만, EC2 Role을 사용하는게 더 안전하다.
EC2 Role을 사용하기 위래서 추가적인 IAM 권한이 필요하다.

1. EC2 Role을 생성한다. ex) ec2-s3-full

2. AWS 사용자가 EC2 Role을 연결할 수 있도록 IAM Policy를 통해 권한을 부여한다.
admin 유저만 IAM 권한에 접속할 수 있는 권한이 있는데, 그러면 매번 admin으로 접속해서 해야해서 너무 불편하니
개발자 유저들도 EC2 Role을 더할 수 있는 권한을 부여한다.

EC2 Role을 추가하고 확인할 수 있는 권한.
개발자 유저 IAM policy에 추가해줄 것.
~~~
{
 "Version": "2012-10-17",
 "Statement": [
   {
     "Sid": "VisualEditor0",
     "Effect": "Allow",
     "Action": [
       "iam:PassRole",
       "iam:ListInstanceProfiles"
     ],
     "Resource": "*"
   }
 ]
}
~~~

3. EC2 인스턴스에 EC2 Role 연결

### EC2 유형 변경
- 실행 중일 경우, 유형 변경 불가능
- 중지 상태에서는 유형 변경 가능
- 보안 그룹은 실행 중에도 추가 변경 삭제 가능
- EC2 Role도 실행 중 변경 가능
- key-pair는 변경 불가능

### EC2의 상태와 요금 과금 정책
- 시작 : 처음 ec2를 생성함
- 실행 중 : 현재 서버가 동작 중인 상태. EC2 요금 + EBS 요금 과금
- 정지 : 정지되면 EC2 요금은 나오지 않지만 EBS 요금이 과금됨
- 종료 : 생성된 EC2가 완전히 사라진 상태, 기본 옵션으로 EBS도 함께 사라짐.

### EC2가 종료되었는데 과금이 되었다면?
- Elastic IP가 남아있는지 확인 할 것
- EBS 스냅샷이 남아있으면 과금이 된다. (S3 요금)
- AMI가 있다면 역시 과금이 된다. (S3 요금)
- AMI를 제거해도 스냅샷은 남아있는 경우가 많으므로 주의할 것

## VPC
### VPC 란?
- Amazon Virtual Private Cloud
- AWS의 가상 사설 네트워크
- EC2의 네트워크 계층이며, 많은 AWS 서비스들이 VPC를 통해 네트워크에 연결된다.

### VPC 핵심 개념
- VPC : 사용자의 AWS 계정 전용 가상 네트워크 망, 리전 서비스
- 서브넷 : VPC를 더 작은 범위의 네트워크로 나눈 것, AZ 서비스
- EC2 인스턴스는 반드시 서브넷에 연결된다. (EC2 인스턴스도 AZ 서비스이기 때문에 같은 AZ에 연결되어야 한다.)
- 라우팅 테이블 : 네트워크 트래픽 전달 규칙 지정
- CIDR 블록 : CIDR 표기법을 통해 IP 주소 범위를 지정

### CIDR 표기법
- IP의 범위를 간단하게 표기하는 표기법
IP address / prefix
ex)
0.0.0.0/0
10.2.0.0/16
192.168.1.0/24

- prefix의 범위는 0 ~ 32이고 의미는 상위 고정 비트(지정된 비트만큼 값이 고정된다.) 또는 네트워크 파트를 의미한다.
- 고정되지 않은 하위 비트가 호스트 비트이며 범위값을 갖는다.
- 하위 비트(가변 부)의 값은 모두 2진수 0으로 채워져야 한다.

ex1) 0.0.0.0/0
상위 고정 비트 (네트워크 비트) : 없음
하위 비트 (호스트 비트) : 0.0.0.0

ex2) 10.2.0.0/16
상위 고정 비트 (네트워크 비트) : 10.2
하위 비트 (호스트 비트) : 0.0 (10.2.X.X)

ex3) 192.168.1.0/24
상위 고정 비트 (네트워크 비트) : 192.168.1
하위 비트 (호스트 비트) : 0 (192.168.1.X)

- CIDR 블록이 가지는 IP 범위 개수 = 2 ^ (32 - prefix)

#### CIDR 표기법 예제
ex1) 0.0.0.0/0
- 고정 비트 : 0 bit
- 가변 비트 : 32 bit
- 범위 : 0.0.0.0 ~ 255.255.255.255
- 의미 : IP 전체 (Any Address)

ex2) 52.38.6.4/32
- 고정 비트 : 32 bit
- 가변 비트 : 0 bit
- 범위 : 52.38.6.4
- 의미 : 특정 주소 하나의 IP

ex3) 10.5.0.0/16
- 고정 비트 : 16 bit
- 가변 비트 : 16 bit
- 범위 : 10.5.0.0 ~ 10.5.255.255
- 의미 : 2^16 개의 IP 범위

ex4) 10.5.1.0/24
- 고정 비트 : 24 bit
- 가변 비트 : 8 bit
- 범위 : 10.5.1.0 ~ 10.5.1.255
- 의미 : 2^8 개의 IP 범위

ex5) 10.5.11.0/24
- 고정 비트 : 24 bit
- 가변 비트 : 8 bit
- 범위 : 10.5.11.0 ~ 10.5.11.255
- 의미 : 2^8 개의 IP 범위

ex6) 10.5.21.64/28
- 고정 비트 : 28 bit
- 가변 비트 : 4 bit
- 범위 : 10.5.21.64 ~ 10.5.21.79
- 의미 : 2^4 개의 IP 범위

### CIDR와 VPC 범위
- prefix는 8비트의 배수일 필요가 없다. ex) 0.5.21.64/28
- 가장 큰 범위의 prefix: 16
- 가장 작은 범위의 prefix : 28

### VPC 만들기
- AWS 관리 콘솔 > VPC > VPC 생성 > 이름과 IPv4 CIDR 블록을 지정 > VPC 생성
- AWS 관리 콘솔에 이름과 CIDR 지정으로 간단히 만들 수 있다.
- VPC를 생성하면 기본 라우팅 테이블이 하나 생긴다.
- default VPC (172.1.0.0/16) : 어떤 VPC를 지정하지 않았을 때 적용되는 default VPC 이다. 생성/삭제 가능.

### 서브넷 생성 및 라우팅 테이블 연결 확인
- 서브넷은 VPC CIDR 블록의 서브넷으로 생성한다.
- CIDR 범위를 지정하고, AZ를 지정한다.
- enable public IP 옵션을 선택할 수 있다. (중요!!!)
- 서브넷은 반드시 하나의 라우팅 테이블을 연결되어야 하고, 초기에는 VPC의 기본 라우팅 테이블이 지정된다.
- default VPC와 마찬가지로 각 AZ 별 default Subnet이 있다.
- 서브넷끼리 CIDR 블록 범위가 중첩되면 안된다.

### 인터넷 게이트웨이 생성 및 VPC 연결
인터넷 게이트웨이(IGW)를 VPC에 연결하지 않으면 VPC에서 인터넷을 할 수 없다.
대부분의 경우 IGW를 생성해서 VPC에 연결한다.
default 인터넷 게이트웨이가 존재할 것이다.
- AWS 관리 콘솔 > 인터넷 게이트웨이 > 인터넷 게이트웨이 생성
- 이름태그 지정 후 생성
- VPC에 연결 버튼 클릭 > VPC 선택 > 연결

### Public 서브넷
서브넷이 인터넷과 연결하기 위해서 라우팅 규칙이 필요하다.
1. 라우팅 테이블을 생성
2. 해당 라우팅 테이블에 인터넷을 위한 규칙을 생성
3. 지정된 서브넷과 라우팅 테이블을 연결

인터넷 게이트웨이(IGW) 규칙이 있는 서브넷을 public 서브넷이라고 한다.
인터넷 세상에 열려있다.
웹 서버, Bastion server(Jump server) 등이 위치한다.
WAS(Web Application Server)의 위치는 상황에 따라 다르지만 public 서브넷에 놓는 경우가 많다.

### 라우팅 테이블 생성
라우팅 테이블 > 라우팅 테이블 생성 (public vpc를 지정하여 생성한다.)
방금 생성한 라우팅 테이블 > 라우팅 편집
- 라우팅 룰을 추가해준다.
- 대상 : 0.0.0.0/0(모든 IP를 지정)
- 대상 : 인터넷 게이트웨이

라우팅 테이블은 위에서 아래로 처리를 한다.
위에서부터 로컬 -> 인터넷 게이트웨이 순이라면, 먼저 로컬에 해당하는 것을 처리하고 인터넷 게이트웨이로 넘어올 것이다.

### public 서브넷 라우팅 테이블 연결
public 서브넷 > 라우팅 테이블 > 라우팅 테이블 연결 편집
인터넷 게이트웨이를 추가한 라우팅 테이블을 지정해준다.

### public 서브넷 라우팅 테이블 연결 및 확인
EC2 대시보드 > 인스턴스 시작 (public 서브넷 지정 가능한 EC2 생성)
- 네트워크 : public 네트워크 지정
- 서브넷 : public 서브넷 지정
- 퍼블릭 IP 자동 할당 : 활성화

=> public 서브넷에 라우팅 테이블이 지정되어 있어야 하고,
=> 라우팅 테이블에는 인터넷 게이트웨이가 추가된 라우팅 룰이 있어야 접속할 수 있다.

### 서브넷 Public IP 자동 할당
서브넷 선택 > 작업 > 자동 할당 IP 설정 수정 > 퍼블릭 IPv4 주소 자동 할당 활성화 클릭 > 저장
해당 설정을 하면 EC2 생성 시, 퍼블릭 IP 자동 할당이 자동으로 활성화 된다.(아니면 비활성화가 default이다.)

### Private 서브넷과 NAT 게이트웨이
인터넷이 연결되지 않은 서브넷을 Private Subnet이라고 한다.
데이터베이스가 이곳에 위치한다.
라우팅 테이블에 동일한 로컬 설정이 있기 떄문에 Private 서브넷은 같은 VPC 안에 위치하는 웹 서버에 연결할 수 있다.
Private 서브넷에서 인터넷을 하려면 NAT Gateway 서비스 이용과 EC2로 직접 NAT instance 구축이 필요하다.

Private 서브넷은 외부 유저가 인터넷을 통해서 들어오는 것을 막는다.
그런데 여기서 한가지 문제가 발생한다.
데이터베이스의 소프트웨어를 설치하거나 업데이트를 할 때 인터넷이 필요하다.
그럼 어떻게 해야할까?
다음 두가지 방법으로 해결할 수 있다.

1. NAT 인스턴스
2. NAT 게이트웨이 (NAT 게이트웨이는 비싸기 때문에 가격에 주의!)

### NAT 인스턴스 설정
VPC > NAT 게이트웨이 > NAT 게이트웨이 생성
- 이름, 서브넷, elastic IP 할당

생성한 NAT 게이트웨이를 라우팅 테이블과 연결해주어야 함.
라우팅 테이블을 생성하여 라우팅 룰을 추가해준다.
- 0.0.0.0/0
- NAT Gateway

Private 서브넷에 라우팅 테이블을 적용해준다.
### EBS (Elastic Block Storage)
EBS는 EC2의 블록 저장장치이며, AZ 서비스이다.
EBS 스냅샷은 EBS의 백업 데이터로, AZ 서비스이다.
스냅샷을 이용해서 다른 AZ로 복사 가능하다.
안전하게 S3에 저장된다.
실행 중인 인스턴스에서도 생성 가능하지만, 가급적이면 정지 후에 생성하는 것이 좋다.

< EBS 스냅샷 생성 >
- EBS > 스냅샷 생성
- Select resource type : instance
- 설명 추가
- 태그 추가

< EBS 스냅샷 다른 AZ에 복사 >
- EBS > 스냅샷 > 작업 comboBox > 볼륨 생성
- 가용영역 선택
- 태그 추가

### AMI (Amazon Machine Image)
AMI란, EC2의 백업이미지이다.
EBS 스냅샷 + 메타데이터로 구성된다.
AMI도 AZ 서비스이기 때문에 AMI를 이용해서 EC2를 다른 AZ로 옮길 수 있다.

< AMI 생성 >
- 인스턴스 > 작업 comboBox > 이미지 및 템플릿 > 이미지 생성
- 이미지 이름 지정

cf) AMI를 생성하면 자동으로 EBS 스냅샷도 생성된다! 직접 생성하지 않은 EBS 스냅샷이라고 막 지우지 말 것!
cf) AMI나 스냅샷을 놔두면 프리티어가 끝나고 나서 과금되므로 삭제해줄 것!

< AMI로 인스턴스 생성 >
- 이미지 > AMI > 작업 comboBox > 시작하기
- EC2 생성 과정과 동일한 절차를 거침
- 기존에 만들어 놓은 키페어를 사용할 수 있음.

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

Elastic IP란, 고정 IP를 말한다.
Elastic IP를 부여받으면 IP가 변화하는 문제를 해결할 수 있다.
Elastic IP는 사용 중에는 무료이나, 사용하지 않을 경우 과금이 된다. (월 4000원 정도)
프리 티어 사용자가 요금을 지불하게 되는 원인 중 하나로, 사용하지 않을 경우 반드시 반납할 것!!

### EC2 Elastic IP 연결 및 해제

< EC2 elastic-ip 연결 >
1. EC2 > Elastic IP 생성

2. 탄력적 IP 주소 할당 (IP를 새로 만드는 것)

3. 작업 comboBox > 탄력적 IP 주소 연결
- 연결하고자 하는 인스턴스 선택하면 됨.

< EC2 elastic-ip 해제 >
1. EC2 > Elastic IP > 작업 comboBox > 탄력적 IP 주소 연결 해제

cf) 탄력적 IP 주소 릴리스를 하면 IP를 삭제하는 것이 됨.
그러면 운영중인 프로그램에 장애가 발생하니 주의할 것!

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
객체 저장소(Object Storage)이며, 파일 단위로 저장한다.
구글 클라우드나 네이버 클라우드와 같이 파일을 저장하는 서비스라고 간단하게 이해해도 된다.
파일 업로드, 다운로드, 검색이 가능하다.
용량이 무제한이다.

### S3의 특징
리전 기반 서비스이다.
99.999999999% 내구성(데이터가 안전하게 저장되는지)을 가지고 있으며, 높은 가용성(서비스가 항상 사용 가능한지)을 가진다.
상대적으로 빠르진 않다. -> 돈을 들이면 좀 더 빠른 속도로 쓸 수 있음ㅋㅋ
CDN과 연동 가능하다.
static web page 기능을 지원한다.
필요에 따라 버저닝(versioning) 기능이 사용 가능하다. ex) 같은 이름으로 덮어쓰기 하면 해당 파일의 버전을 저장해 둠
다양한 요금 옵션으로 비용 절감이 가능하다.

### S3 콘솔을 통한 기본 조작 방법

#### Bucket 생성
* 버킷이란? S3의 최상위 컨테이너이며, 파일을 담는 그릇이라고 생각하면 된다.

1. Create Bucket 클릭 (버킷은 컴퓨터의 하드디스크나 SSD와 같은 저장장치를 말한다.)
2. Bucket Name, Region을 설정
  - Bucket Name : AWS 전체에서 지정하지 않은 이름을 사용해야 함. 글로벌하게 유니크 해야 한다!
  - Region : 서비스 하고자 하는 지역과 가까운 곳에 지정하는 것이 좋음.
3. 폴더 만들기
4. 폴더에 파일 업로드 (클라우드 저장소 이기 때문에 자유롭게 파일을 업로드, 다운로드 하면 됨.)

cf) S3의 폴더는 일반적인 폴더가 아니다. prefix의 개념으로 이해하면 된다!

#### Bucket에 파일 업로드
1. Update 클릭
2. Add Files 클릭

업로드 된 파일을 클릭하면 오른쪽에 파일의 상세 정보가 표시된다.
S3에 업로드한 모든 파일은 객체 URL을 가진다.
업로드 한 파일을 public으로 설정을 하면 해당 URL로 외부에서 해당 파일로 접속이 가능하다.
Link : 외부에서 해당 파일에 접속가능한 URL이다. (접속가능 권한을 주어야 접속이 가능함.)

#### Bucket 및 파일 삭제
버킷 안에 파일이 들어있으면 버킷 삭제가 불가하기 때문에 파일을 먼저 삭제해주어야 한다.

1. 삭제하고자 하는 파일을 선택하고 삭제버튼을 누른다.
2. 삭제하고자 하는 버킷을 선택하고 삭제버튼을 누른다.

or
1. 삭제하고자 하는 버킷을 선택하고 비어있음 버튼을 누른다. (버킷 비우기)
2. 삭제하고자 하는 버킷을 선택하고 삭제버튼을 누른다.

#### 파일 퍼블릭 설정
버킷을 기본 옵션으로 생성하면 public으로 설정할 수 없도록 되어 있다.
버킷 퍼블릭 액세스 차단을 해제해주어야 한다.

1. 버킷 상세 설정 > 퍼블릭 액세스 차단을 위한 버킷 설정 > 모든 퍼블릭 액세스 차단 해제
2. 객체 상세 페이지 > 객체 작업 > 퍼블릭으로 설정

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

### S3 사용 예
- 클라우드 저장소 : 개인 파일 보관, 구글 드라이브처럼 사용 가능
- 서비스의 대용량 파일 저장소 : 이미지, 동영상, 빅데이터 ex) 넷플릭스
- 서비스 로그 저장 및 분석
 ex) EC2 서버의 로그를 EC2 EBS에 저장하지 말자.
   - EBS보다 S3가 더 저렴함
   - 훨씬 더 안전함
- AWS 아데나를 이용한 빅데이터 업로드 및 분석
- 서비스 사용자의 데이터 업로드 서버 : 이미지 서버, 동영상 서버
- 중요한 파일은 EC2의 SSD(EBS)에 저장하지 말고 S3에 저장하자!
- glacier(cold data / 자주 사용하지 않는 데이터)와의 연동으로 비용 절감 및 규정 준수 가능

### S3에서 권한 제어하는 법
1. ACL (Access Control List)
- 객체마다 ACL 지정 가능
- 주로 간단한 제어에 사용

2. Bucket Policy
- IAM Policy와 유사한 문법
- ACL 보다 복잡하고 세부적으로 지정 가능

3. IAM을 이용한 제어
- IAM 사용자에게 버킷 접근 권한을 주기 위해 사용

4. PresignedURL
- URL을 이용해 임시 권한을 부여하는 기능
- 매우 유용함

### ACL (Access Control List)
액세스 제어 목록이다.
다음 3 그룹의 AWS 계정에 대해 액세스 권한을 지정할 수 있다.

- 객체 소유자
- 모든 사람(퍼블릭 액세스)
- 인증된 사용자 그룹(AWS 계정이 있는 모든 사용자)

public 설정 기능도 ACL을 이용해서 권한을 제어한 것이다.
모든 S3 객체는 ACL이 있고, 이를 이용해서 개별 권한 제어가 가능하다.
맨위로


  
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
