# Docker
인프런 '따라하며 배우는 도커와 CI환경' 강의를 듣고!

## 도커를 쓰는 이유?
도커없이 프로그램을 다운 받으면,
installer 다운 -> installer 실행 -> 에러
갖고 있는 서버, 패키지 버전, 운영체제 등등에 따라 프로그램 설치 중 에러가 발생한다.
뿐만 아니라, 설치과정이 다소 복잡하다.

복잡한 설치 과정을 단순하게 만들어 준것이 Docker이다!

ex) 
redis를 사용해본다고 하자.
다음 명령어 만으로 redis를 다운 받아 사용할 수 있다.
(기존의 방식이라면 tar파일을 다운 받아서 압축을 풀고 다운 받는 과정을 거쳐야 한다.)
~~~
docker run -it redis
~~~

## 도커란 무엇인가?
컨테이너를 사용하여 응용프로그램을 `더 쉽게 만들고 배포하고 실행`할 수 있도록 설계된 도구이며,
`컨테이너 기반의 오픈소스 가상화 플랫폼`이며 생태계이다.

### 컨테이너란 무엇인가?
일반적인 컨테이너는 다양한 물건을 한데 담아 다양한 운송 수단을 통해서 쉽게 옮길 수 있도록 하는 거대한 철제 상자이다.
이와 같이 도커 컨테이너도 컨테이너 안에 다양한 프로그램, 실행 환경을 컨테이너로 추상화하고 동일한 인터페이스를 제공하여
프로그램의 배포 및 관리를 단순하게 해준다.
일반 컨테이너의 개념에서 물건을 손쉽게 운송해주는 것처럼 프로그램을 손쉽게 이동, 배포, 관리를 할 수 있게 해준다.
AWS, Azure, Google cloud 등 어디에서든 실행 가능하게 해준다.

## 도커 컨테이너란 무엇인가?
`도커 컨테이너`는 코드와 모든 종속성을 패키지화 하여 응용 프로그램이 한 컴퓨팅 환경에서 다른 컴퓨팅 환경으로 빠르고 안정적으로 실행되도록 하는
소프트웨어의 표준 단위이다.
=> 간단하고 편리하게 프로그램을 실행시켜주는 것

## 도커 이미지란 무엇인가?
`도커 이미지`는 코드, 런타임, 시스템 도구, 시스템 라이브러리 및 설정과 같은 `응용 프로그램을 실행하는데 필요한 모든 것을 포함`하는
가볍고 독립적이며 실행 가능한 `소프트웨어 패키지` 이다. 
도커 이미지는 프로그램을 실행하는데 필요한 설정이나 종속성을 가지고 있으며,
도커 이미지를 이용해서 컨테이너를 생성한다.
토커 컨테이너는 이미지의 인스턴스이며, 도커 컨테이너를 이용해 프로그램을 실행한다.

ex)
카카오톡 도커 이미지로 도커 컨테이너를 생성한다.
도커 컨테이너 안에서 카카오톡을 실행한다.

### MacOS를 위한 도커 다운 받기
1. 도커 홈페이지 접속 (https://www.docker.com/)
2. Get Started 클릭
3. Docker Desktop에서 본인이 사용하고 있는 OS에 맞는 것을 다운 받는다.
4. Docker 회원가입 (도커를 사용하려면 계정이 되어있어야 한다.)
5. Docker에 로그인 (도커를 실행하면 Mac 우상단에 생성되는 고래 모양 아이콘 오른쪽 클릭)
6. 도커가 잘 설치 되었나 터미널에서 확인
~~~
docker version
~~~

## 도커를 사용할 때의 흐름
항상 도커를 사용할 때는
1. 도커 Client (CLI)에 커맨드를 입력한다.
2. 도커 Server (Daemon)이 커맨드를 받아서 그것에 따라 이미지를 생성하든 컨테이너를 생성하든 모든 작업을 하게 된다.

ex)
hello-world를 처음 실행한다고 해보자.

