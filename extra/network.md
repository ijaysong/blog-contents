# 네트워크

Udemy의 The Complete Networking Fundamentals Course를 듣고

## 기본 네트워킹 용어
### 네트워크란?
컴퓨터 네트워크란 공통적인 통신 기술을 사용하는 컴퓨팅 장치인 노드들 사이에서 자원을 공유하는 디지털 통신 네트워크이다.
노드 간 데이터 전송은 트위스트 페어 또는 광섬유 케이블과 같은 물리적 케이블 매체로 구성된 데이터 링크 또는 Wi-Fi, 마이크로파 전송 혹은 자유 공간 광학 통신과 같은 무선 방법을 통해 지원된다.

### 네트워크 기본 유형
1. 이더넷 케이블로 연결
이더넷 케이블은 근거리 통신망을 구축하기 위해 사용되는 케이블이다.
가장 흔하게는 랜선이라고도 하고, UTP 혹은 Unshield Twisted Pair Cable이라고도 한다.
RJ45 커넥터가 달린 이더넷 케이블로 서로 연결한 것이 가장 일반적인 형태의 컴퓨터 네트워크이다.

이더넷 케이블을 꽂았을 때 바로 연결되는 장치가 랜 카드이다.
랜 카드(네트워크 인터페이스 카드)는 컴퓨터를 네트워크에 연결하여 통신하기 위해 사용하는 하드웨어 장치이다.
고유 식별자로 MAC 주소를 사용하여 네트워크 매개체로 물리적인 접근을 사용하게 한다.
사용자들이 케이블을 연결하거나 무선으로 연결하여 네트워크에 접속할 수 있다.
랜카드는 10base5 -> 10base2 -> RJ45 커넥터를 지원하다가 현재는 USB만 지원하는 경우가 많다. (랜카드 자체 크기도 작아짐)

2. Wi-Fi
무선 인터넷 네트워크를 통해 디지털 장치를 연결하여 자원을 공유할 수 있다.
블루투스는 오늘날 가장 일반적으로 사용되는 네트워크 접속 방법 중 하나이다.
근거리 무선 연결에 사용되는 독점 네트워킹 표준이며, 주변 장치를 기본 장치에 연결하는데 자주 사용된다.

ex) 아이폰 AirDrop
에어드랍은 블루투스를 사용하여 근처에 있는 다른 에어드랍 지원 장치를 찾고,
연결이 이루어지면 장치간 Wi-Fi Direct라고 하는 Wi-Fi 링크를 둘 사이에 생성하여 파일을 전송한다.

### 네트워크 장치
거리가 멀면 멀수록 네트워크 신호가 약해진다.
이러한 신호의 강도 및 세기를 증폭시키기 위해 다음과 같은 장치들이 만들어졌다.

1. 리피터
`중계기`라고도 한다.
더 먼 거리에 도달할 수 있도록 입력 신호를 증폭시키는 장치이다.
전송되는 프레임(데이터)을 해석하려고 시도하지 않으므로 해당 기기는 `OSI 모델의 첫번째 계층인 물리 계층`에서 동작한다.

2. 허브
허브는 이더넷 네트워크에서 여러 대의 컴퓨터 네트워크 장비를 연결하는 장치이다.
한 대의 허브를 중심으로 여러대의 컴퓨터와 네트워크 장비가 마치 별 모양으로 서로 연결되며, 같은 허브에 연결된 장비는 모두 상호 간에 통신할 수 있다.

연결된 네트워크에서는 한 컴퓨터에서 주고받은 프레임이 같은 허브에 연결된 다른 모든 컴퓨터에 전달된다.
따라서 연결된 컴퓨터의 개수가 많아질수록 네트워크에서 충돌이 많아지고 속도가 느려진다.
이를 해결하기 위해 등장한 것이 스위치이다.

