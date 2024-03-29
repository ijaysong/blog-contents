# Docker
인프런 '따라하며 배우는 도커와 CI환경' 강의를 듣고!

# 도커 기본
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

# 기본적인 도커 클라이언트 명령어
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

## 도커 컨테이너의 생명주기
지금까지 도커를 생성/ 시작하는 커맨드 `run`이 있다.
~~~
Docker run <이미지 이름>
~~~

그런데 이를 도커 생성과 실행으로 각각 나누어 볼 수 있다.
도커 생성은 `create`를 사용한다.
~~~
Docker create <이미지 이름>
~~~

도커 생성을 하면 도커 컨테이너 아이디가 출력된다.
ex)
~~~
Eunjiui-MacBook:~ eunjisong$ docker create hello-world
6425b4fd81c7a2d134c3ca9612f01f8b85d623559c253b749a9d5626ba6cc925
~~~
도서 실행은 `start`를 사용한다.
~~~
docker start -a <컨테이너 아이디/이름>
~~~
-a : attach (붙이다), 도커 컨테이너의 아웃풋을 출력해준다.

~~~
Eunjiui-MacBook:~ eunjisong$ docker start -a 6425b4fd

Hello from Docker!
This message shows that your installation appears to be working correctly.

... 생략 ...
~~~

=> 결론 : Docker run <이미지 이름> = Docker create <이미지 이름> + Docker start <컨테이너 아이디/이름>

## Docker Stop vs Docker Kill
공통점은 둘다 실행중인 컨테이너를 중지시킨다.

`stop`은 천천히 자비롭게 중지시킨다.
그동한 하던 작업들을 (메세지를 보내고 있었다면 보내고 있던 메세지를) 완료하고 컨테이너를 자비롭게 중지시킨다.
~~~
docker stop <중지할 컨테이너 아이디/이름>
~~~

`kill`의 경우, stop과 달리 어떠한 것도 기다리지 않고, 바로 컨테이너를 중지시킨다.
~~~
docker kill <중지할 컨테이너 아이디/이름>
~~~

cf) 현재 실행 중인 컨테이너의 아이디나 이름을 확인하고자 할때는 `ps`를 사용하면 된다.
~~~
docker ps
~~~

결과 : 
~~~
Eunjiui-MacBook:~ eunjisong$ docker ps
CONTAINER ID   IMAGE     COMMAND            CREATED          STATUS          PORTS     NAMES
5c7086fe84cf   alpine    "ping localhost"   13 seconds ago   Up 12 seconds             vigorous_tu
~~~

## 컨테이너 삭제하기
1. 중지된 컨테이너를 삭제할 때
~~~
docker rm <아이디/이름>
~~~

실행중인 컨테이너는 먼저 중지한 후에 삭제 가능하다.
`ps` 커맨드로 현재 실행 중인 컨테이너가 있는지 없는지 확인 후 실행하면 된다!

~~~
// 현재 실행 중인 컨테이너를 확인한다. 없음
Eunjiui-MacBook:~ eunjisong$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

// 컨테이너 리스트를 출력하여 삭제하고자 하는 컨테이너의 ID를 확인한다.
Eunjiui-MacBook:~ eunjisong$ docker ps -a
CONTAINER ID   IMAGE         COMMAND            CREATED          STATUS                       PORTS     NAMES
5c7086fe84cf   alpine        "ping localhost"   7 minutes ago    Exited (137) 7 minutes ago             vigorous_tu
5a43514beeb6   alpine        "ping localhost"   8 minutes ago    Exited (137) 7 minutes ago             sweet_cannon
6425b4fd81c7   hello-world   "/hello"           18 minutes ago   Exited (0) 18 minutes ago              amazing_diffie
c189a32e16d6   alpine        "ping localhost"   2 days ago       Exited (0) 2 days ago                  zealous_germain
3146fa293894   hello-world   "ls"               2 days ago       Created                                dreamy_yalow
5dba7f117e66   alpine        "ls"               2 days ago       Exited (0) 2 days ago                  tender_goldstine
c104efac0dbe   hello-world   "/hello"           8 days ago       Exited (0) 8 days ago                  angry_greider
b2937496e656   hello-world   "/hello"           8 days ago       Exited (0) 8 days ago                  busy_gould

// 컨테이너(ID: 5c7086fe84cf)를 삭제한다.
Eunjiui-MacBook:~ eunjisong$ docker rm 5c7086fe84cf
5c7086fe84cf

// 컨테이너(ID: 5c7086fe84cf)가 삭제되고 리스트에 없다.
Eunjiui-MacBook:~ eunjisong$ docker ps -a
CONTAINER ID   IMAGE         COMMAND            CREATED          STATUS                       PORTS     NAMES
5a43514beeb6   alpine        "ping localhost"   9 minutes ago    Exited (137) 8 minutes ago             sweet_cannon
6425b4fd81c7   hello-world   "/hello"           19 minutes ago   Exited (0) 18 minutes ago              amazing_diffie
c189a32e16d6   alpine        "ping localhost"   2 days ago       Exited (0) 2 days ago                  zealous_germain
3146fa293894   hello-world   "ls"               2 days ago       Created                                dreamy_yalow
5dba7f117e66   alpine        "ls"               2 days ago       Exited (0) 2 days ago                  tender_goldstine
c104efac0dbe   hello-world   "/hello"           8 days ago       Exited (0) 8 days ago                  angry_greider
b2937496e656   hello-world   "/hello"           8 days ago       Exited (0) 8 days ago                  busy_gould
~~~

2. 모든 컨테이너를 삭제하고 싶을 때
~~~
docker rm `docker ps -a -q`
~~~

3. 이미지를 삭제하고 싶을 때
~~~
docker rmi <이미지 id>
~~~

4. 한번에 컨테이너, 이미지, 네트워크 모두 삭제하고 싶다면?
도커와 관련된 부분이 초기화 된다.
~~~
docker system prune
~~~ 

~~~
Eunjiui-MacBook:~ eunjisong$ docker system prune
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all dangling images
  - all dangling build cache

Are you sure you want to continue? [y/N] y
Deleted Containers:
28aae9ba0b91421a04b6301828f9e83e98f47858278bdca4e016309b62b0e040

Total reclaimed space: 0B
~~~

## 실행 중인 컨테이너에 명령어 전달
`이미 실행 중인` 컨테이너에 명령어를 전달하는 커맨드는 다음과 같다.
~~~
docker exec <컨테이너 아이디>
~~~

ex) 
1. 터미널 2개를 실행한다.
2. 첫번째 터미널에서 컨테이너 하나를 실행한다.
~~~
docker run alpine ping localhost
~~~
3. 두번째 터미널에서 컨테이너가 잘 작동하고 있는지 확인하고 다른 명령어를 전달한다.
`ps` 명령어로 실행 중인 컨테이너의 아이디를 확인한다.
~~~
Eunjiui-MacBook:~ eunjisong$ docker ps
CONTAINER ID   IMAGE     COMMAND            CREATED          STATUS          PORTS     NAMES
27eae59d8c39   alpine    "ping localhost"   16 seconds ago   Up 12 seconds             sleepy_aryabhata
Eunjiui-MacBook:~ eunjisong$ docker exec 27eae59d8c39 ls
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

`docker exec <컨테이너 아이디> ls`와 같은 결과를 출력하는 것이 `docker run alpine ls`이다.

=> docker exec은 `이미 실행 중인 컨테이너`에 명령어를 전달
=> docker run은 `새로 컨테이너를 생성`해서 실행

## 레디스를 이용한 컨테이너 이해
레디스(redis)란, key-value 형태의 비정형 DB 관리 시스템이다. (noSQL)
레디스 서버를 실행 한 후, 레디스 클라이언트를 통해서 서버에 명령어를 전달해줘야 한다.

1. 첫번째 터미널 실행 후, 레디스 서버를 작동시킨다.
~~~
docker run redis
~~~
2. 첫번째 터미널에서는 추가 커맨드를 입력할 수 없다. 두번째 터미널 실행 후, 레디스 클라이언트를 작동시킨다.
~~~
redis-cli
~~~

하지만 에러가 발생한다. 왜일까??
=> 레디스 클라이언트가 레디스 서버가 있는 `컨테이너 밖에서 실행을 하려하니, 접근할 수 없기에` 에러가 발생했다.

3. 레디스 클라이언트를 레디스 서버가 있는 컨테이너 내부에서 실행시킨다.
~~~
docker exec -it <컨테이너 아이디> redis-cli
~~~
-i : interactive (상호적인)
-t : terminal (터미널)
-it : 해당 옵션을 적어줘야 명령어를 실행한 후 계속 명령어를 적을 수 있다.
      -it 가 없다면 그냥 redis-cli를 키기만 하고 밖으로 다시 나와버린다.

## 실행 중인 컨테이너에서 터미널 환경 구축
실행 중인 컨테이너에 명령어를 실행할 때는 매번 다음과 같은 커맨드를 일일히 입력해 줘야 했다.
~~~
docker exec -it <컨테이너 아이디> <명령어>
~~~

실행 중인 컨테이너에 쉘이나 터미널 환경으로 접속하여 좀더 편하게 작업을 수행할 수 있다.
마지막에 `sh` 명령어를 붙여주면 된다.
~~~
docker exec -it <컨테이너 아이디> sh
~~~

컨테이너를 쉘 환경으로 접근해보자.
ex)
1. 첫번째 터미널을 실행한 후, alpine 이미지를 이용해서 컨테이너를 실행한다.
~~~
docker run alpine ping localhost
~~~
2. `exec` 커맨드를 이용하고, 마지막 명령어 부분에 `sh`를 입력한다.
컨테이너 안에 터미널 환경을 구축한다.
~~~
docker exec -it <컨테이너 아이디> sh
~~~
3. 그 안에서 터미널에서 할 수 있는 것들을 작동할 수 있다.
- ls : 컨테이너 디렉토리에 있는 내용을 확인(디렉토리, 파일)
- touch <파일명> : 파일 생성
- export hello=hi echo $hello : 변수 생성 출력

# 직접 도커 이미지를 만들어보기 
## 도커 이미지 생성하는 순서
`도커 이미지`는 컨테이너를 만들기 위해 필요한 설정이나 종속성을 가지고 있는 소프트웨어 패키지이다.
도커 이미지를 생성하는 커맨드는 다음과 같다.
~~~
docker create <이미지 이름>
~~~ 

컨테이너는 도커 이미지로 생성을 한다면, 도커 이미지는 어떻게 생성할까??
도커 이미지를 생성하는 순서는 다음과 같다.

1. Docker File 작성
`Docker File`이란 도커 이미지를 만들기 위한 설정 파일이다.
컨테이너가 어떻게 행동해야 하는지에 대한 설정들을 정의해준다.

2. 도커 클라이언트에 전달
도커 파일에 입력된 것들이 도커 클라이언트에 전달된다.

3. 도커 서버에 전달
도커 클라이언트에 전달된 모든 중요한 작업들을 하는 곳이다.

4. 이미지 생성

## Dockerfile 만들기
`도커 파일 (Dockerfile)`이란, 도커 이미지를 만들기 위한 설정 파일이며 컨테이너가 어떻게 행동해야 하는지에 대한 설정들을 정의해주는 곳이다.

도커 이미지는 시작시 실행될 명령어와 파일 스냅샷으로 이루어져 있다.
ex)
- 시작시 실행될 명령어 : run kakaotalk
- 파일 스냅샷 : 카카오톡 파일

도커 파일을 만들기 위해선 도커 이미지가 무엇이 필요한지 생각해야 한다!
도커 파일을 만드는 순서는 다음과 같다.

1. 베이스 이미지 명시
베이스 이미지를 명시해준다. (파일 스냅샷에 해당)
2. 추가 명령어 명시
베이스 이외에 추가로 필요한 파일을 다운받기 위한 몇가지 명령어를 명시해준다. (파일 스냅샷에 해당)
3. 컨테이너 실행 명령어 명시  
컨테이너 시작 시 실행될 명령어를 명시해준다.