1. 도커 클라이언트는 해당 커맨드를 입력 받는다.
~~~
docker run hello-world
~~~
2. 도커 서버
3. 도커 이미지 cache 보관 장소
   - hello-world 이미지가 존재하는지 체크한다.
   - 캐시 보관 장소에 hello-world 이미지가 없다면 도커 허브에서 가져온다.
4. 도커 허브
   - 누구나 자유로이 다운 받아 사용할 수 있도록 이미지들을 보관한다.
   - busybox, nginx, nodejs 등을 제공한다.

=> 실행 결과
~~~
Eunjiui-MacBook:~ eunjisong$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete 
Digest: sha256:df5f5184104426b65967e016ff2ac0bfcd44ad7899ca3bbcf8e44e4461491a9e
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

~~~

두번째 실행을 한다면??
이미 도커 이미지 cache에 저장이 되었으므로 도커 허브에서 가져오는 과정은 생략된다.

## 도커와 기존의 가상화 기술과의 차이를 통한 컨테이너 이해
1. 가상화 기술이 나오기 전
- 한대의 서버를 하나의 용도로만 사용
- 남는 서버 공간을 그대로 방치
- 하나의 서버에 하나의 운영체제, 하나의 프로그램만을 운영
- 안정적 but 비효율적

2. 하이퍼 바이저 기반의 가상화 출현 (VM)
- 하이퍼 바이저란
  - 호스트 시스템에서 다수의 게스트 OS를 구동할 수 있게 하는 소프트웨어
  - 하드웨어를 가상화 하면서 하드웨어와 각각의 VM을 모니터링 하는 중간 관리자이다.
- 논리적으로 공간을 분할하여 VM이라는 독립적인 가상 환경의 서버 이용 가능

3. 도커 컨테이너의 출현
- 공통점 : 도커 컨테이너와 가상 머신은 기본 하드웨어에서 격리된 환경 내에 애플리케이션을 배치하는 방법이다.
- 차이점
  - 가장 큰 차이점은 격리된 환경을 얼마나 격리를 시키는지의 차이
  - VM과 비교했을 때 컨테이너는 하이퍼바이저와 게스트 OS가 필요하지 않아 더 가볍다.
  - 어플리케이션을 실행할 때는 컨테이너 방식에서는 호스트 OS 위에 어플리케이션의 실행 패키지인 이미지를 배포하기만 하면 되는데
  VM은 어플리케이션을 실행하기 위해서 VM을 띄우고 자원을 할당한 다음 게스트 OS를 부팅하여 어플리케이션을 실행해야 해서 훨씬 복잡하고 무겁다.

### 도커와 기존 가상화 기술(VM)의 차이
- 도커 : 호스트 OS 위에 커널(Docker Engine)을 띄워서 각각의 컨테이너를 실행시킨다. (=> 모든 컨테이너가 동일한 커널을 사용한다.)
        컨테이너가 전체 OS를 내장할 필요가 없어, 매우 가볍고 일반적으로 약 5-100MB이다.
        호스트 시스템이 모든 프로그램을 나열할 수 있는 권한이 있다면, 결과적으로 컨테이너 내부에서 실행되는 프로세스는 호스트 시스템에서 볼 수 있다.
        ex) 도커와 함께 몽고 DB 컨테이너 시작 -> 호스트 OS의 일반 쉘에 `ps-e grep 몽고` 를 실행하면 프로세스가 표시됨.

- 기존 가상화 기술 (VM) : 호스트 OS 위에 게스트 OS를 부팅하여 애플리케이션을 실행시킨다. (=> 모든 애플리케이션이 각각 다른 게스트 OS를 가진다.) 
                    호스트 OS 또는 하이퍼 바이저와 독립되어 있다고 할 수 있다.
                    비교적 사용법이 간단하지만 매우 느리다.

