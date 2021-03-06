# DNS (Domain Name System)
생활코딩의 DNS 강의를 듣고...

## IP 주소와 hosts

### IP 주소와 hosts의 개념

두 대의 컴퓨터가 통신을 하기 위해선 반드시 갖추어야 하는 것이 있는데, 그것이 바로 IP 주소 이다.
인터넷에 연결되어 있는 컴퓨터를 host라고 한다.

모든 운영체제에는 hosts라는 파일이 있다.
해당 파일에는 key-value의 형식으로 도메인과 IP 주소가 저장되어 있다.
도메인을 key로 IP를 찾아내어 접속한다.
DNS 서버를 사용하지 않고, hosts 파일을 통해서 본인이 자주 사용하는 사이트의 IP의 도메인 주소를 알아낼 수도 있다.

### hosts 파일을 설정하는 방법

hosts 파일은 중요한 파일이기 때문에 관리자 권한이 있어야 수정할 수 있다.
다른 컴퓨터(host)의 IP에 이름을 붙여서 사용할 수 있다.
예전에는 DNS를 사용하지 않고 hosts 파일을 조작해서 활용했었다.

## 도메인 이름과 보안

hosts 파일을 변조하여 내가 접속하려 했던 사이트가 아닌, 다른 악성 사이트로의 접속을 유도할 수도 있다.
ex) 내가 접속하려는 사이트
example.com 93.184.216.34 (오리지널)
example.com 66.66.66.66 (변조됨)
이름모를 66.66.66.66 IP로 접속하게 됨.

그만큼 hosts 파일을 안전하게 관리하는 것이 중요하고, 관리를 소홀히 했을 시 보안에 취약해진다. (피싱의 타겟이 될 수 있음)

https = http + secure
https를 사용하면 hosts파일을 변조해 접속 되었을 시, 경고 문구를 표시해준다. 이를 통해 피싱을 막을 수 있다.
중요한 사이트에는 https로 접속 해야 한다.

## DNS의 태동

DNS 이전의 이야기...
로컬 hosts 파일 내용을 수정하면 나에게만 적용되는 내용이므로, 누구나 동일하게 같은 이름으로 접속할 수 있는 것은 아니였다.
Standford Research Institute에서 공통의 hosts 파일을 관리하기 시작하였고,
이를 사용하고 싶은 사람들은 해당 기관의 운영 시간에 전화를 걸어 자신의 IP와 지정하고 싶은 도메인 주소를 알려주어야 했다.
ex) 여보세요 IP 주소 93.184.216.34에 도메인 주소 example.com 를 사용하고 싶은데요~

전세계의 컴퓨터는 Standford Research Institute에서 다운 받은 hosts 파일을 로컬 hosts 파일에 덮어쓰기 하여 공통의 도메인 주소에 접속하는 식으로 사용해왔다.
각자가 hosts 파일을 관리하는 것이 아니라, 신뢰할 수 있는 기관에서 이를 관리하고, IP가 아닌 도메인 주소로 접속할 수 있게 된 것이다.

처음에는 이것만으로도 충분했지만, 인터넷이 점점 발전하면서 여러 문제점이 발생하였다.
hosts 파일을 업데이트 하지 않으면 특정 도메인 주소를 사용할 수 없다는 점이 발생하였으며,
Standford Research Institute에서 수작업으로 이 모든 작업을 수행했기 때문에 수많은 시간과 비용이 소요되었다.

## DNS의 원리

IP를 외워 특정 웹 애플리케이션에 접속하는 것이 어렵기 때문에 DNS가 생기게 되었다.
DNS Server에는 수많은 IP의 DNS가 기록되어 있다.

다음과 같은 도메인 주소를 사용하고 싶은 IP가 있다고 해보자.
도메인 : example.com
IP : 93.184.216.34

해당 IP에 도메인 주소를 부여해 사용하는 과정은 다음과 같다.

1. DNS Server에 IP 93.184.216.34의 도메인 주소 example.com 지정을 요청하여 등록됨.
2. 내 컴퓨터에서 example.com를 입력.
3. 내 컴퓨터의 hosts 파일을 뒤져 해당 도메인 주소에 매칭하는 내용이 있는지 확인한다.
4. 없다면 DNS Server에서 example.com에 해당하는 IP 주소를 찾고 반환.
5. 내 컴퓨터는 DNS Server로부터 받은 IP 주소에 접근.
6. example.com의 서버 컴퓨터에 접속.