~~~
# 베이스 이미지를 명시해준다.
FROM baseImage

# 추가적으로 필요한 파일들을 다운로드 받는다.
RUN command

# 컨테이너 시작시 실행 될 명령어를 명시해준다.
CMD [ "executable" ]
~~~
=> FROM, RUN, CMD 등은 도커 서버에게 무엇을 하라고 알려주는 것이다.

- FROM
이미지 생성 시 기반이 되는 이미지 레이어이다.
`<이미지 이름>:<태그>` 형식으로 작성한다.
ex) ubuntu:14.04
태그를 안붙이면 최신 버전으로 다운 받는다.

- RUN
도커 이미지가 생성되기 전에 수행할 쉘 명령어이다.

- CMD
컨테이너가 시작되었을 때 실행할 실행 파일 또는 쉘 스크립트이다.
해당 명령어는 DockerFile 내에서 1회만 쓸 수 있다.

### 베이스 이미지란 무엇인가
도커 이미지는 여러개의 레이어로 이루어져 있다.
`베이스 이미지`는 그중에서도 여러 이미지들의 기반이 되는 부분이다!
Windows, MacOS, Linux 와 같은 OS라고 생각하면 된다.
`레이어`는 베이스 이미지 위에 쌓이는 중간 단계의 이미지라고 생각하면 된다.
`레이터 캐싱`이란 쌓여진 레이어들 위에 레이어가 추가가 되는것을 말한다.

| 이미지 구조 |
|----------|
|레이어 (Layer)|
|레이어 (Layer)|
|베이스 이미지 (Base Image)|

ex)
"hello" 문구를 출력하는 도커 파일을 하나 만들어보자.

~~~
# 베이스 이미지를 명시해준다.
FROM alpine

# 추가적으로 필요한 파일들을 다운로드 받는다.
# RUN command

# 컨테이너 시작시 실행 될 명령어를 명시해준다.
CMD [ "echo", "hello" ]
~~~
- FROM
베이스 이미지는 ubuntu나 centOS를 사용해도 되지만,
문구를 단순 출력하는 기능이기 떄문에 사이즈가 큰 베이스 이미지 대신에 작은 사이즈의 alpine 베이스를 사용한다.

- RUN
hello 문자 출력을 위해 echo를 사용해야 한다.
이미 alpine 안에 echo 관련 파일이 포함되어 있으므로 RUN은 생략한다.

- CMD
컨테이너 시작시 실행될 명령어 `echo hello`를 적어준다.

## 도커 파일로 도커 이미지 만들기
완성된 도커 파일로 어떻게 이미지를 생성할까?
도커 파일에 입력된 것이 도커 클라이언트에 전달되어서 도커 서버가 인식하게 해야한다.
`build` 명령어를 사용하면 된다.

~~~
docker build ./ 또는 docker build .
~~~
=> 현재 디렉토리에 있는 dockerfile을 찾아서 도커 클라이언트에 전달!

`build` 명령어는 해당 디렉토리 내에서 dockerfile이라는 파일을 찾아서 도커 클라이언트에게 전달해준다.
docker build 뒤에 붙인 `./`와 `.`은 현재 디렉토리를 가리킨다.

### 도커 이미지 생성 과정
다음과 같은 내용의 도커파일을 실행했다.
~~~
# 베이스 이미지를 명시해준다.
FROM alpine

# 추가적으로 필요한 파일들을 다운로드 받는다.
# RUN command

# 컨테이너 시작시 실행 될 명령어를 명시해준다.
CMD [ "echo", "hello" ]
~~~

1. Alpine 이미지 (베이스 이미지)가 불려진다.
- 시작 시 실행될 명령어 : ???
- 파일 스냅샷 : etc, dev, bin

2. 임시 컨테이너가 실행된다.
- 시작 시 실행될 명령어 : echo hello (도커 파일에 작성된 명령어)
- 파일 스냅샷 : etc, dev, bin (하드 디스크에 Alpine 이미지의 파일 시스템 스냅샷이 추가된다.)

3. Apline 새로운 이미지 생성
- 시작 시 실행될 명령어 : echo hello
- 파일 스냅샷 : etc, dev, bin
- 
4. 임시 컨테이너 삭제

=> Summary
베이스 이미지에서 다른 종속성이나 새로운 커맨드를 추가할 때 임시 컨테이너를 만든 후, 그 컨테이너를 토대로 새로운 이미지를 만든다.
그리고 그 임시 컨테이너는 지워준다.

=> 이미지 -> 임시 컨테이너(새로운 명령어, 새로운 파일 스냅샷) -> 새로운 이미지

## 내가 만든 이미지 기억하기 쉬운 이름 주기
도커 파일로 이미지를 만들면 아이디가 숫자로 만들어진다.
ex) 265431....
도커 아이디로 컨테이너를 실행하려면 `docker run 265431....` 이런식으로 너무 길고 복잡하다.
도커 아이디를 매번 기억하기 힘들기 때문에 이미지에 이름을 지정해서 실행할 수 있다.

### 도커 이미지에 이름 주는 방법
`docker build` 커맨드에 `t 옵션`을 준다.
~~~
docker build -t ijaysong/hello:latest .
~~~
-t {나의 도커 아이디} / {저장소/프로젝트 이름} : {버전} 

~~~
Eunjiui-MacBook:dockerfile-folder eunjisong$ docker build -t ijaysong/hello:latest .
[+] Building 0.5s (5/5) FINISHED                                              
 => [internal] load build definition from Dockerfile                     0.1s
 => => transferring dockerfile: 268B                                     0.0s
 => [internal] load .dockerignore                                        0.1s
 => => transferring context: 2B                                          0.0s
 => [internal] load metadata for docker.io/library/alpine:latest         0.0s
 => CACHED [1/1] FROM docker.io/library/alpine                           0.0s
 => exporting to image                                                   0.0s
 => => exporting layers                                                  0.0s
 => => writing image sha256:700d6646badf50c893acf603ca95fcc2a57017d8cf0  0.0s
 => => naming to docker.io/ijaysong/hello:latest                         0.0s

Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them
Eunjiui-MacBook:dockerfile-folder eunjisong$ docker run -it ijaysong/hello
hello
~~~

도커 이미지에 hello라는 이름과 latest라는 이름을 지정하고, 도커 이름으로 실행을 하면 제대로 동작하는 것을 확인할 수 있다.

# 도커를 이용한 간단한 Node.js 어플 만들기
Node.js App을 만들어서 도커 이미지 생성 후, 컨테이너에서 실행해보겠다.

## Node.js 앱 만들기
0. 컴퓨터 사양에 맞는 node.js 다운로드
1. package.json 생성
: 프로젝트의 정보와 프로젝트에서 사용 중인 패키지의 의존성을 관리한다.
2. server.js 생성
: Entry Point로서 가장 먼저 실행되는 파일이다.

### package.json 생성
`package.json`파일을 직접 작성할 수 있지만, `npm init` 커맨드를 통해 작성할 수도 있다.
~~~
Eunjiui-MacBook:nodejs-docker-app eunjisong$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (nodejs-docker-app) 
version: (1.0.0) 
description: 
entry point: (index.js) server.js
test command: 
git repository: 
keywords: 
author: 
license: (ISC) 
About to write to /Users/eunjisong/Documents/projects/Blog-contents/docker/nodejs-docker-app/package.json:

{
  "name": "nodejs-docker-app",
  "version": "1.0.0",
  "description": "",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "dependencies": {
    "express": "^4.16.1"
  },
  "author": "",
  "license": "ISC"
}
~~~
dependency에 `express`를 추가해준다.
`express`는 JavaScript와 jQuery의 관계처럼 Node.js의 API를 단순화하고 새로운 기능을 추가해서 Node.js를 더 쉽고 유용하게 사용할 수 있게 해준다.

### server.js 생성
~~~
const express = require('express');

// Constants
const PORT = 8080;
const HOST = '0.0.0.0';

// App
const app = express();
app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(PORT, HOST);
console.log(`Running on http://${HOST}:${PORT}`);
~~~
Express 모듈을 불러온다.
Express 서버를 위한 포트와 호스트를 지정한다.
새로운 Express 어플을 생성하고,
"/" 경로로 요청이 오면 Hello World를 결과값으로 전달한다.
해당 포트와 호스트에서 HTTP 서버를 시작한다.

### 도커 파일 만들기
dockerfile로 도커 이미지를 만들어서 생성한 도커 컨테이너에 Node.js app을 실행시켜 보겠다.

근본이 되는 부분을 먼저 작성해준다.
~~~
FROM node:10

RUN npm install

CMD ["node", "server.js"]
~~~
- FROM: 베이스 이미지에 node 10버전을 지정해준다.
기존에 사용했던 `alpine 이미지는 가장 최소한의 경량화된 파일들이 들어 있기 때문에 npm을 위한 파일이 들어있지 않아 RUN 커맨드인 npm install을 실행 할 수 없다.`
그래서 npm이 들어있는 베이스 이미지를 찾아야하는데 그것들 중 하나가 node이다.

- RUN: npm은 Node.js로 만들어진 모듈을 웹에서 다운 받아 설치하고 관리해주는 프로그램.
npm install은 package.json에 적혀있는 종속성들(dependencies)을 웹에서 자동으로 다운 받아서 설치해주는 명령어이다.
(npm install -> npm registry에서 모듈 다운로드 -> app에 모듈 설치)
결론적으로, `node.js app을 만들때 필요한 모듈들을 다운받아 설치하는 역할을 한다.`

- CMD: node 파일을 실행시키려면 `node + 엔트리 파일 이름`을 지정해줘야 한다.

### Package.json 파일이 없다고 나오는 이유
위에서 작성한 dockerfile을 빌드하면 Package.json 파일이 없다고 에러가 발생한다.
이유가 무엇일까??

`npm install` 커맨드는 어플리케이션에 필요한 종속성을 다운받아 준다.
이렇게 다운 받을 때, package.json을 보고 그곳에 명시된 종속성들을 다운 받아서 설치해준다.
하지만 package.json가 컨테이너 안에 없기에 찾을 수 없다는 에러가 발생한 것이다.

ex)
Node 베이스 이미지
- 시작시 실행될 명령어: ???
- 파일 스냅샷 : home, bin, dev...

임시컨테이너
- 하드웨어 : Node 베이스 이미지의 파일 스냅샷

package.json 및 그 외 파일들(server.js) : 임시 컨테이너 외부에 존재하고 있음!

이러한 이유로 `COPY`를 이용해서 package.json을 컨테이너 안으로 넣어줘야 한다.
~~~
COPY package.json ./
~~~
- COPY
- package.json : 복사 할 파일 경로, 복사 대상
- ./ : 컨테이너 내에서 파일이 복사될 경로, 붙여넣기 할 위치

Dockerfile을 다음과 같이 수정해준다.
~~~
FROM node:10

COPY package.json ./

RUN npm install

CMD ["node", "server.js"]
~~~

그런데 server.js가 없다고 또 에러가 발생한다.
package.json과 마찬가지로 컨테이너 안에 해당 파일이 존재하지 않기 때문이다.
해당 디렉토리에 존재하는 모든 파일을 복사하여 붙여넣기 해준다.
~~~
COPY ./ ./
~~~

dockerfile도 다음과 같이 변경해준다.
~~~
FROM node:10

COPY ./ ./

RUN npm install

CMD ["node", "server.js"]
~~~

### 생성한 이미지로 어플리케이션 실행 시 접근이 안 되는 이유
Dockerfile로 생성한 이미지 실행까지 무사히 진행했다.
웹 브라우저에서 애플리케이션에 접속하려했더니 접근이 안되는 에러가 발생했다.
왜 그럴까??

< 현재까지 컨테이너를 실행할 때 사용한 명령어 >
~~~
docker run {이미지 이름}
~~~

