# Home Server
생활코딩 'Home Server' 강의와
인프런 '모든 개발자를 위한 HTTP 웹 기본 지식' 강의를 듣고!

인터넷 위에 있는 컴퓨터와 컴퓨터가 서로 연결되기 위해선, IP 주소가 필요하다.

1980년대 초, IPv4라는 인터넷 통신 규약이 생겨났다.
해당 규약에서 IP 주소를0.0.0.0 ~ 255.255.255.255 범위 내에서 IP 주소를 사용하도록 결정했다. 
(해당 범위 내에선 42억개의 IP 주소가 생성될 수 있음) 

시간이 흘러 web, smartphone, cloud computing, IOT 등과 같이 정보 기술이 발달하면서
인터넷과 연결되어야 하는 전자기기가 기하급수적으로 증가했다.

IPv4에서 지정한 IP주소는 금방 동이 나버렸고,
IPv6라는 새로운 통신 규칙(주소체계)을 세우게 되었다.
2001:0db8:85a3:08d3:1319:8a2e:0370:7334의 범위 내에서 IP주소를 할당하게 되었고,
해당 범위 내에서 지정할 수 있는 IP 주소의 수는 약 2823구 개정도 이다.
앞으로 천년뒤에도 쓸 수 있을만큼 넉넉한 숫자이다.

하지만 IP 주소체계를 바꾼다는 것은 쉽지 않은 일이므로,
기존에 사용하고 있는 IPv4를 최대한 아껴써야 하는데 그 일환 중에 하나가 바로 공유기 이다.

공유기를 사용하면 하나의 IP를 여러 컴퓨터가 나눠쓸 수 있다.
IP 주소를 아껴쓸 수 있고, 통신 절약도 된다는 장점이 있다.

## 공유기 (router)

### IP address란?
IP address (Internet Protocol Address) 란, 인터넷 사용을 위해 꼭 필요한 것이고, 컴퓨터에 할당되는 주소이다.
클라이언트에서 서버에 요청을 하면, (서버 IP 주소로 call)
서버는 클라이언트에 응답을 하는 프로세스가 이루어지기 때문에 (클라이언트 IP 주소로 response)
IP 주소가 꼭 필요하다.

통신사와 계약을 해서 컴퓨터에 인터넷이 연결되거나, 스마트폰에 와이파이가 연결되는 순간 IP 주소가 할당된다.
인터넷과 연결되는 모든 전자기기에는 IP 주소가 할당된다.

### 공유기의 역할

공유기의 뒷면을 보면 회선을 연결할 수 있는 구멍이 여러개가 있는데
하나 떨어져 있는 것에는 WAN이라 적혀있을 것이고, 여러개가 붙어있는 것이 LAN을 위한 구멍이다.

* WAN(Wide Area Network) 광역 네트워크
* LAN(Local Area Network) 지역 네트워크

공유기는 광역 네트워크와 지역 네트워크를 연결하는 중계자 같은 역할을 한다.

### 공용 IP와 사설 IP
1. 공용 IP (public IP address)
통신사에서 발급받은 인터넷선을 WAN에 꽂으면, 공유기에 IP 주소가 할당된다.
외부에서 접속할 수 있는 IP 주소이다.
ex)
공유기에 할당받은 IP 주소가 다음과 같다고 해보자. 59.6.66.238
어떤 클라이언트가 59.6.66.238에 접속하면 LAN에 연결되어 있는 전자기기가 아닌 공유기에 접속한다고 이해하면 된다.

2. 사설 IP (private IP address) 
LAN 구멍에 컴퓨터나 노트북을 연결해서 인터넷을 사용하거나, 공유기 안테나를 통해서 와이파이를 사용하면 IP가 할당되지만 공유기에도 자연스럽게 IP 주소가 할당된다.
지역 네트워크 내부에서만 사용할 수 있는 IP이다.
공유기 내부의 IP 주소가 할당된다.
해당 IP 주소를 Gateway address, Router address라고 한다.

