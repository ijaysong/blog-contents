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