< 앞으로 컨테이너를 실행하기 위해 사용할 명령어 >
~~~
docker run -p 49160:8080 {이미지 이름}
~~~
이미지를 만들 때 로컬에 있던 파일(package.json, server.js) 등을 컨테이너에 복사해줘야 했다.
이와 비슷하게 네트워크도 로컬 네트워크에 있던 것을 컨테이너 내부에 있는 네트워크에 연결 시켜줘야 한다.
로컬 호스트에서 아무리 8080 포트로 접속을 해도 로컬 호스트 네트워크와 매핑이 안되어 있으므로 접속이 안되는 것이다.

ex)
브라우저 : http://localhost:49160
로컬 호스트 네트워크 포트 : 49160
컨테이너 네트워크 포트 : 8080 (server.js에서 지정)

`p옵션`을 주어서 로컬 호스트 포트와 컨테이너 호스트 포트를 매핑 시켜준다.
-p: 포트 옵션
49160: 웹 브라우저에서 입력할 포트번호 (로컬 호스트 네트워크)
8080: 컨테이너 네트워크 포트번호

### Working Directory 명시해주기
Work Directory(WORKDIR)란?
이미지 안에서 어플리케이션 소스 코드를 가지고 있을 디렉토리를 생성하는 것이다.
이 디렉토리가 어플리케이션의 working directory가 된다.

그렇다면 왜 working directory를 지정해주어야 하는 것일까?

node 이미지의 파일 스냅샷 리스트를 살펴보면 home, bin, dev 등의 파일들이 있다.
~~~
// Node 이미지 속 Root 디렉토리
Eunjiui-MacBook:nodejs-docker-app eunjisong$ docker run -it node ls
bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr
~~~

반면에 직접 만든 이미지의 Root 디렉토리를 살펴보면 
Dockerfile에서 COPY해온 여러 파일들까지 지저분하게 루트 디렉토리에 저장되어 있는 것을 알 수 있다.  
~~~
Eunjiui-MacBook:nodejs-docker-app eunjisong$ docker run -it ijaysong/nodejs ls 
Dockerfile  etc    media         package-lock.json  run        sys
bin         home   mnt           package.json       sbin       tmp
boot        lib    node_modules  proc               server.js  usr
dev         lib64  opt           root               srv        var
~~~

COPY 해온 파일들이 루트 디렉토리에 저장되면서 발생하는 문제점이 두가지가 있다.

1. 기존에 존재하는 파일과 동일한 이름의 파일을 COPY해오면 기존의 것이 덮어씌워져 사라진다.
ex) 기존 working directory에 home이라는 폴더가 있고 COPY하면서 새로 추가되는 폴더에 home이 있다면 중복되므로 원래있던 폴더가 덮어씌워져 버린다.
2. 모든 파일이 한 디렉토리에 저장되어 정리정돈이 안되어 있다.

=> 그래서 어플리케이션을 위한 소스들은 work 디렉토리를 따로 만들어서 보관한다.

### 어플리케이션 소스 변경으로 다시 빌드하는 것에 대한 문제점
현재까지는 만든 어플을 소스 변경시 변경된 소스를 반영시켜주기 위해서 도커 파일을 다시 빌드해서 컨테이너 이미지를 생성시켜줘야 했다.
ex)
도커 파일 생성 -> 도커 파일로 도커 이미지 생성(docker build) -> 도커 이미지로 컨테이너 생성 후 앱 실행 (docker run)

매번 도커파일을 수정해야 할 떄마다 다시 빌드하고 컨테이너를 생성해야 하는 것은 비효율적이고 번거롭기까지 하다!
도커 파일 내부에서 COPY ././를 지정해주고 있는데
이 부분으로 인해서 타겟 파일들을 다시 다운 받아주어야 하기 때문이다.
그렇다면 이러한 비효율적인 부분을 어떻게 해결할 수 있을까? 

### 어플리케이션 소스 변경으로 재빌드 시 효율적으로 하는 법
기존에 있던 도커 파일은 다음과 같이 구성되어져 있었다.
~~~
COPY ./ ./

RUN npm install
~~~
소스 코드는 물론, 종속성 모듈들까지 함께 copy하여 npm install을 하였다.
그렇기 때문에 소스 코드만 수정한 것인데도 
종속성 모듈까지도 새로 다운 받아졌다.

도커 파일을 다음과 같이 수정하면 조금 더 효율적으로 빌드 할 수 있다.
~~~
COPY package.json ./

RUN npm install

COPY ./ ./
~~~
맨 처음 copy를 할때는 오직 module에 관한 것만 해준다.
그리도 RUN npm install을 해준 이후, 다시 모든 파일들을 copy해준다.
이렇게 해주면 모듈에 변화가 생길 때만 다시 다운 받아주며, 소스 코드에 변화가 생길 때 모듈을 다시 다운 받는 현상이 사라진다.
캐시에 저장되어 있는 기존 모듈을 사용하기 때문에 빌드 속도도 빨라진다.

### Docker Volumes에 대해서
`Volume`은 도커 컨테이너에서 로컬에 있는 파일을 참조하는 것이다.

- COPY : 로컬에 존재하는 소스코드와 종속성 모듈을 새로운 컨테이너에 복사한다. 새롭게 가져옴 (로컬 -> 컨테이너)
- Volume: 로컬에 존재하는 소스코드와 종속성 모듈을 도커 컨테이너에서 참조(mapping)한다.  (컨테이너 -> 로컬)

~~~
docker run -p 5000:8080 -v /usr/src/app/node_modules -v $(pwd):/usr/src/app {이미지 아이디}
~~~
`node_module`이란 컨테이너 내부에 생성되는 디렉토리로, npm install을 할 때 다운 받아지는 모든 종속성 파일들이 저장되는 디렉토리이다. 
컨테이너에서 node_module 디렉토리가 필요한데 로컬에는 해당 디렉토리가 없다.
그러니 volume을 사용할 때 node_module은 무시하고 컨테이너에 맵핑하지 말아 달라고 커멘드를 지정한 것이다.

`pwd(print working directory)`는 현재 작업 중인 디렉토리의 이름을 출력하는데 쓰인다. 
pwd 부분에는 로컬에서 다운로드 받을 경로를 지정을 해주고, : 다음에는 도커 컨테이너 참조하고 있는 경로를 지정해준다.

=> 다시 빌드하지 않아도 소스코드가 반영이 될 수 있다!

## Docker Compose
### Docker Compose란 무엇인가
`docker compose`란 다중 컨테이너 도커 애플리케이션을 정의하고 실행하기 위한 도구이다.

### 애플리케이션 소스 작성하기
1. `npm init`으로 package.json 작성
2. server.js도 작성
3. 기본적인 노드 부분 작성
4. 레디스 부분 작성

#### `레디스`란?
Redis(REmote Dictionary Server)는 메모리 기반의 키-값 구조 데이터 관리 시스템이며,
모든 데이터를 메모리에 저장하고 빠르게 조회할 수 있는 비관계형 데이터베이스(NoSql)이다.

#### 레디스를 쓰는 이유?
메모리에 저장을 하기 때문에 Mysql같은 데이터베이스에 데이터를 저장하는 것과
데이터를 불러올 때 훨씬 빠르게 처리할 수 있으며,
비록 메모리에 저장하지만 영속적으로도 보관이 가능하다.
그래서 서버를 재부팅해도 데이터를 유지할 수 있는 장점이 있다. 

#### Node.js 환경에서 Redis 사용 방법
1. 먼저 redis-server를 작동시킨다.
2. redis 모듈을 다운 받는다. (package.json에 dependencies에 지정해놓음)
3. 레디스 모듈을 받은 후, 레디스 클라이언트를 생성하기 위해서 Redis에서 제공하는 createClient()함수를 이용해서 redis.createClient로 레디스 클라이언트를 생성해준다. (server.js)
   - redis server가 작동하는 곳이 Node.js 앱이 작동하는 곳과 다른 곳이라면 host와 port 값을 명시해주어야 한다.
   - 도커를 사용하지 않는 환경 : host: "https://redis-server.com"
   - 도커를 사용하는 환경 : host: "redis-server" 
   - 도커 Compose를 사용할 때는 host 옵션에 docker-compose.yml에서 명시한 컨테이너 이름을 지정하면 된다.

### Dockerfile 작성하기
~~~
FROM node:10

WORKDIR /usr/src/app

COPY ./ ./

RUN npm install

CMD [ "node", "server.js"]
~~~
- WORKDIR : working directory를 지정해주어 COPY 해온 파일들이 깔끔하게 정리될 수 있도록 한다.
- COPY : 현재 디렉토리의 파일들을 루트(working directory)에 복사한다. ex) package.json 등등...
- RUN : package.json의 dependencies에 작성한 express와 redis를 사용하기 위해서 npm을 설치한다.
- CMD : 노드 실행 커맨드

### Docker Containers간 통신 할 때 나타나는 에러
레디스 클라이언트를 작동하려면 레디스 서버가 켜져 있어야 한다.
먼저 레디스 서버를 위한 컨테이너를 실행하고, 노드 js를 위한 컨테이너를 실행해본다.
ex)
- 컨테이너 1 : 레디스 서버
- 컨테이너 2 : 노드 JS 앱 + 레디스 클라이언트

컨테이너 1을 실행한다. (레디스 서버)
~~~
// 레디스 서버 실행
docker run redis
~~~

컨테이너 2를 실행한다. (노드 JS 앱 + 레디스 클라이언트)
~~~
// 만들어 둔 docker file로 이미지를 생성
docker build -t ijaysong/docker-compose-app ./

// 이미지로 컨테이너를 실행한다.
docker run ijaysong/docker-compose-app
~~~

컨테이너 2를 실행하면 레디스 서버 연결이 실패했다고 뜬다!
왜일까??

컨테이너 간 통신을 할 때 설정을 해주지 않으면, 서로 접근 할 수 없다.
그래서 노드 JS 앱에서 레디스 서버에 접근 할 수 없었던 것이다.

이와 같은 컨테이너 상황에서 쉽게 네트워크를 연결 시켜주기 위해서 `Docker Compose`를 이용하면 된다.

### Docker Compose 파일 작성하기
컨테이너 간 통신을 위해 `Docker Compose.yml`를 작성해보자.
Docker Compose 파일은 yaml(얌)파일 인데 `yml`은 뭘까??

YAML (ain't markup language)의 약자이며, `일반적으로 구성 파일 및 데이터가 저장되거나 전송되는 응용 프로그램에서 사용되고` 원래는 XML이나 json 포맷으로 많이 쓰였지만, `좀더 사람이 읽기 쉬운 포맷`으로 나타난게 yaml 이다.

컨테이너 1, 2 간 통신이 가능하도록 두 개의 컨테이너의 바탕엔 docker compose가 있다.
docker compose에는 버전이 있고, 두 컨테이너를 service로 감싼다.
그렇다면 docker compose 파일을 작성해보자.
~~~
version: "3"
services:
    redis-server:
        image: "redis"
    node-app:
        build: .
        ports:
            - "5000:8080"
~~~
version : 도커 컴포즈의 버전이다.
services: 이곳에 실행하려는 컨테이너
   redis-server : 컨테이너 이름
      image : 컨테이너에서 사용하는 이미지
   node-app : 컨테이너 이름
      build : Dockerfile의 위치를 지정해줌. 현 디렉토리에 있으면 `.`을 작성
      ports : 포트 맵핑 ex) 로컬 포트 : 컨테이너 포트

도커 컴포즈를 이용해서 앱을 실행시켜보자.
~~~
docker-compose up
~~~

### Docker Compose로 컨테이너를 멈추기
도커 컴포즈를 이용해서 앱을 중단시켜보자.
새로운 터미널을 열어서 다음 커맨드를 실행한다.
~~~
docker-compose down
~~~
docker-compose.yml 파일이 위치해있는 디렉토리에서 실행해야 한다.

새로운 터미널을 열어서 실행해줘야 해서 번거로운 점이 있다.
굳이 다른 터미널을 켜지 않고ㅡ 하나의 터미널로 해결하고 싶다면 
docker compose를 컨테이너를 실행할 때, `d` 옵션을 주면 된다.
~~~
docker compose -d up
~~~
-d : detached 모드로서 앱을 백그라운드에서 실행시킨다. 그래서 앱에서 나오는 output을 표출하지 않는다.

