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