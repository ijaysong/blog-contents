## 6. Angular의 파일 구조와 처리 흐름

 

### 6.1. src

 

src 폴더는 Angular의 모든 구성요소, 공통 CSS, 이미지나 폰트와 같은 정적 파일, 설정 파일 등 애플리케이션 필수 파일을 담고 있다.

개발자가 생성하는 파일은 /src/app/ 폴더 하위에 생성된다.

src 폴더 밖의 파일들은 테스트, 빌드, 배포 등을 위한 각종 설정 파일이다.

 

### 6.2. Angular 애플리케이션의 처리 흐름

 

Angular 프로젝트 파일들은 Angular 고유의 처리 흐름을 갖는다.

 

#### 6.2.1. index.html

 

웹 브라우저가 가장 먼저 로딩하는 프로젝트 파일은 /my-app/dist/index.html이다.

이것은 ng build 명령어로 프로젝트를 빌드하였을 때 /my-app/src/index.html에 번들링된 자바스크립트 파일이 추가되어 자동으로 생성되는 파일이다.

 

Angular 애플리케이션을 기동하기 위해서는 수많은 의존성 모듈과 TypeScript 파일의 컴파일 결과물인 자바스크립트 파일을 로드할 필요가 있다.

Angular는 모듈 번들러 Webpack을 사용하여 의존성 모듈과 자바스크립트 파일을 번들링한 후, 수작업 없이 간편하게 로드할 수 있도록 자동화 기능을 제공한다.

 

번들링 결가물로 생성된 자바스크립트 파일들이 로드되어 실행되면서 Angular 애플리케이션은 동작하기 시작한다.

번들링된 자바스크립트 파일은 아래와 같다.

 

- main.js

- polifills.js

- styles.js

- vendor.js

- runtime.js

 

#### 6.2.2. main.ts

 

main.ts는 프로젝트의 메인 진입점이다.

루트 모듈(/src/app/app.module.ts)을 사용하여 애플리케이션을 기동한다.

 

```

// src/main.ts

...

platformBrowserDynamic().bootstrapModule(AppModule)

.catch(err => console.log(err));

```

 

main.ts는 angular.json의 main 프로퍼티의 설정에 의해 로드된다.

 

```

// angular.json

{

    ...

    "architect" : {

        "build" : {

            "builder" : "@angular-devkit/build-angular:browser",

            "options" : {

                "outputPath" : "dist/my-app",

                "index" : "src/index.html",

                "main" : "src/main.ts"

                ...

            }

        }

    }

}

```

 

#### 6.2.3. app.module.ts

 

@NgModule 데코레이터의 인자로 전달되는 메타데이터에 애플리케이션 전체의 설정정보를 기술한 루트 모듈이다.

루트 모듈은 루트 컴포넌트(/src/app/app.component.ts)를 기동한다.

 

#### 6.2.4. app.component.ts

 

모든 컴포넌트의 부모 역할을 담당하는 루트 컴포넌트이다.

 

### 6.3. Angular의 구성요소

 

Angular의 핵심 구성요소는 아래와 같다.

 

- 컴포넌트 (Component) : 컴포넌트는 템플릿과 메타데이터, 컴포넌트 클래스로 구성되며, 데이터 바인딩에 의해 연결된다. 컴포넌트는 화면을 구성하는 뷰를 생성하고 관리하는 것이 주된 역할이며 화면은 1개 이상의 컴포넌트를 조립하여 구성한다.

 

- 디렉티브 (Directive) : 애플리케이션 전역에서 사용할 수 있는 뷰에 관련한 공통 관심사를 컴포넌트에서 분리하여 구현한 것으로 컴포넌트의 복잡도를 낮추고 가독성을 높인다. 구조 디렉티브와 어트리뷰트 디렉티브로 구분할 수 있으며 큰 틀에서 컴포넌트 또한 디렉티브로 구분할 수 있다.

 

- 서비스 (Service) : 다양한 목적의 애플리케이션 공통 로직을 담당한다. 컴포넌트에서 애플리케이션 전역 관심사를 분리하기 위해 사용하며 의존성 주입이 가능한 클래스로 작성된다.

 

- 라우터 (Router) : 컴포넌트를 교체하는 방법으로 뷰를 전환하여 화면 간 이동을 구현한다.

 

- 모듈 (NgModule) : 기능적으로 관련된 구성요소를 하나의 단위로 묶는 매커니즘을 말한다. 모듈은 관련이 있는 기능들이 응집된 기능 블록으로 애플리케이션을 구성하는 하나의 단위를 만든다. 모듈은 다른 모듈과 결합할 수 있으며 Angular는 여러 모듈을 조합하여 애플리케이션을 구성한다. 컴포넌트, 디렉티브, 파이프, 서비스 등의 Angular의 구성요소는 모듈에 등록되어야 사용할 수 있다.

 

Angular는 컨포너느를 중심으로 Angular 구성요소를 조합하여 애플리케이션을 구축한다.

뷰를 담당하는 컴포넌트를 중심으로 화면을 구성하고, 디렉티브와 서비스를 사용하여 애플리케이션 전역 관심사를 분리하고 컴포넌트는 필요 시 디렉티브와 서비스를 사용한다.

라우터는 컴포넌트를 교체하는 방식으로 뷰를 전환하여 화면 간 이동을 구현하고, 모듈은 관련된 구성요소를 하나로 묶어 애플리케이션을 구성하는 하나의 단위를 만드는 역할을 한다.