cf )
- docker-compose up : 이미지가 없을 때 이미지를 빌드하고 컨테이너 시작
- docker-compose up --build : 이미지가 있든 없든 이미지를 빌드하고 컨테이너 시작

## 간단한 어플을 실제로 배포해보기(개발 환경 부분)
### 리액트 앱 설치
리액트를 다운받기 위해선 node가 설치되어 있어야 한다.
다음 명령어로 node 설치 유무를 확인한다.
~~~
node -v
~~~

리액트를 다운받아보자.
~~~
npx create-react-app ./
~~~
./ : 리액트를 설치하고자 하는 디렉토리 이름을 지정해준다. 현재 위치하고 있는 디렉토리에 설치하겠다는 뜻이다.

리액트는 다음과 같은 흐름으로 이어진다.
1. 개발단계
~~~
npm run start
~~~

2. 테스트 단계
개발한 것이 문제가 있는지 없는지, 테스트 해볼 수 있다.
~~~
npm run test
~~~

3. 배포 단계
배포를 위한 build 폴더와 그 안에 많은 파일을 생성한다.
~~~
npm run build
~~~

### 도커를 이용하여 리액트 앱 실행해보기
개발 흐름은 다음과 같다.
1. Dockerfile 작성
   1-1. Dev Dockerfile.dev
   1-2. Prod Dockerfile
   실제 배포 후 각각 달리 적용되는 부분이 있어서 개발과 운영단계를 위한 도커파일을 분리한다.
   관용적으로 개발 단계에서 사용하는 도커 파일에 `.dev`를 붙여준다.
2. 도커 이미지 생성
3. 이미지를 이용해서 컨테이너 만들기
4. 컨테이너 안에서 앱 실행하기

다음과 같이 개발 단계의 dockerfile을 작성하고 `docker build`를 해준다.

그러면 Dockerfile을 찾을 수 없다고 에러가 뜬다.
왜 일까??

지금까지 `docker build ./`를 실행하면 현재 디렉토리 안에 존재하는 Dockerfile을 찾아서 실행했는데, 도커 파일 뒤에 `.dev`가 붙어서 찾지 못한 것이다.
그래서 `f옵셥`을 사용해 `이미지를 빌드 할때 쓰일 도커 파일을 임의로 지정`해준다.
~~~
docker build -f Dockerfile.dev .
~~~

cf) `도커 환경에서 리액트 앱을 실행할 때는 node_modules 폴더를 삭제해줘도 된다.`
리액트 앱을 실행 할 때 필요한 모듈들이 node_modules 안에 들어있다.
그러나 이미지를 빌드할 때 이미 npm install로 모든 모듈을 도커 이미지에 다운 받기 때문에 굳이 로컬 머신에 node_module를 둘 필요가 없다.

다음은 개발 단계에서 작성한 도커 파일이다.
~~~
FROM node:alpine

WORKDIR /usr/src/app

COPY package.json ./

RUN npm install

COPY ./ ./

CMD [ "npm", "run", "start" ]
~~~
- RUN npm install : 여기서 한번 node_modules가 생성
- COPY ./ ./ : 로컬머신에 node_module이 있다면 여기서 한번 더 이미지에 복사가 되서 중복이 된다.

### 생성된 도커 이미지로 로컬에서 리액트 앱 실행해보기
리액트 앱은 3000번 포트에서 실행된다.
로컬 포트와 컨테이너 내부의 포트를 매핑시켜준다.
그래야 컨테이너 안에서 실행되고 있는 리액트 앱에 도달할 수 있다.

기존에 포트를 매핑하는 옵션으로 `p옵션`을 사용했었다!
그런데 리액트쪽의 업그레이드로 인해서 `it옵션`을 붙여야만 실행이 가능하게 되었다.
~~~
docker run -it -p 3000:3000 {이미지 이름} 
~~~
-i : 상호 입출력
-t : tty를 활성화 하여 bash 쉘을 사용

### 도커 Volume을 이용한 소스 코드 변경
먼저 `COPY`와 `Volume`에 대해서 살펴보자.
- COPY : 로컬에 있는 server.js나 package.json 파일 등을 도커 컨테이너로 그대로 `복사`하는 것.
- Volume : 로컬에 있는 파일을 도커 컨테이너에 `매핑`하거나 `참조`해서 사용하는 것. 

Volume `v 옵션`을 사용해서 어플리케이션을 실행하는 방법은 다음과 같다.
~~~
docker run -it -p 3000:3000 -v /usr/src/app/node_modules -v $(pwd):/usr/src/app <이미지 아이디>
~~~
-v /usr/src/app/node_modules : 호스트 디렉토리에 node_modules는 없기에 컨테이너에 맵핑을 하지 말라고 하는 것
-v $(pwd):/usr/src/app : pwd 경로에 있는 디렉토리 혹은 파일을 /usr/src/app 경로에서 참조

COPY로 실행시키면 소스 코드를 수정해도 바로 반영되지 않는다. build를 해줘야 하기 때문이다.
반면에 Volume으로 실행시키면 코드 변경 내용이 바로 반영된다. 참조를 하고 있기 때문이다.

### 도커 컴포즈로 좀 더 간단하게 앱 실행해보기
1. docker-compose.yml 파일 작성하기
~~~
version: "3"
services: 
  react:
    build:
      context: .
      dockerfile: : Dockerfile.dev
    ports:
    - "3000:3000"
    volumes: 
    - /usr/src/app/node_modules
    - ./:/usr/src/app
    stdin_open: true
~~~
- 도커 컴포즈의 버전 : 3
- 이곳에 실행하려는 컨테이너들을 정의
- 컨테이너 이름 : react
- 도커 이미지를 구성하기 위한 파일과 폴더들이 있는 위치 (.)
- 도커 파일의 이름
- 포트 맵핑 ex) 로컬 포트 : 컨테이너 포트
- 로컬 머신에 있는 파일들 맵핑
- 리액트 앱을 끌때 필요 (버그 수정)
  
2. 도커 컴포즈로 실행
~~~
docker-compose up
~~~

### 리액트 앱 테스트 하기
도커를 이용한 리액트 앱에서 테스트를 진행해보자.
이미지 생성 커맨드는 다음과 같다.
~~~
docker build -f dockerfile.dev .
~~~

앱 실행을 해본다.
~~~
docker run -it 이미지 이름 npm run test
~~~
`-it` 옵션은 더 좋은 포맷으로 결과값을 보기 위한 옵션이다.

테스트 코드도 소스 코드와 마찬가지로 변경 되는대로 바로 build해서 반영이 되었으면 좋겠다.
동일하게 `volume`을 사용해서 테스트 코드를 참조하도록 한다.

1. docker-compose.yml 파일 작성하기
compose.yml 파일에 test용 컨테이너를 추가한다.
yaml 파일에 tests 컨테이너를 추가해줌으로서 앱을 시작할 때 두개의 컨테이너를 다 시작하게 된다. 
(먼저 리액트 앱을 실행하고 그 앱을 테스트를 한다.)
~~~
  tests:
    build:
      context: .
      dockerfile: Dockerfile.dev
    volumes:
      - /usr/src/app/node_modules
      - ./:/usr/src/app
    command: ["npm", "run", "test"]
~~~
- 컨테이너 이름 : tests
- 도커 이미지를 구성하기 위한 파일과 폴더들이 있는 위치 (.)
- 도커 파일의 이름
- 로컬 머신에 있는 파일들 맵핑
- 테스트 컨테이너 시작할 때 실행되는 명령어

2. 도커 컴포즈 build 하기
~~~
docker-compose up --build
~~~
이렇게 실행시킨 후 테스트를 변경해보면 자동으로 변경된 부분도 반영되어 테스트 된다.

### 운영환경을 위한 Nginx
개발환경과 운영환경에서 리액트가 실행되는 과정을 살펴보자.

개발환경에서는
브라우저에서 도메인을 입력을 하면, 
ex) 브라우저 - http://localhost:3000

리액트 컨테이너 내부의 개발 서버가 도메인과 매칭되는 정적 파일을 제공해준다.
ex) index.html, JS, CSS 파일 등등...

운영환경에서는
리액트 컨테이너 내부에 개발 서버가 존재하지 않아,
그 대신에 `NGINX`가 `정적 파일을 제공하는 웹 서버` 역할을 한다.
npm run build를 수행하고 build 된 파일을 브라우저로부터 요청받은 도메인에 맞게 제공한다.

그렇다면 왜 개발 환경과 운영 환경 서버를 달리 써야하는걸까??

개발 서버는 소스의 수정이 바로 반영이 되어야 하는데 nginx는 바로 반영이 되지 않는 단점이 있다.
반면에 운영 환경에서 개발 서버를 사용하기엔 개발 서버에 잡다한 많은 것들이 포함되어 무겁고 느리다는 단점이 있어
각 서버의 장단점 및 용도, 목적에 맞게 사용하는 것이 효율적이기 때문에 환경별로 서버를 달리 사용하는 것이다. 

### 운영환경 도커 이미지를 위한 Dockerfile 작성하기
운영환경을 위한 Dockerfile을 요약하자만 두가지 단계로 이루어져 있다.
1. build 파일을 생성한다. (Builder Stage)
2. nginx를 가동하고 첫번째 단계에서 생성된 build 폴더의 파일들을 웹 브라우저의 요청에 따라 제공해준다. (Run Stage)

~~~
# builder stage
FROM node:alpine as builder
WORKDIR /usr/src/app
COPY package.json ./
RUN npm install
COPY ./ ./
CMD [ "npm", "run", "build" ]

# run stage
FROM nginx
COPY --from=builder /usr/src/app/build /usr/share/nginx/html
~~~
- as builder : 여기 FROM 부터 다음 FROM 전까지는 모두 builder stage라는 것을 명시
- builder stage에서 생성된 파일과 폴더들은 /usr/src/app/build로 들어간다.
- --from=builder : 다른 stage에 있는 파일을 복사할 때 다른 stage 이름을 명시
- `/usr/share/nginx/html` 패스에 파일이 놓여있어야 nginx가 요청에 맞게 제공해줄 수 있다.
- working directory에 있는 파일들을 `/usr/share/nginx/html` 로 복사해주어 nginx가 사용할 수 있도록 해준다.
- nginx가 사용하는 해당 패스는 `/usr/share/nginx/html` 변경할 수 있다.

이렇게 다 작성을 했다면 Dockerfile로 이미지를 생성해보자.
~~~
docker build .
~~~
도커 파일명이 `Dockerfile.dev`가 아니라 일반 `Dockerfile`이므로 `-f 옵션`을 붙여서 build 해줄 필요가 없다.

이미지를 생성했다면 그 이미ㅏ지를 이용해서 앱을 실행해보자.
~~~
docker run -p 8080:80 {이미지 이름}
~~~
- nginx의 기본 사용포트는 80이다.

## 간단한 어플을 실제로 배포해보기(테스트 & 배포 부분)
### Travis CI 란?
Travis CI는 Github에서 진행되는 오픈소스 프로젝트를 위한 지속적인 통합 서비스(Continuous Integration)이다.
Travis CI를 이용하면 Github repository에 있는 프로젝트를 특정 이벤트에 따라 자동으로 `테스트`,
빌드하거나 `배포` 할 수 있다.
Private repository는 유료로 일정 금액을 지불하고 사용할 수 있다.

### Travis CI의 흐름
1. 로컬 Git
2. Github
3. Travis CI
4. AWS

- 로컬 Git에 있는 소스를 Github 저장소에 push 한다.
- Github의 해당 저장소에 소스가 push 되면 Travis CI에게 소스가 push 되었다고 알려준다.
- Travis CI는 업데이트 된 소스를 Github에서 가지고 온다.
- Github에서 가져온 소스의 테스트 코드를 실행해본다.
- 테스트 코드 실행 후 테스트가 성공하면 AWS같은 호스팅 사이트로 보내서 배포를 한다.

