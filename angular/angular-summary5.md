## 5. Angular CLI

 

### 5.1. 프로젝트 생성

 

```

ng new <project-name>

```

 

### 5.2. 프로젝트 실행

 

```

cd <project-name>

ng serve

```

 

ng serve 명령어를 실행하면 Webpack을 사용하여 소스코드와 의존 모듈을 번들링 하고 Angular CLI가 내장하고 있는 개발용 서버를 실행한다.

브라우저를 열고 주소창에 `localhost:4200`을 입력하여 개발용 서버에 접속한다.

프로젝트를 실행할 때 `--open(축약형 -o)` 옵션을 추가하면 자동으로 브라우저를 실행해준다.

 

Angular CLI가 내장하고 있는 개발용 서버는 코드의 변경을 감지하여 자동으로 브라우저를 리로드하는 LiveReload 기능을 제공한다.

따라서, 코드 수정 후 파일을 저장하면 코드 변경을 자동 반영하여 번들링이 수행되고 브라우저가 리로드 되어 코드 변경 결과를 즉시 확인할 수 있다.

 

### 5.3. 프로젝트 구성요소 생성

 

| 생성 대상 구성요소 | 명령어                               | 축약형                |

| ------------------ | ------------------------------------ | --------------------- |

| 컴포넌트           | ng generate component component-name | ng g c component-name |

| 디렉티브           | ng generate directive directive-name | ng g d directive-name |

| 파이프             | ng generate pipe pipe-name           | ng g p pipe-name      |

| 서비스             | ng generate service service-name     | ng g s service-name   |

| 모듈               | ng generate module module-name       | ng g m module-name    |

| 가드               | ng generate guard guard-name         | ng g g guard-name     |

| 클래스             | ng generate class class-name         | ng g c class-name     |

| 인터페이스         | ng generate interface interface-name | ng g i interface-name |

| Enum               | ng generate enum enum-face           | ng g e enum-face      |

 

#### 5.3.1. 컴포넌트 생성

 

```

ng generate component <component-name>

```

 

component-name이 home인 컴포넌트를 생성하면 Angular CLI는 다음과 같이 동작한다.

 

- src/app 폴더에 home 폴더를 생성한다. (컴포넌트는 URL 경로의 단위가 될 수 있기 때문에 폴더로 구분한다.)

- src/app/home 폴더에 4개의 파일을 생성한다.

 

1. home.component.html : 컴포넌트 템플릿을 위한 HTML 파일

2. home.component.css : 컴포넌트 탬플릿의 스타일링을 위한 CSS 파일

3. home.component.ts : 컴포넌트 클래스 파일

4. home.component.spec.ts : 컴포넌트 유닛 테스트를 위한 스펙 파일

 

- 루트 모듈 src/app/app.module.ts에 새롭게 생성된 컴포넌트를 등록한다. (컴포넌트 클래스를 import하고 @NgModule 데코레이터의 declarations 프로퍼티에 컴포넌트 클래스를 등록한다.)

 

##### 5.3.1.1. 파일명의 암묵적 변경

 

`ng generate component` 다음에 지정한 컴포넌트 명이 실제 생성된 파일명과 다를 수 있다.

예를 들어, 컴포넌트 명을 newComponet로 지정해도, 실제 생성된 컴포넌트 파일명은 new-component.component.\*일것이다.

Angular CLI는 지정된 컴포넌트의 명이 대소문자를 구별하여 정해진 규칙에 따라 파일명을 암묵적으로 변경한다.

 

이와 같은 파일명의 암묵적 변경은 컴포넌트뿐만이 아니라 `ng generate` 명령어로 추가되는 구성요소에 모두 해당된다.

혼란을 방지하기 위해 ng genrate 명령어에 지정하는 구성요소의 명칭은 하이픈'-'으로 단어를 연결하는 `케밥 표기법`을 사용하는 것이 좋다.

 

##### 5.3.1.2. selector 프로퍼티 값의 접두사(Prefix)와 컴포넌트 클래스 이름

 

생성된 컴포넌트 클래스 파일을 살펴보면, (/src/app/home/home.component.ts)

컴포넌트명에 의해 자동 생성된 selector 프로퍼티 값은 ng generate component 명령어에서 지정한 컴포넌트명 home 앞에 접두사 app이 추가된 app-home이다.

Angular는 다른 애플리케이션의 selector 또는 HTML 요소와 충돌을 방지하기 위해 접두사를 추가하여 케밥 표기법으로 명명하는 것을 권장하고 있다.

 

#### 5.3.2. 디렉티브 생성

 

```

ng generate directive <directive-name>

```

 

directive-name이 highlight인 디렉티브를 생성하면 Angular CLI는 다음과 같이 동작한다.

 

- src/app 폴더에 2개의 파일을 생성한다.

 

1. highlight.directive.ts : 디렉티브 클래스 파일

2. highlight.directive.spec.ts : 디렉티브 유닛 테스트를 위한 스펙 파일

 

- 루트 모듈 src/app/app.module.ts에 새롭게 생성된 디렉티브를 등록한다. 디렉티브를 import하고 @NgModule 데코레이터의 declarations 프로퍼티에 디렉티브를 등록한다.

 