3~6번의 과정은 인터넷을 통해 모두 순식간에 이루어진다.
DNS Server를 사용함으로서 IP가 변경되거나, DNS가 추가 삭제 되어도 전세계 모든 컴퓨터에 공통적으로 적용될 수 있으며,
꼭 운영시간이 아니더라도 언제든지, 쉽고 간단한게 사용할 수 있다는 장점이 있다.

## public DNS의 사용

컴퓨터를 인터넷에 연결하는 즉시 인터넷 통신사들이 자동으로 특정 DNS 서버의 IP를 셋팅하는 메커니즘을 가지고 있다.
하지만 internet service provider가 제공하는 DNS를 사용하고 싶지 않을 수도 있다.
ex) internet service provider가 내가 접속한 ip주소를 어딘가에 기록하여 마케팅에 활용할 수도 있고, 보안 및 프라이버시에 취약...

public DNS server : 누구나 무료로 사용할 수 있는 도메인 네임 서비스

구글 public DNS Service는 8.8.8.8이라는 IP를 가짐.
개인 컴퓨터의 DNS 설정을 8.8.8.8이라고 설정하면 internet service provider가 제공하는 DNS가 아닌, 구글의 DNS Server를 사용할 수 있음.

osx에서는 네트워크 > 고급 > DNS에 들어가서 설정하면 된다!

## 도메인 이름의 구조

DNS 서버는 전세계에 수천대, 수만대가 존재하고, 서로가 협력하여 전세계인들이 IP를 외우지 않아도 인터넷을 사용할 수 있도록 돕고 있다.

ex) blog.example.com.
blog : sub
.example : Second-level
.com : Top-level
. : Root

도메인의 각각의 부분을 담당하는 독자적인 서버 컴퓨터가 있다.
각각의 컴퓨터가 전담하는 파트가 다른 것이다.
ex) A 컴퓨터는 Root만 담당,
B 컴퓨터는 Top-level 만 담당...

각각의 컴퓨터는 상위가 직속 하위 파트의 내용을 알고 있어야 한다.
ex) A 컴퓨터 : Root 만 담당하지만 Top-level의 내용을 알고 있어야 한다. Second-level과 sub 파트의 내용은 모른다.
B 컴퓨터 : Top-level 만 담당하지만 Second-level의 내용을 알고 있어야 한다. Root와 sub 파트의 내용은 모른다.

sub를 전담하는 서버가 IP 주소를 가지고 있다.

DNS 내부에서 IP를 알아내는 과정은 다음과 같다.
다음의 도메인 네임으로 접속했다고 해보자.
ex) blog.example.com.

1. Root를 담당하는 서버 내부에서 .을 검색하며 IP를 묻는다.
2. Root를 담당하는 서버에 IP 주소가 없어 Top-level을 담당하는 서버에 .com.을 검색하며 IP를 묻는다.
3. Top-level을 담당하는 서버에 IP 주소가 없어 Second-level을 담당하는 서버에 .example.com.을 검색하며 IP를 묻는다.
4. Second-level을 담당하는 서버에 IP 주소가 없어 sub을 담당하는 서버에 blog.example.com.를 검색하며 IP를 묻는다.
5. sub를 담당하는 서버에 IP가 존재했다. 해당 IP를 반환한다.

## 도메인 이름 등록 과정과 원리

DNS는 행정적이며 이와 관련해서 자동화 기술들이 뒷받침해주고 있다. (행정적 + 기술)
등록자가 등록하고자 하는 IP와 도메인을 등록 대행자가 대신 등록소(Top-level domain name server, root name server)에 등록해준다.

1. 등록자 (Registrant)
  일반적인 서버 컴퓨터이며,
  다음과 같은 도메인 주소로 IP를 등록하고 싶다고 해보자.

- 도메인 : example.com
- IP : 93.184.216.34

2. 등록대행자 (Register)
  등록소에 IP와 도메인을 등록을 대신해주는 등록 대행자이다.
  일정 수수료를 받고 대신 처리 해준다.
  개인이 Name Server를 세워서 등록할 수도 있다.

  authoritative name server
  a.iana-servers.net
  example.com.
  example.com A 93.184.216.34

