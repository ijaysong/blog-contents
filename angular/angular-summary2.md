# 앵귤러(Angular)

## 2. Node.js와 npm
### 2.1. Node.js
Node.js는 Chrome V8 자바스크립트 엔진으로 빌드된 자바스크립트 런타임 환경으로 주로 서버 사이드 애플리케이션 개발에 사용되는 소프트웨어 플랫폼이다.  
브라우저 외부 환경에서 자바스크립트 애플리케이션 개발에 사용되며, 이에 필요한 모듈, 파일 시스템, HTTP 등 빌트인 API를 제공한다.

Node.js는 자바 스크립트를 사용해 개발한다.  
프런트앤드와 백엔드에서 자바스크립트를 사용할 수 있다는 동형성은 별도의 언어 학습 시간을 단축해 주는 장점이 있다.

논블로킹(non-blocking) I/O와 단일 스레드 이벤트 루프를 통한 높은 요청 처리 성능을 가지고 있다.  
데이터베이스로부터 대량의 데이터를 취득하여 웹 페이지에 표시할 때, 일반적으로 데이터베이스 처리에 대기시간이 발생하기 때문에 웹페이지 표시가 지연되는 현상이 발생한다.  
Node.js의 모든 API는 비동기 방식으로 동작하여 논블로킹 I/O가 가능하고 단일 스레드 이벤트 루프 모델을 사용하여 보다 가벼운 환경에서도 높은 요청처리 성능을 가지고 있다.

Node.js는 데이터를 실시간 처리하여 빈번한 I/O가 발생하는 SPA에 적합하다.  
하지만 CPU 사용률이 높은 애플리케이션에는 권장하지 않는다.

Node.js는 module 단위로 각 기능을 분할할 수 있다.  
module은 파일과 1대1 대응 관계를 가지며 하나의 모듈은 자신만의 독립적인 실행영역(scope)를 가지게 된다.  
따라서 클라이언트 사이드 자바스크립트와 달리 전역 변수의 중복문제가 발생하지 않는다.  
모듈은 module.exports 또는 exports 객체를 통해 정의하고 외부로 공개한다.  
그리고 공개된 모듈은 require 함수를 사용하여 임포트 한다.

### 2.2. npm
npm(Node Package Manager)은 자바스크립트 패키지 매니저이다.  
Node.js에서 사용할 수 있는 모듈을 패키지화하여 모아둔 저장소 역할과 패키지 설치 및 관리를 위한 CLI를 제공한다.

#### 2.2.1. 지역 설치와 전역 설치
npm install 명령어에는 지역(local)설치와 전역(global) 설치 옵션이 있다.  
옵션을 별도로 지정하지 않으면 지역으로 설치되며, 프로젝트 디렉터리 내에 node_modules 디렉터리가 자동 생성되고 그 안에 패키지가 설치된다.  
지역으로 설치된 패키지는 해당 프로젝트 내에서만 사용할 수 있다.

전역에 패키지를 설치하려면 npm install -g 옵션을 지정한다.  
전역으로 설치된 패키지는 전역에서 참조될 수 있다.  
모든 프로젝트가 공통으로 사용하는 패키지는 지역으로 설치하지 않고, 전역으로 설치한다.  
전역에 설치된 패키지는 OS에 따라 설치 장소가 다르다.  

* mac OS  : /usr/local/lib/node_modules
* 윈도우 OS : \Users\%USERNAME%\AppData\Roaming\npm\node_modules

#### 2.2.2. package.json과 의존성 관리
Node.js 프로젝트에서는 많은 패키지를 사용하게 되고 패키지의 버전도 빈번하게 업데이트되므로 프로젝트가 의존하고 있는 패키지를 일괄적으로 관리할 필요가 있다.  
`npm은 package.json 파일을 통해서 프로젝트 정보와 패키지의 의존성을 관리한다.`  
`이미 작성된 package.json 파일이 있다면 팀 내에 배포하여 동일한 개발환경을 빠르게 구축할 수 있는 장점이 있다.`  
package.json은 Java의 maven에서 pom.xml과 비슷한 역할을 한다.

package.json을 생성하려면 프로젝트 루트에서 npm init 명령어를 실행한다.  
npm init 명령어를 사용하면 프로젝트에 대한 여러 가지 정보를 입력하도록 요구받는다.  
이때 입력된 정보를 바탕으로 npm은 package.json 파일을 생성한다.  
npm init 명령어에 --yes 또는 -y 옵션을 추가한다. 그러면 기본 설정값으로 package.json 파일을 생성한다.  

package.json에서 가장 중요한 항목은 `name`과 `version`이다. 이것은 패키지의 고유성을 판단하므로 생략할 수 없다.  
그리고 dependencies 항목에는 해당 프로젝트가 참조하는 패키지들의 이름과 버전을 명시함으로서 의존성을 설정한다.