본질적으로 허브는 여러개의 포트를 가진 리피터라고 할 수 있다.
한 포트를 통해 들어온 프레임은 증폭되어 다른 포트들에 전달된다.
전송되는 프레임을 이해하지 않고 단순히 증폭시키기만 하므로 해당 기기는 `OSI 모델의 첫번째 계층인 물리 계층`에서 동작한다.

허브와 컴퓨터 장비 사이의 연결에는 보통 UTP 케이블과 RJ45 커넥터가 사용된다.

3. 스위치
간단히 스위치라고 부르며, 브리징 허브(bridging hub), MAC 브리지(MAC Bridge), 스위칭 허브 (Switching hub), 포트 스위칭 허브(Port switching hub)라고도 한다.

본질적으로 허브와 비슷하다.
소규모 통신을 위한 허브보다 훨씬 향상된 네트워크 속도를 제공한다.
이는 허브처럼 모든 컴퓨터에 프레임을 제공하는 것이 아니라, 필요로 하는 컴퓨터에만 전송하기 때문이다.
따라서 허브처럼 병목 현상이 쉽게 생기지 않는다.

전이중 통신방식(쌍방향 통신방식)을 지원하기 때문에 송신과 수신이 동시에 일어나는 경우 훨씬 향상된 속도를 제공한다.
스위치는 이 기능을 수행하기 위해서 각 컴퓨터의 고유한 MAC 주소를 기억하고 있어야 하고, 이 주소를 통해 프레임이 어디로 전송되어야 하는지 판단한다.
MAC address table을 확인하여 프레임을 올바른 목적지로 전달하므로 해당 기기는 `OSI 모델의 두번째 계층인 데이터 링크 계층`에서 동작한다.

4. 라우터
공유기라고도 한다.
IP 주소를 기반으로 한 둘 이상의 네트워크 간에 데이터 패킷을 전송하는 네트워크 장치이다.
패킷의 위치를 추출하여, 최적의 경로를 찾아 최단 시간에 전달해준다.
간단히 말해 서로 다른 네트워크 간 중계 역할을 해준다.

5. 방화벽
들어오고 나가는 네트워크 트래픽을 모니터링 하고 제어하는 네트워크 보안 시스템이다.
신뢰할 수 없는 외부 네트워크로부터의 해로운 트래픽이 들어오지 못하게 막는 역할을 한다.
서로 다른 네트워크를 지나는 데이터를 허용하거나 거부하거나, 검열, 수정하는 하드웨어나 소프트웨어 장치이다.

6. IDS (Instrusion Detection System)
침입 탐지 시스템이다.
시스템에 대한 원치 않는 조작을 탐지해준다.
침입 탐지 시스템은 전통적인 방화벽이 탐지할 수 없는 모든 종류의 악의적인 네트워크 트래픽 및 컴퓨터 사용을 탐지하기 위해 필요하다.
다음 활동에 대해 탐지하고 시스템 운영자에게 경고 동작을 취한다.

- 취약한 서비스에 대한 네트워크 공격
- 데이터 처리 공격
- 권한 확대 및 침입자 로그인
- 침입자에 의한 주요 파일 접근
- 악성 소프트웨어 (컴퓨터 바이러스 , 트로이 목마, 웜)

7. IPS (Intrusion Prevetion System)
침입 차단 시스템 혹은 침입 방지 시스템이다.
외부 네트워크로부터 내부 네트워크로 침입하는 네트워크 패킷을 찾아 제어하는 기능을 가진 소프트웨어 혹은 하드웨어이다.
일반적으로 내부 네트워크로 들어오는 모든 패킷이 지나가는 경로에 설치되며,
호스트의 IP주소, TCP/UDP의 포트번호, 사용자 인증에 기반을 두고 외부 침입을 차단하는 역할을 한다.
허용되지 않은 사용자나 서비스에 대해 사용을 거부하여 내부 자원을 보호한다.

=> 이렇게 이해하면 쉽다.
=> IDS는 집 지키는 작은 개, IPS는 집 지키는 큰 개
=> 집 지키는 개는 침입자에 대해 냄새를 맡고 짖음으로서 주인에게 침입자의 존재를 경고한다.