3. 등록소 (Registry)
  어떤 IP가 어떤 도메인을 사용하는지 권한을 인식한다.
  대여 기간 동안 다른 사람은 해당 도메인을 사용할 수 없다.

  Top-level domain
  a.gtld-servers.net
  .com.
  example.com NS a.iana-servers.net (example.com의 name server는 a.iana-servers.net이다)
  
  4. ICANN
  전세계의 IP를 관리하는 거대한 비영리단체이다.
  Root name server에 대한 관리자이다.

  Root name server
  a.root-servers.net
  .
  com NS a.gtld-servers.net (com의 name server는 a.gtld-servers.net이다)

5. DNS
  인터넷에 연결되면 internet service provider에 의해서 DNS Server가 자동으로 셋팅된다.
  DNS Server는 Root name server의 IP를 가지고 있다.

DNS Server
1.1.1.1
. NS a.root-servers.net (.의 name server는 a.root-servers.net이다)

- 도메인을 등록할 때 : 등록자 -> 등록 대행자 -> 등록소 -> Root Name Server (ICANN)
- 도메인을 사용할 때 : 유저 -> DNS Server -> Root Name Server (ICANN) -> 등록소 -> 등록대행자

## nslookup 사용법

nslookup은 도메인 이름에 대한 정보를 조회하는데 사용되는 대표적인 도구이다.

1. example.com 조회

```
> nslookup example.com
> nslookup -type=a example.com (동일)

OUTPUT:
Server: 168.126.63.1
Address: 168.126.63.1#53

Non-authoritative answer:
Name: example.com
Address: 93.184.216.34
```

첫 문단에 표시된 Server와 Address는 로컬 컴퓨터에 연결되어 있는 DNS Server의 정보이다.

두번째 문단에 표시된 내용은 DNS Server로부터 반환된 권한 없는 대답에 대한 내용이다.
example.com에 대한 권한은 등록대행자(authoritative name server)가 가지고 있다.
DNS 서버가 매번 다음과 같은 흐름으로 IP를 찾는다면 매우 비효율적일 것이다.

DNS Server -> Root Name Server (ICANN) -> 등록소 -> 등록대행자

그래서 DNS Server는 검색한 값을 cache로 저장해놓고 있다.
Non-authoritative answer는 cache에 저장한 값을 반환한 것이다.
이렇게 cache를 저장해두면 성능도 높이고, 네트워크 부하도 낮출 수 있다.

2. example.com의 name server 조회

```
> nslookup -type=ns example.com

OUTPUT:
Server: 168.126.63.1
Address: 168.126.63.1#53

Non-authoritative answer:
example.com nameserver = a.iana-servers.net.
example.com nameserver = b.iana-servers.net.

Authoritative answers can be found from:
```

두번째 문단은 example.com의 name server에 대한 정보이다.
name server 하나가 죽더라도 실행될 수 있도록 두개가 존재하고 있음을 알 수 있다.

3. 네임서버에 직접 접속하여 example.com 조회

```
> nslookup example.com a.iana-servers.net.

OUTPUT:
Server: a.iana-servers.net.
Address: 199.43.135.53#53

Name: example.com
Address: 93.184.216.34
```

첫번째 문단은 지정한 name server에 대한 정보이다.

두번째 문단에선 Non-authoritative answer가 사라졌다.
a.iana-servers.net.가 authoritative name server이기 때문이다.
특정 Name Server를 지정해서 IP를 찾을 수 있음

## 나의 도메인 이름 장만하기

freenom.com 을 사용해서 도메인을 지정해보겠다.
ex) 사용하고 싶은 도메인 주소 : dns4u.ga.

1. 등록대행자 freenom.com에서 dns4u.ga를 할당 받았다.

authoritative name server
ns01.freenom.com
dns4u.ga.
dns4u.ga.52.231.13.171

2. 등록소에 1년간 dns4u.ga 도메인을 사용하겠다는 것을 지정한다.
  Top-level domain
  a.ns.ga
  .ga.
  dns4u.ga NS ns01.freenom.com

도메인 name을 사용하기 위해선 name server가 구축되어 있어야 하는데, 등록대행자 freenom.com는 name server도 제공한다.
하지만 내가 name server를 세워서 실행하겠다고 한다면, freenom.com 쪽에 name server 변경에 대한 내용을 전달하여 등록소에 저장된 name server의 주소를 바꾸면 된다.

