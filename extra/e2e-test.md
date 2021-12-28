# Angular E2E Framework 조사

## [ 조사 목적 ]
- 프론트엔드에 적용할 E2E 테스트 프레임워크 조사에 대한 건

## [ 조사 내용 요약 ]
1. 주요 테스트 도구에 대해 정리 (Jasmine, Karma, Jest, Selenium, Protractor, Cypress, Cucumber)
2. ng test와 ng e2e 적용방법과 차이점에 대해 정리

## [ 조사 내용 개요 ]
1. E2E 테스트 도구 정리
2. ng test  
1) 테스트 코드 작성  
2) 테스트 실행 및 결과  
3. ng e2e  
1) 테스트 코드 작성  
2) 테스트 실행 및 결과  

## [ 조사 내용 ]

## 1. E2E 테스트 도구 정리

E2E 테스트 주요 도구에 대해 살펴보겠습니다.

### 1) [Jasmine] (https://jasmine.github.io/)

**[ 현재 Spice의 dependency로 지정되어 있음 ]**

BDD 스타일의 단언 API를 사용하는 통합 **테스트 프레임워크**.
Node.js와 브라우저 환경 모두에서 사용 가능하다.
모든 기능을 통합해서 제공하기 때문에 라이브러리를 추가로 설치하고 설정할 필요 없이 쉽게 사용할 수 있다.

------

### 2) [Karma] (https://karma-runner.github.io/latest/index.html)

**[ 현재 Spice의 dependency로 지정되어 있음 ]**

Karma는 **자바 스크립트 테스트러너**이다.
작성한 테스트를 읽어들여 작성한 코드를 실행하고, 그 결과를 특정한 형식으로 출력해주는 역할을 한다.
Karma는 테스트 러너의 역할만 하기 때문에 **별도의 테스트 프레임워크가 추가로 필요하며, 보통 Jasmine을 사용하기를 권장한다.**
Jasmine으로 작성한 테스트 코드를 브라우저 환경에서 실행하기 위해서 별도의 페이지를 생성하고, 소스 코드 및 테스트 코드 등을 모두 로드하는 등의 작업이 추가로 필요한데, 이러한 일련의 작업을 대신 해주는 도구이다.

Karma가 동작되는 방식을 요약하면 다음과 같다.
> 1. karma 자체 서버를 띄운다.
> 2. 사용자가 작성한 테스트 코드와 소스 코드를 karma.config.js에 미리 정의한 테스트 환경(웹 브라우저)의 IFrame 내부로 불러들여 테스트를 실행한다.
> 3. 테스트를 모두 수행하고 난 뒤 수행 결과를 karma 서버로 받고, 콘솔을 통해 개발자에게 결과를 보여준다.

------

### 3) [Jest] (https://jestjs.io/)
페이스북에서 만든 오픈소스 **자바스크립트 테스트 프레임워크**이며, 최근 프론트엔드 개발에서 가장 활발하게 사용되고 있다.
Karma와 다르게 Node.js 환경에서 실행되며, 내부적으로 Jasmine 스타일의 단언 API를 사용하기 때문에 기존 Jasmine 유저들도 쉽게 적응할 수 있다.

------

### 4) [Selenium] (https://www.selenium.dev/)
웹 애플리케이션 **자동화 테스트를 지원하는 오픈 소스 프로젝트**이다.
셀레늄은 여러 테스트 도구의 패키지이므로 Suite라고 한다.
셀레늄 Suite 패키지에는 Selenium Server, WebDriver API 및 WebDriver 브라우저 드라이버가 포함된다.
여러 언어에서 웹 드라이버를 통해 웹 자동화 테스트 혹은 웹 자동화를 도와주는 라이브러리이다.

------

### 5) [Protractor](https://www.protractortest.org/#/)

**[ 현재 Spice의 dependency로 지정되어 있음 ]**

**Angular와 Angular JS 애플리케이션을 위한 E2E 테스트러너**이다.
Jasmine, Mocha와 같은 테스트 프레임워크를 지원하는 Node.js 프로그램이다.
Protractor는 Selenium과 함께 작동하여 브라우저 또는 모바일 장치에서 실행되는 Angular 프로그램을 시뮬레이션할 수 있는 자동화된 테스트 인프라를 제공한다.
Cross Browser Testing을 수행할 수 있다.
Angular JS 개념을 기반으로 하므로 AngularJS에 대해 이미 알고 있는 경우 Protractor를 쉽게 배울 수 있다.
실제 브라우저와 헤드리스 브라우저에서 실행된다.