### Travis CI 이용 순서
Travis CI에서 계정을 만들때 github 계정과 동일한 이메일을 사용해야 연동이 된다.
Travis CI의 Settings에서 연결할 repository를 선택해준다. 

Github에서 Travis CI로 소스를 어떻게 전달 시킬것이며,
전달 받은 것을 어떻게 TEST 할 것이며,
그 테스트가 성공했을 때 어떻게 AWS에 전달해서 배포할 것인지를 설정해주어야 한다.

이러한 설정을 위해서 `.travis.yml` 파일을 작성해주어야 한다.

cf)
설정을 위해서
Docker: docker-compose.yml
Travis CI: .travis.yml 

### .travis.yml 파일 작성하기 (테스트까지)
전체적인 흐름은 다음과 같다.
1. Test를 수행하기 위한 준비
   - 도커 환경에서 리액트 앱을 실행하고 있으니 Travis CI에서도 도커 환경을 구성한다.
   - 구성된 도커 환경에서 Docker.dev를 이용해서 도커 이미지를 생성한다.
2. Test를 수행하기
   - 어떻게 Test를 수행할 것인지 설정해준다.
3. AWS로 배포하기
   - 어떻게 AWS에 소스코드를 배포할 것인지 설정해준다.

`.travis.yml`은 다음과 같이 작성해본다.
~~~
sudo: required

language: generic

services:
   - docker

before_install:
   - echo "start Creating an image with dockerfile"
   - docker build -t ijaysong/docker-react-app -f Dockerfile.dev .

script:
   - docker run -e CI=true ijaysong/docker-react-app npm run test -- --coverage

after_success:
   - echo "Test Success"
~~~
- sudo : 관리자 권한 갖기
- language: 언어(플랫폼)을 선택
- services: 도커 환경 구성
- before_install : 스크립트를 실행하기 전에 수행할 내용 (도커 이미지 build)
- script: 테스트 코드를 적은 스크립트를 실행
- after_success: 테스트 성공 후

### AWS 알아보기
AWS에서 사용할 두가지 기능에 대해서 살펴보자.
1. EC2 (Elastic Compute Cloud)
- 한대의 컴퓨터를 임대한다고 생각하면 된다.
- AWS 클라우드에서 제공하는 확장식 컴퓨팅
- 해당 컴퓨터에 OS를 설치하고 웹 서비스를 위한 프로그램들(웹 서버, DB)을 설치해서 사용하면 된다.
- 1대의 컴퓨터를 하나의 EC2 인스턴스라고 부른다.

2. EB (Elastic Beanstalk)
- EC2나 DB, Auto-Scaling 그룹, 로드 벨런서, 보안 그룹 등등을 포함하는 하나의 환경이라고 이해하면 된다.
- 소프트웨어를 업데이트 할때마다 자동으로 이 환경을 관리해준다.
=> EB를 사용해서 배포를 해보겠다.

### Elastic Beanstalk 환경 구성하기
1. AWS의 Elastic Beanstalk 페이지로 이동
2. 새 환경 생성 > 웹 서버 환경 선택
3. 애플리케이션 이름 및 플랫폼을 선택한다.
   - 애플리케이션 이름 : docker-react-app
   - 플랫폼 : Docker
   - 플랫폼 브랜치 : Docker running on 64bit Amazon Linux 64
   - 플랫폼 버전 : 3.0.3
4. 애플리케이션 생성

### .travis.yml 파일 작성하기 (배포 부분)
도커 이미지를 생성 후 어플을 실행하여 테스트 하는 부분까지 travis 설정을 하였다.
이제는 테스트에 성공한 소스를 AWS Elastic Beanstalk에 자동으로 배포하는 부분을 travis 파일에 넣어줄 차례이다.

다음은 .travis.yml 파일에 추가로 넣어줄 내용이다.
~~~
deploy:
  provider: elasticbeanstalk
  region: "ap-northeast-2"
  app: "docker-react-app"
  env: "DockerReactApp-env"
  bucket_name: "elasticbeanstalk-ap-northeast-2-972153559337"
  bucket_path: "docker-react-app"
  on:
    branch: main
~~~
- provider : 외부 서비스 표시 (s3, elasticbeanstalk, firebase 등등...)
- region: 현재 사용하고 있는 AWS의 서비스가 위치하고 있는 물리적 장소
- app: 생성된 어플리케이션 이름
- env: 환경의 이름
- bucket_name: 해당 elasticbeanstalk을 위한 s3 버켓 이름 
  ex) Travis CI에서 가지고 있는 파일을 압축해서 S3에 보내기 때문에 bucket_name을 지정해주어야 한다.
  ex) elasticbeanstalk을 설치하면 자동으로 S3까지 설치된다. 커다란 환경이기 때문에.
- bucket_path : 어플리케이션의 이름과 동일
- on
  - branch : 어떤 브랜치에 Push를 할때 AWS에 배포를 할 것인지

하지만 Travis CI는 아무런 허가 없이 AWS에 파일을 전송할 수 없다.
어떻게 해야할까??

### Travis CI의 AWS접근을 위한 API 생성
Travis CI와 AWS가 소통을 할 수 있도록 인증하는 부분을 설정해보자.

#### 소스 파일을 전달하기 위한 접근 요건
~~~
Github -> Travis CI -> AWS
~~~
1. Github -> Travis CI
- Travis CI 아이디 로그인 시, Github 연동으로 인증해준다.

2. Travis CI -> AWS
- AWS에서 제공해주는 `Secret Key`를 Travis yml 파일에다가 적어주면 된다.

그렇다면 `Secret Key`는 어떻게 받아와야 할까??

### Secret, Access API Key 받는 순서
1. IAM USER 생성
   `IAM`(Identity and Access Management)란, 
   AWS 리소스에 대한 액세스를 안전하게 제어할 수 있는 웹 서비스이다.
   IAM을 사용하여 리소스를 사용하도록 인증(로그인) 및 권한부여(권한 있음)된 대상을 제어한다.

   `Root 사용자`는 처음 가입해서 사용할 때의 계정으로, AWS 서비스 및 리소스에 대한 완전한 액세스 권한이 있다.
   하지만 보안상 Root 사용자를 사용하는 것은 좋지 않기 때문에, IAM 유저를 생성한다.
   `IAM 사용자`는 root 사용자가 부여한 권한만 가지고 있다. 배포를 위해 생성한 beanstalk에 대한 권한을 제공해보자.

   액세스 키와 비밀 액세스 키는 한번만 발급이 되므로 복사하여 어딘가에 잘 보관해두는 것을 권장한다.

2. API 키를 Travis yml 파일에 적어주기
직접 API 키를 Travis yml 파일에 적어주면 노출이 되기 때문에, 다른 곳에 적고 그것을 가져와야 한다.

API 키를 숨겨서 적어놓을 곳
Travis CI > More Options > Settings > Environment Variables
`Travis CI 환경변수`에 액세스 키와 비밀 엑세스 키를 입력한다.
- AWS_ACCESS_KEY
- AWS_SECRET_ACCESS_KEY   

## 복잡한 어플을 실제로 배포해보기 (개발 환경 부분)
멀티 컨테이너 or 풀 스택 어플리케이션으로 구성해보겠다. (컨테이너를 여러개 활용하겠다는 말이다.)
ex) 
- Nginx 컨테이너
- React JS 컨테이너
- Node JS 컨테이너
- Mysql 컨테이너

설계는 이하 두가지 방법으로 진행될 수 있는데, Nginx의 Proxy를 이용한 설계 방법으로 진행해보겠다.

1. Nginx의 Proxy를 이용한 설계 
다음과 같은 방법으로 요청을 받는다.
~~~
axios.get(`/api/values`)
~~~
- 요청을 routing 해주는 설계
- 장점
  - Request를 보낼 때, URL 부분의 host 이름이 바뀌어도 변경시켜 주지 않아도 된다.
  - 포트가 바뀌어도 변경을 안해줘도 된다.
- 단점
  - nginx 설정, 전체 설계가 다소 복잡하다.

1. Nginx는 정적파일을 제공만 해주는 설계
~~~
axios.get(`http://localhost:5000/api/values`)
axios.get(`http://johnahn.com:5000/api/values`)
~~~
- 장점 : 설계가 다소 간단하여 구현하는게 더 쉽다.
- 단점 : host name 이나 포트 변경이 있을 때, Request URL도 변경시켜줘야 한다.

### 개발 흐름
1. 전체 소스 코드 작성 (NodeJS, React)
2. Dockerfile 작성
   - 개발환경 Dockerfile.dev
   - 운영환경 Dockerfile
3. Docker-compose 작성
4. 깃헙에 push
   - feature -> main 머지
5. Travis CI
   - 테스트 성공 -> Dockerfile을 이용해서 Image 생성 (빌드) -> Docker Hub으로 전달
6. Docker Hub
   - Travis CI에서 전달받은 이미지 보관 -> AWS에서 가져가려 할때 전달
7. AWS Elastic Beanstalk
   - Travis CI에서 빌드된 이미지를 이용해서 배포하기

### Node JS 구성하기
1. backend 라는 폴더 만들기 : Node JS 소스들이 들어가는 장소

2. package.json 파일 만들기 : npm init

3. package.json 파일 안에 스크립트와 사용할 모듈들 명시해주기
~~~
{
  "name": "backend",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "dependencies": {
    "express": "4.16.3",
    "mysql": "2.16.0",
    "nodemon": "1.18.3",
    "body-parser": "1.19.0"
  },
  "author": "",
  "license": "ISC"
}
~~~
- test : test 코드를 실행할 때 사용
- start : express 서버를 시작할때 사용
- dev : nodemon을 이용하여 express 서버를 시작할 때 사용
  `nodemon`이란, Node JS로 작성한 코드를 수정했을 때, 서버를 껐다가 다시 빌드하지 않고, 서버가 계속 켜진 상태에서 수정된 내용이 반영되도록 해주는 확장 모듈
- express : 웹 프레임워크 모듈
- mysql : mysql을 사용하기 위한 모듈
- body-parser : 클라이언트에서 오는 요청의 본문을 해석해주는 미들웨어 

4. 시작점이 되는 server.js 만들기
: 앱을 실행할 때 `node server.js`로 시작하니 server.js 파일이 시작점이 된다.

5. server.js의 기본 구조 작성
~~~
const express = require('express');
const bodyParser = require('body-parser');

const app = express();

app.use(bodyParser.json());

app.listen(5000, () => {
    console.log('어플리케이션이 서버 5000번 포트에서 되었습니다.');
})
~~~

6. mysql을 연결하기 위한 db.js 파일 생성


7. Host, 유저 이름, 비밀번호, 데이터베이스 이름을 명시해서 Pool을 생성해줌.
   그리고 생성한 pool을 다른 부분에서 쓸 수 있게 export 해줌.
~~~
var mysql = require("mysql");
var pool = mysql.createPool({
    connectionLimit: 10,
    host: 'mysql',
    user: 'root',
    password: 'johnahn',
    database: 'myapp',
});
exports.pool = pool;
~~~

8. export 된 pool을 시작점인 server.js 에서 불러오기
server.js에 다음 내용 추가
~~~
const db = require('./db');
~~~

9. 이 어플에서 필요한 두가지 API 작성하기 (server.js)
    - 1) 입력을 받은 keyword를 저장하는 API
    - 2) 저장된 keyword를 화면에 뿌려주는 API
~~~
// DB lists 테이블에 있는 모든 데이터를 프론트 서버에 보내주기
app.get('/api/values', function(req, res, next) {
    db.pool.query('SELECT * FROM lists;', 
    (err, results, fields) => {
        if (err)
            return res.status(500).send(err)
        else
            return res.json(results)
    })
})