### 어떻게 CPU, 커널 등에서 도커 컨테이너를 격리 시킬까?
리눅스에서 쓰이는 Cgroup(control groups)과 네임 스페이스(namespace)가 있다.
컨테이너와 호스트에서 실행되는 다른 프로세스 사이에 벽을 만드는 리눅스 커널 기능들이다.

- C Group
  - CPU, 메모리, Network Bandwith, HD i/o 등 시스템 리소스에 특정 프로세스의 사용량을 할당하고 관리하는 기능.

- 네임 스페이스
  - 하나의 시스템에서 프로세스를 격리시킬 수 있는 가상화 기술
  - 특정 프로세스의 경계에 벽을 세워 격리된 공간을 사용하는 것처럼 격리된 환경을 제공하는 경량 프로세스 가상화 기술

## C-group, 네임스페이스를 도커 환경에서 쓸 수 있는 이유
Cgroup과 네임스페이스는 리눅스 환경에서 사용되어지는 것인데 어떻게 MacOS와 Window OS에서 사용할 수 있는 것일까?
`도커는 리눅스 VM 위에서 실행`되어지고 있기 때문에 해당 커맨드를 사용할 수 있는 것이다!

| 도커 환경 |
|---------|
| 카카오톡 or MySQL or Node.js |
| 리눅스 커널 |
|리눅스 VM |
| MacOS / Windows |
| 하드웨어 |

## 도커 이미지 내부 파일 구조 보기

### 도커 이미지 실행
도커 이미지를 실행하는 커맨드는 다음과 같다.
~~~
docker run 이미지 이름
~~~
- docker : 도커 클라이언트 언급
- run : 컨테이너 생성 및 실행
- 이미지 이름 : 이 컨테이너를 위한 이미지

ex) docker run hello-world 

해당 커멘드를 실행하면 이미지는 두가지를 가지게 된다.
1. 시작시 실행될 명령어 : run hello-world
2. 파일 스냅샷 : hello-world

이미지로 컨테이너를 생성하는 순서는 다음과 같다.
1. 먼저 파일 스냅샷 되어 있는 것을 컨테이너의 하드 디스크 부분에 올린다.
2. 시작 커맨드를 이용해 애플리케이션을 실행한다.

### 이미지 내부 파일 시스템 구조 보기
도커 이미지 내부 파일 시스템 구조를 보는 커맨드는 다음과 같다.
~~~
docker run 이미지 이름 ls
~~~
- docker : 도커 클라이언트 언급
- run : 컨테이너 생성 및 실행
- 이미지 이름 : 이 컨테이너를 위한 이미지
- ls : 이 자리는 원래 이미지가 가지고 있는 시작 명령어를 무시하고 여기에 있는 커맨드를 실행하게 한다.
        ls 커맨드는 현재 디렉토리의 파일 리스트를 표출한다.
ex) docker run alpine ls

해당 커멘드를 실행하면 이미지는 두가지를 가지게 된다.
1. 시작시 실행될 명령어 : ??? (alpine에서 사용될 어떤 시작 명령어)
2. 파일 스냅샷 : bin,dev, etc...

이미지로 도커를 생성하면
1. 컨테이너 하드디스크 부분에 bin,dev, etc...를 올린다.
2. ls를 시작 커맨드로 애플리케이션을 실행한다.

#### 왜 hello-world 이미지로 ls 커맨드를 실행할 수 없을까??
알파인의 리스트를 출력하는 커맨드를 날리면 결과 값이 출력된다.
~~~
// docker run alpine ls
bin
dev
etc
home
lib
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
~~~

그런데 hello-world 이미지의 리스트를 출력하는 커맨드를 날리면 결과값이 출력되지 않는다.
왜 그럴까???
~~~
Eunjiui-MacBook:~ eunjisong$ docker run hello-world ls
docker: Error response from daemon: OCI runtime create failed: container_linux.go:380: starting container process caused: exec: "ls": executable file not found in $PATH: unknown.
~~~