| 네트워크 구분 | IP 구분 | IP | 기기 종류 |
|-----|-------------------|-------------|------|
| WAN | public IP address | 59.6.66.238 | 공유기 |
| LAN | private IP address | 192.168.0.1~4 | 공유기, 컴퓨터, 노트북, 스마트폰 |

3. IP 할당 범위
| IP 할당 범위 | IP 갯수 | 용도 |
| 10.0.0.0 ~ 10.255.255.255 | 16,777,216 | 공용 IP 용 |
| 172.16.0.0 ~ 172.31.255.255 | 1,048,576 | 
| 192.168.0.0 ~ 192.168.255.255 | 65,536 | 사설 IP 용 |

## NAT (Network address translation)
NAT란 로컬 IP를 공공 IP로 변환하여 외부 IP와 접속이 가능하도록 하는 기능이다. 
공유기에 연결된 장치들이 인터넷을 통해서 공유기 밖의 정보에 접속할 수 있는 것은 NAT 덕분이다.

예를 들어 google.com에 접속해본다고 해보자.
1. 와이파이가 연결된 노트북으로 구글에 접속을 시도한다.
노트북은 로컬 IP를 가지기 때문에 외부에서 IP를 인식할 수 없다.
2. 공유기에 노트북의 로컬 IP가 기록된다. (192.168.0.4)
3. 공유기를 거쳐 public IP로 변환되어 나온다. (59.6.66.238)
4. public IP로 구글에 접속한다.
5. 구글로부터의 response가 오면 공유기에 기록해 두었던 사설 IP(노트북)에 요청이 반환된다. 

즉 NAT는 로컬 IP의 요청을 공용 IP의 요청으로 바꾸는 역할을 한다.


## 내 컴퓨터의 IP 주소 알아내기
### IP 주소 알아내기
1. 윈도우
제어판 > 네트워크와 인터넷 > 인터넷 접속 방법 > 상세
default gateway : LAN에서의 IP

2. 리눅스
터미널에서 ifconfig > eth0(이너넷 0) > inet addr (인터넷 주소, IP)
터미널에서 route > default의 Gateway(공유기의 주소)

3. 맥
환경설정 > 무선랜 > 고급 > TCP/IP
IPv4 주소 = 컴퓨터의 IP
라우터 = 공유기의 주소

### 라우터의 환경설정
내부 IP 주소 : gateway IP
외부 IP 주소 : 공용 IP

## 포트 (port)
영어로 항구,
하나의 IP에서 여러 애플리케이션이 사용하기 위해 포트를 지정한다.

ex)
하나의 클라이언트 PC에서 게임도 하고, 화상통화도 하고, 웹 브라우저 요청도 한다고 해보자.
그러면 하나의 클라이언트가 여러 개의 서버와 통신을 해야 한다.
서버에서는 클라이언트의 어떤 동작을 위해 패킷을 돌려주어야 하는지 파악하기 쉽지 않고,
클라이언트는 서버로부터 받은 패킷이 어떤 동작을 위한 패킷인지 알 수 없다.

TCP/IP 패킷 정보에 다음과 같은 정보가 포함되어 있기 때문에 서버와 클라이언트가 원할하게 패킷을 주고 받는 것이다.

- 출발지 IP, PORT
- 목적지 IP, PORT

| 동작 | 클라이언트 IP: 포트 | 서버 IP: 포트 |
| 게임 | 100.100.100.1:8090 | 200.200.200.2:11220 |
| 화상통화 | 100.100.100.1:21000 | 200.200.200.2:32202 |
| 웹 브라우저 | 100.100.100.1:10010 | 200.200.200.2:80 |

0 ~ 65535번 포트 : 할당 가능
0~1023번 포트 : Well-known port (알려져 있는, 이미 지정이 되어 있는 포트, 사용하지 않는 것이 좋음)
- FTP : 20(SSH), 21
- TELNET : 23
- HTTP : 80 (web server 자동으로 연결 됨)
- HTTPS : 443