3. 지정한 도메인에 IP를 등록한다.
  IP : 도메인에 엮고 싶은 IP 주소를 입력해준다.
  TTL(Time To Leave) : 캐쉬가 남아있는 시간(초 단위) IP가 자주 바뀌는 도메인이라고 한다면 TTL을 낮은 숫자로 지정해주면 된다. TTL 단위마다 캐쉬를 새로 갱신 함. 그러므로 TTL 값이 크다면 도메인 값이 바로 반영이 안될 수도 있다.

## DNS record와 CNAME 레코드의 이해

도메인 이름에 대한 정보 한건 한건을 DNS Record라고 한다.
ex)
Register에 등록된 DNS Record : dns4u.ga A 52.231.13.22 => dns4u.ga의 IP는 52.231.13.22이다.
Registry에 등록된 DNS Record : dns4u.ga NS ns01.freenom.com => dns4u.ga의 Name Server는 ns01.freenom.com이다.

DNS Record의 타입에는 여러가지가 있다.

- A : IPV4 타입
- NS : Name Server 레코드

타입 명  key  value
A  example.com.  192.0.1.1
CNAME  www.example.com.  example.com.
CNAME  edu.example.com.  lorem-1c6b.kxcdn.com

A 타입은 도메인(example.com.)에 IP 주소를 매핑한 것이다.
C 타입은 도메인에 대해 별명을 지정하는 방식으로 또 다른 도메인을 지정한 것이다.
IP 주소가 자주 바뀌는 경우에는 A 타입의 값만 바꿔주면 된다.

ex)

1. 유저가 www.example.com.로 접속하면 example.com.를 반환한다 (CNAME)
2. example.com.은 IP가 아니기 떄문에 A 타입에서 example.com.로 검색해 IP를 찾아낸다. (A)

ex) 혹은

1. edu.example.com.로 접속을 하면 lorem-1c6b.kxcdn.com을 반환한다(CNAME)
2. lorem-1c6b.kxcdn.com은 IP가 아니기 때문에 A 타입에서 lorem-1c6b.kxcdn.com로 검색해 IP를 찾아낸다. (A)

## github pages에 도메인 연결하기
github에 html 파일을 업로드 하거나 하면 서버로서 기능을 제공하기도 한다.
github에 업로드한 페이지에 도메인을 연결하고 싶다고 해보자.

* github에 업로드한 페이지 = https://web-n.github.io/web1_html_internet/
* github의 ip 주소 = 192.30.252.153
* 지정하고자 하는 도메인 주소 = dns4u.ga

1. DNS Server로부터 지정하고자 하는 도메인 주소를 할당 받는다.
    dns4u.ga으로 접속하면 192.30.252.153 IP로 연결되도록 a record가 DNS Server에 등록된다.
2. github에도 도메인 주소를 지정해둔다.
   dns4u.ga으로 접속하면 https://web-n.github.io/web1_html_internet/ 페이지를 표시하도록 한다.
3. 유저가 dns4u.ga으로 접속한다.
4. DNS server에서는 IP 주소 192.30.252.153를 반환한다.
5. IP 주소를 따라 github에 접근한다.
6. dns4u.ga으로 접속했으므로 github 룰에 따라서 https://web-n.github.io/web1_html_internet/ 페이지를 표시한다.

* github에서 DNS를 설정하는 곳
Settings > Github Pages > Custom domain
상세 설정법은 github의 document를 확인하면 됨.
(Setting up an apex domain, Setting up a www sub domain)
github은 안정성을 위해 두개의 IP를 DNS Server에 등록하도록 함 (부하 분산)

## DNS 관련 추가 토픽
1) BIND
캘리포니아 대학교에서 만든 최초의 DNS server
DNS server의 표본처럼 여겨짐

2) Dyanamic DNS (DDNS)
집으로 들어오는 인터넷의 IP는 변경할 수 없는 자원이다
서버가 설치된 IP 주소가 바뀌었을 때, 해당 내용이 DNS Server로 전달된다.
동일한 도메인 네임을 사용하면서도 IP와의 연결이 끊기지 않도록 해주며,
IP가 변경되어도 서비스를 유지할 수 있게 해준다.

3) HTTPS, SSL
누군가가 교묘하게 도메인 네임을 속여 피싱 하는 것을 차단한다.
SSL을 사용하기 위해선 인증서를 발급받는데, 해당 인증서를 사용하면 사용자가 위조된 웹 사이트에 접근하면 강력한 경고 메세지와 접속 제한을 해준다.
최근에는 SSL 인증서가 무료화 되고 있는 추세이기 떄문에 편하게 설치할 수 있는 방향으로 발전되고 있다.