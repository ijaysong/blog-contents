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