웹 서버를 하나 더 연결하고 싶을 때 관습적으로 8080 포트나 8000번 포트에 연결하기도 함.

특정 포트에 접속하고 싶을 때 다음과 같이 접속하면 됨.
80 포트 : https://www.opentutorials.org
8080 포트 : https://www.opentutorials.org:8080

## 포트 포워딩 (Port forwading)
공유기 외부에서 공유기 내부의 컴퓨터에 접속하기 위해서는 공유기의 몇번 포트에 접속한 정보를 공유기 내의 어떤 아이피의 몇번 포트로 연결해줄 것인지를 공유기에게 알려줘야 한다. 

나의 public IP의 특정 포트로 접속을 하면 특정 private IP에 접속할 수 있도록 라우터에 기록을 하는 것이다.
예를 들어,
59.6.66.238:8080으로 접속을 하면 192.168.0.3:80 (모니터 컴퓨터)로 연결해주고,
59.6.66.238:8081로 접속을 하면 192.168.0.4:80(노트북)으로 연결해준다.
라우터는 public IP의 안내자 같은 역할을 한다.

라우터 종류에 따라 다르지만, 
ipTIME 기준 
라우터 설정 페이지 > 고급 설정 > 포트포워딩 설정에서 설정할 수 있다.

이렇게 하면 외부에서 내 컴퓨터 서버에 있는 웹 애플리케이션에 접속할 수 있다.
내 IP를 외부에 알리는 것은 매우 위험한 일이기 때문에 보안에 신경을 쓰고, 되도록이면 알리지 않는 것이 좋다. 

즉, 포트 포워딩이란 외부 IP의 포트번호가 무엇이냐에 따라 특정 내부 IP로 연결하는 기능을 말한다.

## 유동 아이피와 고정 아이피
통신사에서 제공하는 인터넷을 연결하면 자동으로 IP가 할당된다.
할당 받은 IP 통해 외부 클라이언트가 접속할 수 있지만, 통신사로부터 할당 받은 IP가 자주 바뀐다는 점 때문에 가정에서 서버를 운영하는 것이 어렵다.

IP가 자주 바뀌는 이유로
통신사에 가입하는 고객의 수는 느는데, IP의 수는 제한되어 있는것이 가장 큰 원인이다.

그래서 통신사는 자사 인터넷 서비스에 가입되어 있지만, 일정 기간 인터넷을 사용하지 않는 고객의 IP를 회수에서
새롭게 가입한 고객에게 해당 IP를 할당하고, 기존의 고객이 인터넷을 사용하기 시작하면 새로운 IP를 부여한다.
(안쓰는 사람의 IP를 회수에서 빌려주고, 회수하고, 빌려주고의 반복...)

기존 고객의 입장에선 IP가 계속 바뀌기 때문에 유동 아이피(Dynamic IP Address)를 가지게 된다.
이러한 이유로 가정에서 서버를 운영하는 것이 어렵다.

반면에, 통신사에게 2-3만원을 더 주면 고정 IP(Static IP Address)를 제공해준다.
IP를 독점적으로 사용할 수 있는 이러한 방법도 있다.
(캬 자본주의 세상)

## DHCP
DHCP(Dynamic Host Configuration Protocol)는 네트워크에 접속한 장치의 ip, subnet mask, gateway address, DNS와 같은 정보를 자동으로 설정해주는 기술이다.
Mac address(Media Access Control)는 PC의 물리적 주소를 뜻하며, DHCP는 Mac address를 통해 서버와 클라이언트를 식별한다.
DHCP가 작동하는 방식에 대해서 살펴보자.

ex)
DHCP Server는 공유기(router)가 되며, 
DHCP Client는 로컬 네트워크 내부에서 인터넷에 접속하고자 하는 전자기기가 된다.