// 클라이언트에서 입력한 값을 데이터베이스 lists 테이블에 넣어주기
app.post('/api/value', function (req, res, next) {
    db.pool.query(`INSERT INTO lists (value) VALUES ("${req.body.value}");`, 
    (err, results, fields) => {
        if (err)
            return res.status(500).send(err)
        else
            return res.json({ success: true, value: req.body.value })
    })
})
~~~

### React JS 구성하기
1. Create-React-App으로 리액트 앱 생성하기
다음 커맨드를 실행하면 React JS 가 다운로드 된다.
~~~
npx create-react-app frontend
~~~

2. App.js 파일 안에 원하는 UI를 생성
- Input 박스, Button 추가

3. UI를 위한 CSS 코드 작성

4. 데이터 흐름을 위한 State 생성
App.js 파일에 다음 내용을 지정해준다.
~~~
const [lists, setLists] = useState([])
const [value, setValue] = useState("")
~~~
- useState : useState을 사용하기 위해서 react 라이브러리에서 가져옴
- lists: 데이터베이스에 저장된 값을 가져와서 화면에 보여주기 전 이 Stage에 넣어둠
- value: input 박스에 입력한 값이 이 stage에 들어감

5. DB에서 데이터를 가져오기 위해, 필요한 useEffect 넣어주기
- useEffect: useState을 사용하기 위해서 react 라이브러리에서 가져옴

6. 나머지 해야할 것들 처리하기
- useEffect에서 DB에 있는 값을 가져온다.
- changeHandler : input 박스에 입력을 할때 onChange가 발생 할때마다 value State을 지정해준다.
- submitHandler : 값을 input 박스에 입력하고, 입력한 값이 DB에 저장한다.

### 리액트 앱을 위한 도커 파일 만들기
전체 소스 코드 작성을 완성했다. (Node JS + React JS)
개발환경과 운영환경 Dockerfile을 따로 따로 만들어야 한다.
먼저 React JS을 위한 도커파일을 작성해보겠다.

< 개발 환경을 위한 Dockerfile >
~~~
FROM node:alpine

WORKDIR /app

COPY package.json ./

RUN npm install

COPY ./ ./

CMD [ "npm", "run", "start" ]
~~~
- FROM : 베이스 이미지를 도커 허브에서 가져온다.
- WORKDIR : 해당 어플의 소스 코드들이 들어가게 된다.
- COPY : 소스 코드가 비뀔 때마다 종속성까지 다시 복사를 해주는 수고를 하지 않기 위해 먼저 종속성 목록을 담고 있는 package.json을 복사한다.
- RUN : package.json에 명시된 종속성을 다운 받는다.
- COPY : 모든 소스코드들을 WORKDIR로 복사해준다.
- CMD : 이 컨테이너가 실행될 때 같이 실행할 명령어를 지정해준다.

< 운영 환경을 위한 Dockerfile >
~~~
FROM node:alpine
WORKDIR /app
COPY package.json ./
RUN npm install
COPY ./ ./
CMD [ "npm", "run", "start" ]

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html
~~~
크게 두 단계로 나뉜다.

1. Build 파일을 생성하는 단계
- nginx가 제공해줄 Build 파일들을 생성하는 단계이다.

2. Nginx에 Build 파일을 제공하는 단계
- Nginx를 가동하고 윗 단계에서 생성된 빌드 파일들을 제공해준다.
- default.conf에서 해준 설정을 nginx 컨테이너 안에 있는 설정이 되게 복사를 해준다.

### 프론트 Nginx 설정파일 작성하기
클라이언트에서 받은 요청을 넘겨 받으면 프론트에 있는 Nginx가 받아서 요청에 따라 빌드 파일을 제공하는 역할을 한다.
이번 단계에서는 프론트에 있는 Nginx의 설정파일을 작성해보겠다.

~~~
server {
    listen 3000;

    location / {

        root /usr/share/nginx/html;

        index index.html index.html;

        try_files $uri $uri/ /index.html
    }
}
~~~
- listen 3000
: 운영환경용 Dockerfile에서도 적었듯이 서버 포트는 3000이다.

- location / 
: 클라이언트에서 넘어오는 요청 중 `/`은 프론트 용이다. `/`로 넘어오는 요청을 받을 것이라는 것을 지정하고 있다.

- root 
: HTML 파일 등 빌드 파일이 위치하는 디렉토리이다.

- index
: 사이트의 index 페이지로 할 파일명이다.

- try_files
: React Router를 사용해서 페이지 간 이동할 때 이 부분이 필요하다.
React 는 Single Page Application이다.
/home에 접속하려고 할 때 /home에 매칭되는 것이 없으면, 대안책으로 index.html을 제공해서 /home으로 라우팅 시킬 수 있게 임의로 설정해주는 것이다.

### 노드 앱을 위한 도커 파일 만들기
1. backend 폴더 안에 Dockerfile을 생성한다.
2. 개발 환경을 위한 Dockerfile을 작성한다.
3. 운영환경을 위한 Dockerfile을 작성한다.
~~~
FROM node:alpine

WORKDIR /app

COPY ./package.json ./

RUN npm install

COPY . .

# 개발환경
CMD ["npm", "run", "dev"]

# 운영환경
# CMD ["npm", "run", "dev"]
~~~
개발환경에서 start가 아닌 dev를 실행한 이유는
코드가 변경될 때 바로 반영을 시켜주게 해주는 nodemon이라는 모듈을 사용하기 위해서!
nodemon은 node를 바로 중단 시켰다가 다시 재기동 시켜주는 역할을 한다.

운영환경에서는 소스를 바꿀때마다 반영할 필요가 없기 때문에 start를 실행한다.

cf)
"start": "node server.js",
"dev": "nodemon server.js"

### DB에 관해서
개발환경과 운영환경 각각 DB 구성을 어떻게 해야할까!
실제 중요한 데이터를 다루는 운영환경에서는 더욱 안정적인 AWS RDS를 사용해보겠다.

1. 개발 환경 : 도커 환경 이용
 - Server에서 MySQL로 이어지는 흐름을 Elastic Beanstalk 안에서 처리

2. 운영 환경 : AWS RDS 서비스 이용
- Elastic Beanstalk 내부의 Server와 AWS RDS의 MySQL를 연결해서 처리

### MYSQL을 위한 도커 파일 만들기
현재 MySQL과 NodeJS를 연결하는 코드는 작성되어 있다.
이제 MySQL을 도커 이미지를 통해서 설치를 해보겠다.

<MySQL 도커 파일 작성>
1. mysql이라는 폴더를 Root 디렉토리에 생성한 후 그 안에 Dockerfile 생성
2. Dockerfile 작성
~~~
FROM mysql:5.7
~~~

3. MySQL을 시작할 때 Database와 Table이 필요한데 그것들을 만들 장소를 만들어준다.
4. Database와 Table을 만들어준다.
5. 한글도 저장할 수 있도록 설정해준다. (my.cnf)
아무런 설정이 없이 실행시키면 한글을 DB에 넣었을 때 깨지는 현상이 발생한다.
설정해준것을 도커 컨테이너 내부의 my.conf 파일에 덮어씌워주는 작업을 추가한다.
~~~
FROM mysql:5.7

ADD ./my.cnf /etc/mysql/conf.d/my.cnf
~~~

### NGINX를 위한 도커 파일 만들기
클라이언트에서 Request를 보낼 때, Nginx를 통해서 프론트와 서버로 나눠서 보내줄 수 있다.
Request는 다음과 같이 나누어서 처리할 것이다.
- /api로 오는 요청 : 서버
- /로 오는 요청 : 프론트

현재 Nginx가 쓰이는 곳은 두군데이다. 서로 다른 이유로 쓰이고 있다.
하나는 Proxy를 이유로, 다른 하나는 Static 파일을 제공해주는 역할을 하고 있다.

Nginx가 요처을 나눠서 보내주는 기준은
location이 /로 시작하는지, /api로 시작하는지에 따라서 나눠준다.
/로 시작하면 ReactJS로
/api로 시작하면 NodeJS로 보내준다.

이러한 proxy 기능을 위해 먼저 Nginx를 설정해주어야 한다.
1. nginx 폴더와 default.conf 파일, Dockerfile 생성
2. default.conf 파일에 proxy 기능 작성
~~~
upstream frontend {
    server frontend:3000;
}

upstream backend {
    server backend:5000;
}

server {
    listen 80;

    location / {
        proxy_pass http://frontend;
    }

    location /api {
        proxy_pass http://backend;
    }

    location /sockjs-node {
        proxy_pass http://frontend;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
    }
}
~~~
- 3000번 포트에서 frontend가 돌아가고 있다는 것을 명시해줌.
- 5000번 포트에서 backend가 돌아가고 있다는 것을 명시해줌.
- Nginx 서버 포트 80번으로 열어준다.
- location에는 우선 숭위가 있는데 / 그냥 이렇게만 되는 것은 우선 순위가 가장 낮다.
그래서 /api로 시작하는 것을 먼저 찾고, 그게 없다면 /로 찾아 그 요청을 http://frontend로 보내면 된다.
- /api로 들어오는 요청을 http://backend로 보내준다.
- /sockjs-node에 대한 부분이 없다면 web socket connection 관련 에러가 일어한다. (개발 환경에서만 발생) -> 에러 처리를 위한 것

3. Nginx를 위한 도커 파일 작성하기
~~~
FROM nginx
COPY ./default.conf /etc/nginx/conf.d/default.conf
~~~
- Nginx 베이스 이미지 가져와서
- 작성된 conf 파일을 컨테이너에서 실행될 Nginx에도 적용될 수 있게 COPY 해주기

### Docker Compose 파일 작성하기
각각의 컨테이너를 위한 도커 파일을 작성했다.
컨테이너 간에는 통신이 불가능 하기 때문에, 서로 연결을 시켜주기 위해서 Docker Compose를 작성해보겠다.

1. 먼저 docker-compose.yml 파일을 생성한다.
2. 각각의 서비스들을 위한 틀을 만든다.
~~~
version: "3"
services: 
  frontend:

  nginx:

  backend:

  mysql:
~~~

3. frontend 서비스를 위한 설정을 해준다.
~~~
  frontend:
    build:
      dockerfile: dockerfile.dev
      context: ./frontend
    volumes:
      - /app/node_modules
      - ./frontend:/app
   stdin_open: true
~~~
- build : 개발환경을 위한 Dockerfile이 어디에 있는지 알려준다.
- volumes : 코드를 수정 후 다시 이미지를 build 하는 것 없이 수정된 코드가 반영될 수 있게 volume을 이용해준다.
- stdin_open: 리액트 앱을 종료할 때 나오는 버그를 잡아줌

4. nginx 서비스를 위한 설정을 해준다.
~~~
  nginx:
    restart: always
    build:
      dockerfile: Dockerfile.dev
      context: ./nginx
    ports: 
      - "3000:80"
~~~
- restart : 재시작 정책
  - restart: no -> 어떠한 상황에서도 재시작을 하지 않는다.
  - restart: always -> 항상 재시작을 한다.
  - restart: on-failure -> on-failure 에러 코드와 함꼐 컨테이너가 멈추었을 때만 재시작을 한다.
  - restart: unless-stopped -> 개발자가 임의로 멈추려고 할 때 빼고는 항상 재시작을 한다.

5. backend 서비스를 위한 설정을 해준다.
~~~
  backend:
    build:
      dockerfile: Dockerfile.dev
      context: ./backend
    container_name: app_backend
    volumes:
      - /app/node_modules
      - ./backend:/app
~~~

6. mysql 서비스를 위한 설정을 해준다.
~~~
  mysql:
    build: ./mysql
    restart: unless-stopped
    container_name: app_mysql
    ports:
      - "3306:3306"
    volumes: 
      - ./mysql/mysql_data:/var/lib/mysql
      - ./mysql/sqls/:/docker-entrypoint-initdb.d/
    environment:
      MYSQL_ROOT_PASSWORD: johnahn
      MYSQL_DATABASE: myapp
~~~
- restart: unless-stopped -> 개발자가 임의로 멈추려고 할 때 빼고는 항상 재시작을 한다.
- volumes:

### Docker Volume을 이용한 데이터 베이스 데이터 유지하기
docker-compose 파일에서 volumes 부분이 어떤 역할을 하는 것일까?

현재까지는 리액트나 노드쪽에서 코드를 업데이트 할때 그 코드가 바로 어플리케이션에 적용될 수 있게 해주기 위해서 사용했다.
이번에는 데이터베이스의 저장된 자료를 컨테이너를 지우더라도 자료가 지워지지 않도록 해주기 위한 용도로 volume을 사용할 것이다.

원래는 컨테이너를 지우면 컨테이너에 저장된 데이터들이 지워지게 된다.
1. 도커 이미지로 컨테이너 생성
2. 도커 이미지는 컨테이너 생성 후 읽기 전용이 된다.
3. 컨테이너 안에서 변화
4. 변화된 데이터를 컨테이너 안에 저장
5. 컨테이너 삭제 시 컨테이너 안에 저장된 데이터도 함께 삭제된다.

~~~
    volumes: 
      - ./mysql/mysql_data:/var/lib/mysql
      - ./mysql/sqls/:/docker-entrypoint-initdb.d/
~~~

볼륨 내부에서 컨테이너 내부의 파일들이 로컬에 있는 파일을 바라보도록 참조를 지정해준다.
ex) <로컬에 있는 파일들>:<컨테이너 내부의 파일들>

도커 컨테이너의 Volume으로 인해 컨테이너 내부에 데이터를 저장하는 것이 아니라 `호스트 파일 시스템`이라고 하는 Docker Area에 저장이 된다.
그 중에서도 도커에 의해서만 통제가 되는 도커 Area에 저장이 되므로 도커 컨테이너를 삭제하더라도 변화된 데이터는 호스트 파일 시스템 안에 남아있게 된다.

### 도커 환경의 MYSQL 부분 정리하기
지금까지와는 달리 MySQL을 도커 안에서 돌아가도록 하는 것이 아닌, AWS에서 돌아가도록 수정할 것이다.
MySQL에 대한 연결 부분만 남겨두고 나머지 부분은 다 삭제하도록 하겠다.

1. docker-compose.yml에서 MySQL 부분 지워주기

2. mysql 폴더 지워주기
docker-compose.yml에서 mysql 부분을 코멘트 처리 해주었기 때문에 지우지 않아도 작동 안된다.

3. AWS에서 생성한 DB 정보는 backend의 db.js에 내용을 다시 넣어준다.

### GITHUB에 소스코드 올려보기
1. new repository 만들기

2. 로컬 git 저장소 만들기
~~~
git init
~~~

3. git에 올리고 싶지 않는 파일을 `.gitignore`로 지정해준다.
- backend : node_modules (종속성을 관리하는 파일)
- mysql : mysql_data (DB 데이터를 저장하는 파일)

4. 현재까지의 소스를 로컬 git 저장소에 저장
~~~
git add .
git commit -m "first commit"
~~~

5. 로컬 git 저장소와 github remote를 연결시키기
~~~
git remote add origin {repository url}
~~~

6. 로컬 git 저장소에 있는 소스를 github에 업로드 시키기
~~~
git push origin master
~~~

### Travis CI Steps
github의 master 브랜치에 새로 업데이트 된 소스가 올라왔다면, 해당 소스를 Travis CI에서 가져와야 한다.
Travis CI에서의 동작은 다음과 같이 이루어진다.

< Travis CI에서의 흐름 >
1. 깃헙에서 코드를 Push한다.

2. Travis CI가 자동으로 코드를 가져온다.

3. 가져온 코드로 `테스트 코드`를 실행한다.

4. 성공하면 운영 환경 이미지들을 Build 한다.

5. 빌드 된 이미지들을 `DockerHub`로 보낸다.
DockerHub는 유명한 이미지를 다운받을 수 있을 뿐만 아니라, 자신이 만든 이미지도 업로드 할 수 있다.
DockerHub에 빌드된 이미지를 보내고 AWS에서 그 이미지를 가져가기 때문에, EB 안에서 다시 이미지를 빌드하지 않아도 된다.
(모든 과정 중에 빌드가 한번만 이루어진다.)

6. AWS EB에 DockerHub에 이미지를 보냈다고 알려준다.

7. AWS EB에서 DockerHub에 있는 이미지를 가져온 후에 배포를 한다.

< 작업 순서 >
1. Travis CI 사이트에서 깃헙 아이디로 로그인
깃헙 아이디로 로그인 해야 깃헙에 있는 repository에 접근 할 수 있다.

2. Settings에서 작업한 repository를 활성화시켜준다.
repository가 없는 걸로 나온다면 sync account 버튼을 눌러서 최신화를 시켜준다.

3. 해당 저장소의 Setting 버튼(활성화 버튼)을 눌러서 Travis CI에게 Github 저장소의 소스가 변경될 때마다 소스를 가져와서 `테스트`하고 `배포`하라고 알려준다.

### .travis.yml 파일 작성하기
1. 파일 생성
   - .travis.yml 파일을 생성한다.

2. Test를 수행하기 위한 준비
   - 앱을 도커 환경에서 실행하고 있으니 Travis CI에게 도커 환경으로 만들 것이라고 선언해준다.
   - 구성된 도커 환경에서 Dockerfile.dev를 이용해서 도커 이미지를 생성한다.
   ~~~
   before_install:
       - docker build -t ijaysong/react-test-app -f ./frontend/Dockerfile.dev ./frontend
   ~~~

   ~~~
   docker build -t <도커 아이디>/<어플 이름> -f <Dockerfile 경로> 빌드해야할 파일들이 있는 경로
   ~~~

3. Test를 수행하기
   - 생성된 테스트 이미지를 이용해서 테스트를 수행한다.
   ~~~
   script:
       - docker run -e CI=true ijaysong/react-test-app npm run test
   ~~~

4. 모든 프로젝트의 운영버전 이미지를 빌드하기
   - 테스트가 성공했다면 하나하나의 프로젝트의 운영버전 이미지를 빌드하는 설정을 해준다.
   ~~~
   after_success:
       - docker build -t ijaysong/docker-frontend ./frontend
       - docker build -t ijaysong/docker-backend ./backend
       - docker build -t ijaysong/docker-nginx ./nginx
   ~~~

5. 빌드된 이미지를 도커 허브에 보내주기
   - 도커 허브에 빌드 된 파일을 넣어주기 위해서 도커 허브에 로그인 한다.
   ~~~
       - echo "$DOCKER_HUB_PASSWORD" | docker login -u "$DOCKER_HUB_ID" --password-stdin
   ~~~
   ID나 패스워드를 적어서 깃헙에 push하면 개인 정보 유출의 위험이 있으므로 직접적으로 적지 않고,
   Travis CI에 도커 허브 ID와 패스워드를 미리 넣어준다.
   Travis CI에서 작업하고 있는 해당 Repository의 Setting에 들어가서 Environment Variables에 다음과 같은 값을 지정해준다.
   - DOCKER_HUB_ID
   - DOCKER_HUB_PASSWORD
   이렇게 도커 허브 아이디와 비밀번호라는 환경변수를 만들어 주면 Travis CI가 Script에서 이 변수를 읽을 때 자동으로 해당하는 값을 가져가서 로그인 할 수 있다.

   - 빌드된 이미지를 도커 허브에 보내준다.
   ~~~
       - docker push ijaysong/docker-frontend
       - docker push ijaysong/docker-backend
       - docker push ijaysong/docker-nginx
   ~~~

6. 배포하기
   - AWS Elastic Beanstalk이 업데이트된 빌드 이미지를 가져와서 배포 할 수 있게 걸정해준다.

### Dockerrun.aws.json에 대해서
Dockerrun.aws.json파일을 써야 Elastic Beanstalk에서 어플리케이션을 작동 시킬 수 있다.
왜 그럴까?

1. Dockerfile이 하나인 경우
Dockerfile이 하나만 있으면 Elastic Beanstalk에서 이미지를 실행시켜서 컨테이너를 만든다.

ex)React App
이전에 리액트만 이용한 어플리케이션을 만들때는 Dockerfile이 하나라서 그 도커 파일을 Elastic Beanstalk에 전달하면 EB가 알아서 처리를 해주면
그 빌드된 이미지를 돌려서 어플리케이션을 실행했기 때문에 아무런 설정을 해주지 않아도 됐다.

2. Dockerfile이 여러 개인 경우
Dockerfile이 여러 개 있으면 Elastic Beanstalk이 어떻게 처리해야 될지 모르고 헷갈리게 된다.
이때 어떤 파일을 실행시킬지 설정해주는 파일이 바로 `Dockerrun.aws.json`이다.

ex) Full Stack App
이번에 작성한 어플리케이션에는 노드, MySQL, Nginx 등을 위한 Dockerfile이 존재하는데
EB의 입장에선 어떤 파일을 먼저 실행하고 어떻게 행동을 취해야 하는지 알 수 없어 자동으로 프로세스를 해나갈 수 없기 때문에 임의로 설정을 해주어야한다.

<AWS에서 말하는 Dockerrun.aws.json 파일의 정의>
`Dockerrun.aws.json`파일은 Docker 컨테이너 세트를 Elastic Beanstalk 애플리케이션으로 배포하는 방법을 설명하는
Elastic Beanstalk 고유의 JSON 파일이다.
Dockerrun.aws.json 파일을 멀티 컨테이너 Docker 환경에서 사용할 수 있다.
Dcoekrrun.aws.json은 환경에서 각 컨테이너 인스턴스 (Docker 컨테이너를 호스트하는 Amazon EC2 인스턴스)에 배포할 컨테이너 및 탑재할 컨테이너의 호스트 인스턴스에서 생성할 데이터 볼륨을 설명한다.

=> EB는 다중 컨테이너를 어떻게 실행시켜야 할지 잘 모르기 떄문에 Dockerrun.aws.json 파일이 어떻게 작동시킬지 알려준다. (Task Definition : 작업정의)

<AWS에서 말하는 Task Definition(작업 정의)에서 지정할 수 있는 것들>
- 작업의 각 컨테이너에서 사용할 도커 이미지
- 각 작업 또는 작업 내 각 컨테이너에서 사용할 CPU 및 메모리의 양
- 사용할 시작 유형으로서 해당 작업이 호스팅되는 인프라를 결정
- 작업의 컨테이너에 사용할 도커 네트워킹 모드
- 작업에 사용할 로깅 구성
- 컨테이너가 종료 또는 실패하더라도 작업이 계속 실행될지 여부
- 컨테이너 시작 시 컨테이너가 실행할 명령
- 작업의 컨테이너에서 사용할 데이터 볼륨
- 작업에서 사용해야 하는 IAM 역할

=> 작업 정의를 등록할 때는 Container Definition (컨테이너 정의)을 명시해줘야 한다.
Dockerrun.aws.json 안에 Container Definition에 명시해주며 도커 데몬으로 전해진다.

### Dockerrun.aws.json 파일 작성하기
1. Dockerrun.aws.json 파일 생성
2. Container Definitions을 작성하기
~~~
{
   "AWSEBDockerrunVersion": 2,
   "containerDefinitions": [
       {
           "name": "frontend",
           "image": "ijaysong/docker-frontend",
           "hostname": "frontend",
           "essential": false,
           "memory": 128
       },
       {
           "name": "backend",
           "image": "ijaysong/docker-frontend",
           "hostname": "backend",
           "essential": false,
           "memory": 128
       },
       {
           "name": "nginx"
           "image": "ijaysong/docker-nginx",
           "hostname": "nginx",
           "essential": true,
           "portMappings": [
               {
                   "hostPort": 80.
                   "containerPort": 80
               }
           ],
           "links": ["frontend", "backend"],
           "memory": 128
       }
   ]
}
~~~
객체 안에서 하나의 컨테이너를 정의한다.

- AWSEBDockerrunVersion : Dockerrun 버전 2로 지정
- containerDefinitions : 이 안에서 컨테이너들을 정의해준다.