alpine 컨테이너의 하드디스크에는 ls 커맨드를 서포트 하는 파일이 포함되어 있어 리스트를 출력할 수 있지만,
hello-world 컨테이너는 간단한 기능을 수행하기 때문에 하드디스크에 ls 기능을 수행하는 파일이 포함되어 있지 않아 동작을 수행할 수 없었다.

=> 이처럼, 컨테이너가 하드디스크에 포함하고 있는 파일에 따라서 커맨드 실행 유무가 결정 된다!!!

## 컨테이너들 나열하기
### 현재 실행중인 컨테이너 나열
현재 실행 중인 컨테이너를 나열하는 커맨드는 다음과 같다.
~~~
docker ps
~~~
- docker : 도커 클라이언트 언급
- run : process status

실행 결과 :
~~~
Eunjiui-MacBook:~ eunjisong$ docker ps
CONTAINER ID   IMAGE     COMMAND            CREATED          STATUS         PORTS     NAMES
c189a32e16d6   alpine    "ping localhost"   10 seconds ago   Up 9 seconds             zealous_germain
~~~

1. CONTAINER ID
   컨테이너의 고유한 아이디 해쉬값.
   실제로는 더욱 길지만 일부분만 표출된다.
2. IMAGE
   컨테이너 생성시 사용한 도커 이미지.
3. COMMAND
    컨테이너 시작 시 실행될 명령어.
    대부분 이미지에 내장되어 있으므로 별도 설정이 필요 없다.
4. CREATED
   컨테이너가 생성된 시간.
5. STATUS
   컨테이너의 상태.
   실행중은 Up, 종료는 Exited, 일시정지 Paus.
6. PORTS
   컨테이너가 개방한 포트와 호스트에 연결한 포트.
   특별한 설정을 하지 않은 경우 출력되지 않는다.
7. NAMES
   컨테이너 고유한 이름.
   컨테이너 생성시 --name 옵션으로 이름을 설정하지 않으면, 도커 엔진이 임의로 형용사와 명사를 조합해 설정.
    id와 마찬가지로 중복이 안되고 docker rename 명령어로 이름을 변경할 수 있다.
    ex) docker rename original-name changed-name
    

### 원하는 항목만 보기
원하는 항목만(현재 실행중인 컨테이너만) 지정하여 보는 커맨드는 다음과 같다.
~~~
docker ps --format 'table{{.Names}}\table{{.Image}}'
~~~
- docker : 도커 클라이언트 언급
- run : process status
- --format
- 'table{{.Names}}
- \t : 탭
- table{{.Image}}'

~~~
Eunjiui-MacBook:~ eunjisong$ docker ps --format 'table{{.Names}}\table{{.Image}}'
NAMES             ableIMAGE
zealous_germain   ablealpine
~~~

### 모든 컨테이너 나열
실행 중이건, 중지 상태이건 상관 없이 모든 컨테이너를 나열하는 커맨드는 다음과 같다.
~~~
docker ps -a
~~~
- docker : 도커 클라이언트 언급
- run : process status
- a : all

~~~
Eunjiui-MacBook:~ eunjisong$ docker ps -a
CONTAINER ID   IMAGE         COMMAND            CREATED          STATUS                      PORTS     NAMES
c189a32e16d6   alpine        "ping localhost"   4 minutes ago    Up 4 minutes                          zealous_germain
3146fa293894   hello-world   "ls"               29 minutes ago   Created                               dreamy_yalow
5dba7f117e66   alpine        "ls"               30 minutes ago   Exited (0) 30 minutes ago             tender_goldstine
c104efac0dbe   hello-world   "/hello"           5 days ago       Exited (0) 5 days ago                 angry_greider
b2937496e656   hello-world   "/hello"           5 days ago       Exited (0) 5 days ago                 busy_gould
~~~