| 구분 | 장치 | mac address | IP |
| DHCP Server | 공유기(Router) | 88:36:6C:33:FC:50 | 192.168.0.1 |
| DHCP Client | 노트북 | 8c:85:90:0c:e3:cc | 192.168.0.4 |

1. DHCP Client -> Server
8c:85:90:0c:e3:cc(노트북) 입니다. IP주소가 필요합니다.

2. DHCP Server -> Clinet
88:36:6C:33:FC:50(공유기) 입니다. 192.168.0.4 사용가능합니다.
(라우터에 이미 다른 기기에 할당된 IP주소가 다 기록되어 있고, 남은것이 XX.4인 것!)

3. DHCP Client -> Server
8c:85:90:0c:e3:cc(노트북) 입니다. 192.168.0.4 사용하겠습니다.

4. DHCP Server -> Clinet
88:36:6C:33:FC:50(공유기) 입니다. 네 알겠습니다. 임대시간은 2시간입니다.

위와 같은 과정을 통해 각 기기의 TCP/IP 정보가 자동으로 할당이 된다.
요즘과 같이 모바일을 빈번하게 사용하는 시대에서
한 곳에서만 인터넷을 사용하는 것이 아니라, 여러 장소에서, 여러 공유기를 거쳐 와이파이에 접속한다.
DHCP의 기능이 있었기에 빠르게 IP를 할당 받아 사용하고 있으며, 덕분에 모바일의 발전이 가속화 되지 않았나 생각한다.

라우터 관리 화면 > 고급 설정 > 내부 네트워크 설정 : DHCP 설정 부분
- DHCP 서버 동작 : 실행 /중지
- 동적 IP 주소 범위 : 192.168.0.2 - 192.168.0.254 (DHCP에서 IP를 할당하는 범위가 된다)
- IP 대여시간 : 1분 ~ 7일 (연결된 컴퓨터가 많은 상태라면 시가늘 짧게 설정하는 것이 좋다)

정해진 시간만큼 IP를 바꿔가며 할당하기 때문에 Dynamic IP가 된다.

인터넷을 통해 다양한 것들이 가능하게 되었다.
기회의 통로이다.

라우터(공유기)는 네트워크와 관련해서 다양한 기능을 갖추고 있다.
서버, 클라이언트, IP, 포트, NAT에 대한 지식을 갖추고 있다면 공유기의 관리자 화면에서 할 수 있는 일들이 참 많다.

라우터와 관련된 심화 주제에 대해 살펴보자면,
1. NAS(Network Attached Storage)
네트워크에서 사용하는 저장장치라고 할 수 있다.
데이터의 저장과 백업을 도와주는 편의 기능이다.
ex) Dropbox, Google Drive, Web hard

2. Domain name
IP address에 이름을 붙인 것으로
IP가 자주 바뀌어도 고정된 이름으로 접속할 수 있어 편리하다. 
도메인 네임은 연간 만원~십만원 정도 국제 기구에 수수료를 제공해서 사용할 수 있다.
DDNS (Dynamic DNS)를 사용하면 고정 IP를 가지고 있는 것과 같은 효과를 낼 수 있다.

3. http
웹에 접속할 때 보안과 관련해서 http를 사용하고 있다.
http는 누군가 감청할 가능성이 높기 때문에 이러한 점을 보완하여 만든 것이 https이다.
https를 사용하면 서버와 클라이언트가 안전하게 정보를 주고 받을 수 있다.
예전에는 https를 사용하기 위해서 비용을 지불해야 했지만, 요새는 무료로 많이 제공되고 있어 사용하지 않을 이유가 없다.
Let's encript 등과 같은 사이트에서 인증서를 발급해 주기도 하니, 서버와 클라이언트 간 안전한 통신을 위해 적용해 볼 수 있다.

4. web hosting
웹 서버를 제공하는 업체. 

5. server hosting
좀 더 높은 자유도를 가지는 서버 제공 업체.

6. cloud computing
보다 큰 규모로 여러 편의 시설을 제공하는 업체.