- name : 컨테이너의 이름
- image : Docker 컨테이너를 구축할 온라인 Docker 리포지도리의 Docker 이미지가 이름이다.
- hostname : 호스트 이름. 이 이름을 이용해서 도커 컴포즈를 이용해 생성된 다른 컨테이너에서 접근이 가능하다.
- essential : 컨테이너가 실패할 경우 작업을 중지해야 하면 true이다.
           필수적이지 않은 컨테이너는 인스턴스의 나머지 컨테이너에 영향을 미치지 않고 종료되거나 충돌할 수 있다.
- memory : 컨테이너용으로 예약할 컨테이너 인스턴스에 있는 메모리 양이다.
           컨테이너 정의에서 memory 또는 memoryReservation 파라미터 중 하나 또는 모두에 0이 아닌 정수를 지정하면 된다.
- portMappings : 컨테이너에 있는 네트워크 지점을 호스트에 있는 지점에 매핑한다.
- links : 연결할 컨테이너의 목록. 연결된 컨테이너는 서로를 검색하고 안전하게 통신할 수 있따.
- nignx : links를 통해서 Frontend와 Backend를 연결해 통신

### 다중 컨테이너 앱을 위한 Elastic Beanstalk 환경 생성
1. AWS에서 Elastic Beanstalk을 생성해준다.
Create Application 버튼 클릭

2. 어플리케이션 이름 정하기
docker-fullstack-app

Elastic Beanstalk은 EC2 인스턴스, Security 그룹, Auto-Scaling 그룹 등을 컨트롤 한다.
트래픽이 많지 않을 땐 하나의 EC2에서 처리하지만 트래픽이 많아지면 로드 밸런서에서 EC2 인스턴스를 여러개 만들어서 처리한다.

### VPC (Virtual Private Cloud)와 Security Group 설정하기
AWS의 RDS를 이용해 MySQL을 어플리케이션과 연결하기 위해서 VPC와 Security Group을 설정해주어야 한다.
또한 EB 인스턴스와 RDS(MySQL)는 기본적으로 연결이 되어 있지 않기 때문에 연결을 해주어야 한다.

#### VPC란?
Amazon Virtual Private Cloud(VPC)의 약자로,
AWS 클라우드에서 논리적으로 격리된 공간을 제공하여 고객이 정의하는 가상 네트워크에서 AWS 리소스를 시작할 수 있도록 하는 서비스이다.
AWS에서 EC2 인스턴스나 EB 인스턴스 혹은 RDS 데이터 베이스를 만들었다면
VPC는 해당 인스턴스를 `나의 아이디`에서만 접근이 가능하도록 `논리적으로 격리된 환경에서 생성해준다.`
뿐만 아니라 EC2 인스턴스나 RDS를 생성하면 자동적으로 기본 VPC(default VPC)가 할당된다.
그리고 할당이 될때는 `지역(region)별`로 다르게 할당이 된다.
ex)
AP-Norteast-2(서울)에서 VPC가 생성이 되었다.
AP-Norteast-1(도쿄)에서 VPC를 확인해보면 아무것도 없는 것을 확인할 수 있다.

1. 대시보드에서 VPC(격리형 클라우드 리소스) 검색
Elastic Beanstalk을 생성할 때 함께 만들어진 VPC가 보일 것

#### Security Group(보안그룹 / 방화벽)이란?
Security Group은 보안그룹 혹은 방화벽이라고도 한다.
Security Group을 거쳐서 Elastic Beanstalk 내부의 EC2 인스턴스나 EB 인스턴스와 요쳥을 주고 받는다. (Inbound, Outbound 처리)
- Inbound : 외부에서 EC2 인스턴스나 EB 인스턴스로 요청을 보내는 트래픽이다. ex) HTTP, HTTPS, SSH 등등...
- Outbound : EC2 인스턴스나 EB 인스턴스 등에서 외부로 나가는 트래픽이다.
   파일을 다운로드하거나 inbound로 들어온 트래픽을 처리하여 응답하는 경우도 포함된다.

=> Security Group이 Inbound와 Outbound를 통제하는 역할을 한다.
=> 결론적으로 Security Group이 트래픽을 열어줄수도 있고, 닫아줄 수도 있다.

동일한 VPC에서 오는 트래픽을 모두 허용하여 EB 인스턴스와 RDS(MySQL)를 연결해 줄 수 있다.

### MYSQL을 위한 AWS RDS 생성하기
1. docker-compose 부분에 DB를 위한 환경변수를 넣어준다.

docker-compose.yml
~~~
backend:
   build:
       dockerfile: Dockerfile.dev
       context: ./backend
   volumes:
       - /app/node_modules
       - ./backend:/app
   environment:
       MYSQL_HOST: mysql
       MYSQL_USER: root
       MYSQL_ROOT_PASSWORD: johnahn777
       MYSQL_DATABASE: myapp
       MYSQL_PORT: 3306
~~~

db.js
~~~
const mysql = require("mysql");
const pool = mysql.createPool({
   connectionLimit: 10,
   host: process.env.MYSQL_HOST,
   user: process.env.MYSQL_USER,
   password: process.env.MYSQL_ROOT_PASSWORD
   database: process.env.MYSQL_DATABASE
   port: process.env.MYSQL_PORT
})
~~~

2. RDS를 생성해준다.
- AWS > RDS > 데이터베이스 생성
- 엔진유형 : MySQL
- 템플릿 : 프리티어
- DB 인스턴스 식별자 : docker-fullstack-mysql
- 마스터 사용자 이름 : root (DB 환경변수에 지정한 MYSQL_USER)
- 마스터 암호 : johnahn777 (DB 환경변수에 지정한 MYSQL_ROOT_PASSWORD)
- 데이터베이스 옵션 > 초기 데이터베이스 옵션 : myapp (DB 환경변수에 지정한 MYSQL_DATABASE)

### Security Group 생성하기
AP-Norteast-2에 할당된 기본 VPC가 있고 내부에는 다음의 것들이 존재한다.
- EB 인스턴스
- RDS (MySQL)
Security Group에서 같은 VPC에서 오는 트래픽은 모두 허용하도록 설정하여, EB 인스턴스와 RDS가 서로 통신이 가능하도록 해준다.

EB 인스턴스와 RDS가 서로 요청을 보낼 수 있게 Security Group을 생성해보겠다.
1. AWS > VPC > 보안그룹 생성

2. 기본 세부 정보 작성
- 보안 그룹 이름 : DockerSecurityGroup
- 설명 : allow traffics between services in docker app
- vpc : 기본값 설정

3. 인바운드 규칙 추가
- 유형 : 사용자 지정 TCP
- 포트 범위 : 3306
- 소스 : 만든 Security Group 선택
- 설명 : open port for mysql inside the vpc

### Security Group 적용하기
RDS에 새로 생성된 Security Group(보안그룹) 적용하기
1. AWS > RDS > 데이터베이스
2. MySQL 인스턴스 클릭
3. 수정 > 보안 그룹 > 만들어 놓은 Security Group 선택

EB 인스턴스에 새로 생성된 Security Group(보안그룹) 적용하기
1. AWS > EB
2. EB 인스턴스 > 구성 클릭
3. 보안그룹 편집 > 인스턴스 보안 그룹에서 새로 생성된 보안 그룹 선택

=> VPC 내부의 EB 인스턴스와 RDS (MySQL)에 보안그룹을 적용해주었다.

### EB와 RDS 소통을 위한 환경 변수 설정하기
아직은 ElasticBeanstalk 안에 있는 컨테이너들이 MySQL 인스턴스와 소통할 때 환경 변수 부분을 인식하지 못한다.
그래서 AWS ElasticBeanstalk에 환경변수를 설정함으로서 그 부분의 문제를 해결해보겠다.

1. AWS > EB
2. EB 인스턴스 > 구성 클릭
3. 소프트웨어 > 편집 클릭
4. 환경 속성 편집
- MYSQL_HOST : RDS 인스턴스의 앤드포인트에 작성된 호스트를 직접 가져와 붙여넣어준다.
- MYSQL_USER : root
- MYSQL_ROOT_PASSWORD : johnahn777
- MYSQL_DATABASE : myapp
- MYSQL_PORT : 3306

### .travis.yml 파일 작성하기 (배포 부분)
travis CI에서 AWS로 배포하는 부분을 작성해보겠다.

.travis.yml
~~~
deploy:
   provider: elasticBeanstalk
   region: "ap-northeast-2"
   app: "docker-fullstack-app"
   env: DockerFullstackApp-env
   bucket_name: elasticbeanstalk-ap-northeast-2-306476627547
   bucket_path: "docker-fullstak-app"
   on:
       branch: main
~~~
- provider : 외부 서비스 표시 (s3, elasticbeanstalk, firebase 등등)
- region: 현재 사용하고 있는 AWS의 서비스가 위치하고 있는 물리적 장소
- app : 생성된 어플리케이션의 이름
- env: 환경 이름 (ElasticBeanstalk에 적혀있는 환경 이름)
- bucket_name : 해당 elasticbeanstalk을 위한 s3 버켓 이름 (s3에 넣어서 elasticBeanstalk을 사용하기 때문)
- bucket_path : 어플리케이션의 이름과 동일
- on
   - branch : 어떤 브랜치에 Push를 할때 AWS에 배포를 할 것인지

### Travis CI의 AWS 접근을 위한 API key 생성
아무런 인증 없이 Travis CI에서 마음대로 AWS와 소통할 수 없다.
Travis CI가 AWS에 접근 할 수 있게 인증 방식을 설정해주겠다.

< 소스 파일을 전달하기 위한 접근 요건 >
1. GITHUB -> Travis CI
: Travis CI 아이디 로그인 시 Github 연동으로 로그인 해준다.

2. Travis CI -> AWS
: AWS에서 제공해주는 Secret Key를 Travis yml 파일에 적어준다.
=> 인증을 위해서 API Key가 필요하다! 어떻게 받아야할까?

< Secret, Access API Key 받는 순서 >
1. IAM USER 생성

IAM이란? (Identity and Access Management)
AWS 리소스에 대한 액세스를 안전하게 제어할 수 있는 웹 서비스이다.
IAM을 사용하여 리소스를 사용하도록 인증(로그인) 및 권한 부여(권한 있음)된 대상을 제어한다.

- Root 사용자 : 현재 우리가 처음 가입하여 사용하고 있는 계정, AWS 서비스 및 리소스에 대한 완전한 액세스 권한이 있다.
- IAM 사용자 : root 사용자가 부여한 권한만 가지고 있음
=> 일상적인 관리 or 관리 작업이던 보안 측면에서 Root 사용자를 사용하는 것은 좋지 않다. IAM 유저를 생성해 사용하는 것을 추천!!

2. IAM > 사용자 추가
- 사용자 이름 : docker-fullstack-user
- 액세스 유형 : 프로그래밍 액세스
- 권한 설정 : AWSElasticBeanstalkFullAccess

3. IAM 사용자 액세스 키 ID와 비밀 액세스 키가 생성됨

4. API키를 Travis yml 파일에 적어주기
(직접 API 키를 Travis yml 파일에 적어주면 노출이 되기 때문에, 다른 곳에 적고 그것을 가져와줘야 한다.)

5. Travis CI에서 작업 중인 repo > more options > settings > Environment Variables
AWS에서 받은 API 키들을 NAME과 VALUE에 적어서 입력해준다.
- AWS_ACCESS_KEY
- AWS_SECRET_ACCESS_KEY
이곳에 넣어주면 외부에서 접근할 수 없어 더욱 안전하다.


6. travis yml 파일에서 환경변수로 입력해준 값을 받아오기 위한 설정을 입력해준다.
Travis CI 웹 사이트에서 보관 중인 Key와 Value를 로컬 환경에서 가지고 올 수 있게 travis yml 파일을 설정해준다.
.travis.yml
~~~
access_key_id: $AWS_ACCESS_KEY
secret_access_key: $AWS_SECRET_ACCESS_KEY
~~~