Protractor가 동작되는 방식을 요약하면 다음과 같다.
> 1. 테스트 프레임워크(Jasmine, Mocha 등등)에서 테스트 스크립트를 작성한다.
> 2. Protractor가 테스트 러너로서 코드를 읽어들여 테스트를 실행한다.
> 3. Selenium을 사용하여 브라우저를 관리한다.
> 4. Selenium WebDriver를 사용하여 브라우저 API 호출한다.

## 2. ng test

* **Jasmine, Karma**
* browser에 표시되는 데이터의 결과까지 포함한다.
* component와 service를 모두 테스트 가능하다.
* native javascript 코딩방식으로 querySelector를 활용하는 것이 편하다.
* 단, service 단위까지 테스트 가능하므로 **Unit Test(단위 테스트)에 적합**하다.
* 즉, 함수 단위의 테스트로 활용하는 것이 좋다.

------

### 1) 테스트 코드 작성
테스트코드는 **spec 파일**에 작성한다.
.component.ts 및 .component.spec.ts 파일은 같은 폴더에 있는 형제 자매이다.

다음은 App Component를 테스트하는 코드이다. (app.component.spec.ts)

~~~ javascript
import { TestBed, async } from '@angular/core/testing';
import { AppComponent } from '../app/app.component';
describe('AppComponent', () => {
 beforeEach(async(() => {
   TestBed.configureTestingModule({
     declarations: [
       AppComponent
     ],
   }).compileComponents();
 }));
 it('app component를 생성합니다.', async(() => {
   const fixture = TestBed.createComponent(AppComponent);
   const app = fixture.debugElement.componentInstance;
   expect(app).toBeTruthy();
 }));
 it('타이틀은 app title 입니다.', async(() => {
   const fixture = TestBed.createComponent(AppComponent);
   fixture.detectChanges();
   const app = fixture.debugElement.componentInstance;
   expect(app.title).toEqual('app title');
 }));
 it('컨텐츠는 app content 입니다.', async(() => {
   const fixture = TestBed.createComponent(AppComponent);
   fixture.detectChanges();
   const app = fixture.debugElement.componentInstance;
   expect(app.content).toEqual('app content');
 }));
 it('h1 태그에 들어갈 제목은 Welcome to app title 입니다.', async(() => {
   const fixture = TestBed.createComponent(AppComponent);
   fixture.detectChanges();
   const compiled = fixture.debugElement.nativeElement;
   expect(compiled.querySelector('h1').textContent).toContain('Welcome to app title!');
 }));
 it('로그인 정보를 입력합니다', async(() => {
   const fixture = TestBed.createComponent(AppComponent);
   // fixture.detectChanges();
   const compiled = fixture.debugElement.nativeElement;
   compiled.querySelector('input#email').value = 'test@test.com';
   compiled.querySelector('input#password').value = 'password';
   compiled.querySelector('button.btn').click();
 }));
});
~~~

------

### 2) 테스트 실행 및 결과

ng test가 동작되는 방식을 요약하면 다음과 같다.
> 1. 콘솔에 Karma 테스트 결과가 출력된다.
> 2. Chrome 브라우저가 열리고, Jasmine HTML Reporter에 테스트 출력이 표시된다.
> 3. 브라우저에 테스트와 실행결과가 출력된다.
> 4. 테스트 실행기가 준비되면 Angular는 Jasmine 테스트 프레임워크를 통해 단위 테스트를 실행한다.

ng test CLI 명령을 실행한다.

~~~
ng test
~~~

콘솔 출력은 다음과 같다.

~~~
10% building modules 1/1 modules 0 active
...INFO [karma]: Karma v1.7.1 server started at http://0.0.0.0:9876/
...INFO [launcher]: Launching browser Chrome ...
...INFO [launcher]: Starting browser Chrome
...INFO [Chrome ...]: Connected on socket ...
Chrome ...: Executed 3 of 3 SUCCESS (0.135 secs / 0.205 secs)
~~~
로그의 마지막 줄을 보면 Karma가 세 가지 테스트를 모두 통과했음을 알 수 있다.

Chrome 브라우저가 열리고 Jasmine HTML Reporter에 테스트 출력이 표시된다.
테스트 행을 클릭하여 해당 테스트만 다시 실행할 수 있다.
ng test 명령은 변경 사항을 감시하고 있어, 테스트가 다시 실행되고 브라우저가 새로 고쳐지며 새 테스트 결과가 나온다.