컴포넌트를 생성할 때와 달리, 디렉티브를 위한 폴더는 생성되지 않으며 기본적으로 src/app 폴더에 생성된다.

 

#### 5.3.3. 모듈 생성

 

```

ng generate module <module-name>

```

 

module-name이 todos 모듈을 생성하면 Angular CLI는 다음과 같이 동작한다.

 

- src/app 폴더에 todos 폴더를 생성한다.

- src/app/todos 폴더에 2개의 파일을 생성한다.

 

1. todos.module.ts : 모듈 클래스 파일

2. todos.module.spec.ts : 모듈 유닛 테스트를 위한 스펙 파일

 

#### 5.3.4. 서비스 생성

 

```

ng generate service <service-name>

```

 

service-name이 data 모듈을 생성하면 Angular CLI는 다음과 같이 동작한다.

 

- src/app/ 폴더에 2개의 파일을 생성한다.

 

1. data.service.ts : 서비스 클래스 파일

2. data.service.spec.ts : 서비스 유닛 테스트를 위한 스펙 파일

 

#### 5.3.5. 클래스 생성

 

```

ng generate class <class-name>

```

 

테스트를 위한 스펙 파일을 함께 생성하기 위해서는 `--spec` 옵션을 추가한다.

 

### 5.4. 프로젝트 빌드

 

```

ng build

```

#### 5.4.1. 트랜스파일링과 의존 모듈 번들링

 

TypeScript 기반으로 개발이 진행되는 Angular 애플리케이션은 TypeScript를 자바 스크립트로 변환하여야 한다.

또한 프로젝트가 의존하는 모듈들을 로드하는 HTML 파일의 script 태그를 작성해야 한다.

Angular CLI로 새로운 프로젝트를 생성하면 기본 패키지 매니저인 npm이 의존 모듈 설치를 자동으로 진행한다.

Angular CLI의 빌드 기능은 의존성 관리를 자동화하며, 내부적으로 모듈 번들러인 webpack을 사용해 아래와 같은 작업의 자동화를 지원한다.

 

- TypeScript에서 자바스크립트로의 트랜스파일링

- 디버깅 용도의 source map 파일 생성

- 의존 모듈과 HTML, CSS, 자바스크립트 번들링

- AoT 컴파일

- 코드의 문법체크

- 코드의 규약 준수 여부 체크

- 불필요한 코드의 삭제 및 압축

 

빌드 이전과 빌드 이후의 index.html을 비교해보자.

 

```

// src/index.html (빌드 이전)

...

<body>

    <app-root></app-root>

</body>

</html>

```

 

```

// dist/index.html (빌드 이후)

...

<body>

    <app-root></app-root>

 

    <script type="text/javascript" src="runtime.js"></script>

    <script type="text/javascript" src="polyfills.js"></script>

    <script type="text/javascript" src="styles.js"></script>

    <script type="text/javascript" src="vendor.js"></script>

    <script type="text/javascript" src="main.js"></script>

</body>

</html>

```

 

빌드가 완료되면 dist 폴더가 추가되고 그 내부에 빌드 결과물이 생성된다.

 

#### 5.4.2. 프로덕션 빌드와 배포

 

ng build 명령어를 실행하면 Angular CLI는 src/environments/environments.ts 파일을 참조하여 빌드를 수행한다.

이때 실행된 빌드는 개발환경 빌드로, 프로덕션 용도로 최적화 되어 있지 않다.

프로덕션 빌드를 수행하기 위해선 아래의 명령어를 실행한다.

 

```

ng build --prod

```

 

프로덕션 빌드 시에는 src/environments/environment.prod.ts 파일을 참조하여 빌드를 수행한다.

프로덕션 빌드의 결과물로 dist 폴더에 생성된 파일들을 서버에 업로드하면 배포가 완료된다.

 

호스팅 환경을 구축해주는 서비스인 now를 사용하여 프로덕션 빌드의 결과물을 서버에 업로드할 수 있다.

먼저 now를 전역에 설치한다.

 

```

npm install -g now

```

 

해당 프로젝트의 dist 폴더로 이동한 후, now 명령어를 실행한다.

 

```

now

```

 

#### 5.4.3. AoT 컴파일

 

Angular CLI의 빌드기능은 TypeScript를 자바스크립트로 트랜스파일링한다.

사실은 TypeScript 뿐만 아니라 컴포넌트 템플릿 또한 컴파일이 필요하다.

템플릿은 빌드 시에 컴파일 되지 않고 런타임에 JIT(Just In Time) 컴파일 된다.

단, 프로덕션 빌드 시에는 AoT 컴파일이 자동 적용된다.

 

```

ng build --aot

```

 

AoT(Ahead-of Time) 컴파일이란 프로젝트를 빌드할 때 템플릿을 미리 컴파일해 두는 것을 말한다.

빌드에 소요되는 시간이 조금 더 걸리더라도 런타임에 템플릿 컴파일이 실행되지 않기 때문에 실제 애플리케이션이 동작하는 시간은 단축되는 효과가 있다.

또한 템플릿을 JIT 컴파일하지 않고 미리 컴파일하기 때문에 템플릿에서 발생하는 에러를 사전에 감지할 수 있는 장점과 JIt 컴파일러를 포함할 피룡가 없어져 애플리케이션 전체 용량도 줄어드는 효과가 있다.


