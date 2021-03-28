# Home Server
생활코딩 Home Server 강의를 듣고!

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
| LAN | private IP address | 192.168.0.1 | 공유기, 컴퓨터, 노트북, 스마트폰 |

3. IP 할당 범위
| IP 할당 범위 | IP 갯수 | 용도 |
| 10.0.0.0 ~ 10.255.255.255 | 16,777,216 | 공용 IP 용 |
| 172.16.0.0 ~ 172.31.255.255 | 1,048,576 | 
| 192.168.0.0 ~ 192.168.255.255 | 65,536 | 사설 IP 용 |