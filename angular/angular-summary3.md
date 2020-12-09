# 앵귤러(Angular)

## 3. ECMAScript 6

### 3.1. let, const와 블록 레벨 스코프

#### 3.1.1. var 키워드의 특징

- `함수레벨 스코프` : 전역 변수의 남발, for 루프의 초기화 식에서 사용한 변수를 for 루프 외부 또는 전역에서 참조 가능
- `var 키워드 생략 허용` : 의도하지 않은 변수의 전역화
- `중복 선언 허용` : 의도하지 않은 변숫값 변경
- `변수 호이스팅` : 변수를 선언하기 전에 참조 가능

대부분의 문제는 전역 변수로 인해 발생한다.
전역변수는 사용이 편리하다는 장점이 있지만 불가피한 상황을 제외하고는 사용을 억제해야 한다.
전역 변수는 유효 범위가 넓어서 어디에서 어떻게 사용될지 파악하기 힘들며, 비순수 함수에 의해 의도하지 않게 변경될 수도 있어서 코드의 복잡도를 증가시키는 원인이 된다.
따라서 변수의 유효 범우는 좁을수록 좋다.
ES6에서는 이러한 var의 단점을 보완하기 위해 let과 const 키워드를 도입하였다.

#### 3.1.2. let 키워드의 특징

##### 3.1.2.1. 블록 레벨 스코프

대부분의 C-family 언어는 블록 레벨 스코프를 지원하지만 자바 스크립트는 함수 레벨 스코프를 갖는다.

- `함수 레벨 스코프` : 함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다. 즉, 함수 내부에서 선언한 변수는 지역변수이며 함수 외부에서 선언한 변수는 모두 전역 변수 이다.
- `블록 레벨 스코프` : 코드 블록 내에서 선언된 변수는 코드 블록 내에서만 유효하며 코드 블록 외부에서는 참조할 수 없다.

```
console.log(foo); // undefined
var foo = 123;
console.log(foo); // 123
{
    var foo = 456;
}
console.log(foo); // 456
```

ES6에서는 블록 레벨 스코프를 갖는 변수를 선언하기 위해 let 키워드를 제공한다.

```
let foo = 123;
{
    let foo = 456;
    let bar = 456;
}
console.log(foo); // 123
console.log(bar); // ReferenceError : bar is not defined
```

let 키워드로 선언된 변수는 블록 레벨 스코프를 갖는다. 따라서 전역에서는 변수 bar를 참조할 수 없다.

##### 3.1.2.2. 중복 선언 금지

var 키워드로는 이름이 같은 변수를 중복해서 선언할 수 있었지만, `let 키워드`로는 이름이 같은 변수를 중복해서 선언하면 `문법 에러`가 발생한다.

```
var foo = 123;
var foo = 456; // 중복 선언 허용

let bar = 123;
let bar = 456; // Uncaught SyntaxError : Identifier 'bar' has already been declared
```

##### 3.1.2.3. 호이스팅

호이스팅(Hoisting)이란, var 선언문이나 function 선언문 등을 해당 스코프의 선두로 옮긴 것처럼 동작하는 특성을 말한다.  
하지만 var 키워드로 선언된 변수와는 달리 let 키워드로 선언된 변수를 선언문 이전에 참조하면 참조 에러가 발생한다.  
이는 let 키워드로 선언된 변수는 스코프의 시작에서 변수의 선언까지 `알시적 사각지대(TDZ, Temporal Dead Zone)`에 빠지기 때문이다.

```
console.log(foo); // undefined
var foo;

console.log(bar); // Error : Uncaught ReferenceError : bar is not defined
let bar;
```

변수는 3단계에 걸쳐 생성된다.

- 선언 단계 (Declaration phase) : 변수를 실행 컨텍스트의 변수 객체에 등록한다. 이 변수 객체는 스코프가 참조하는 대상이 된다.
- 초기화 단계 (Initialization phase) : 변수 객체에 등록된 변수를 위한 공간을 메모리에 확보한다. 이 단계에서 변수는 undefined로 초기화된다.
- 할당 단계 (Assignment phase) : undefined로 초기화된 변수에 실제 값을 할당한다.

var 키워드로 선언된 변수는 선언 단계와 초기화 단계가 한번에 이루어진다.  
즉, 스코프에 변수를 등록(선언 단계)하고 메모리에 변수를 위한 공간을 확보한 후, undefined로 초기화(초기화 단계)한다.  
따라서 변수 선언문 이전에 변수에 접근하여도 스코프에 변수가 존재하기 때문에 에러가 발생하지 않는다.  
다만 undefined를 반환한다.  
이후 변수 할당문에 도달하면 비로소 값이 할당된다. 이러한 현상을 `변수 호이스팅`이라고 한다.

`let 키워드로 선언된 변수는 선언 단계와 초기화 단계가 분리되어 진행된다.`  
즉, 스코프에 변수를 등록(선언 단계)하지만 초기화 단계는 변수 선언문에 도달했을 때 이루어진다.  
초기화 이전에 변수에 접근하려고 하면 참조 에러가 발생한다.  
이는 변수가 아직 초기화 되지 않았기 때문이다. 다시 말하면 변수를 위한 메모리 공간이 아직 확보되지 않았기 때문이다.  
따라서 스코프의 시작 지점부터 초기화 시작 지점까지는 변수를 참조할 수 없다.  
스코프의 시작 지점부터 초기화 시작 지점까지의 구간을 `일시적 사각지대`라고 부른다.

```
let foo = 1; // 전역 변수
{
    console.log(foo); // ReferenceError : foo is not defined
    let foo = 2; // 지역 변수
}
```

let으로 선언된 변수는 블록 레벨 스코프를 가지므로 코드 블록 내에서 선언된 변수 foo는 지역 변수 이다.  
따라서 지역 변수 foo도 해당 스코프에서 호이스팅 되고 코드 브록의 선두부터 초기화가 이루어지는 지점까지 일시적 사각지대에 빠진다.  
따라서 전역 변수 foo의 값이 출력되지 않고 참조 에러가 발생한다.

##### 3.1.2.4. 클로저

블록 레벨 스코프를 지원하는 let은 var보다 직관적이다.

```
var funcs = [];

// 함수의 배열을 생성하는 for 루프의 i는 전역 변수다.
for (var i = 0; i < 3; i++) {
    funcs.push(function() {
        console.log(i);
    });
}

// 배열에서 함수를 꺼내어 호출한다.
for (var j = 0; j < 3; j++) {
    funcs[j]();
}
```

위 실행 결과로 3이 세번 출력된다.  
그 이유로 for 루프의 var i가 전역 변수이기 때문이다.  
0, 1, 2를 출력하려면 아래와 같은 코드가 필요하다.

```
var funcs = [];

// 함수의 배열을 생성하는 for 루프의 i는 전역 변수다.
for (var i = 0; i < 3; i++) {
    (function(index) { // index는 자유 변수다.
        funcs.push(function() { console.log(index); });
    }(i));
}

// 배열에서 함수를 꺼내어 호출한다.
for (var j = 0; j < 3; j++) {
    funcs[j]();
}
```

자바스크립트 함수 레벨 스코프로 인하여 for 루프의 초기화 식에 사용된 변수가 전역 스코프를 갖게 되어 발생하는 문제를 회피하기 위해 클로저를 활용한 방법이다.

let 키워드를 for 루프의 초기화 식에 사용하면 클로저를 사용하기 않아도 위 코드와 동일한 동작을 한다.  
for 루프의 let i는 for 루프의 코드 블록에서만 유효한 지역 변수이다.  
또한 i는 자유변수로서 for 루프의 생명주기가 종료되어도 변수 i를 참조하는 함수가 존재하는 한 계속 유지된다.

```
var funcs = [];

// 함수의 배열을 생성하는 for 루프의 i는 for 루프의 코드 블록에서만 유효한 지역 변수이면서 자유 변수이다.
for (let i = 0; i < 3; i++) {
    funcs.push(function() {console.log(i); });
}

// 배열에서 함수를 꺼내어 호출한다.
for (var j = 0; j < 3; j++) {
    console.dir(funcs[j])
    funcs[j]();
}
```

##### 3.1.2.5. 전역 객체와 let

전역 객체는 모든 객체의 유일한 최상위 객체를 의미하며 일반적으로 브라우저 사이드에서는 window 객체, 서버 사이드(Node.js)에서는 global 객체를 의미한다.  
var 키워드로 선언된 변수를 전역 변수로 사용하면 전역 객체의 프로퍼티가 된다.

```
var foo = 123; // 전역변수
console.log(window.foo); // 123
```

let 키워드로 선언된 변수를 전역 변수로 사용하는 경우, let 전역 변수는 전역 객체의 프로퍼티가 아니다.  
즉, window.foo와 같이 접근할 수 없다.  
let 전역 변수는 보이지 않는 개념적인 블록 내에 존재하게 된다.

```
let foo = 123; // 전역 변수
console.log(window.foo); // undefined
```

#### 3.1.3. const 키워드의 특징

const는 상수(변하지 않는 값)을 위해 사용한다. 반드시 상수만을 위해 사용하지는 않는다.  
const의 특징은 대부분 let과 비슷하므로 다른 점만 살펴보겠다.

##### 3.1.3.1. 선언과 초기화

let은 재할당이 자유로우나 const는 재할당이 금지된다.

```
const FOO = 123;
FOO = 456; // TypeError : Assignment to constant variable.
```

const는 반드시 선언과 동시에 할당이 이루어져야 한다는 것이다.  
그렇지 않으면 아래처럼 문법 에러가 발생한다.

```
const FOO; // SyntaxError: Missing initializer in const declaration
```

또한 const는 let과 마찬가지로 블록 레벨 스코프를 갖는다.

```
{
    const FOO = 10;
    console.log(FOO); // 10
}
console.log(FOO); // ReferenceError : FOO is not defined
```

##### 3.1.3.2. 상수

상수는 가독성과 유지보수의 편의를 위해 적극적으로 사용해야 한다.  
네이밍이 적절한 상수로 선언하면 가독성과 유지보수성이 대폭 향상된다.

```
// 10의 의미를 알기 어렵기 때문에 가독성이 좋지 않다.
if (rows > 10) {

}

// 값의 의미를 명확히 기술하여 가독성이 좋아졌다.
const MAXROWS = 10;
if (rows > MAXROWS) {

}
```

##### 3.1.3.3. const와 객체

const는 객체에도 사용할 수 있다. 물론 이때도 재할당은 금지된다.

```
const obj = { foo: 123 };
obj = { bar: 456 }; // TypeError: Assignment to constant variable.
```

const 변수의 타입이 객체인 경우, 객체에 대한 참조를 변경하지 못한다는 것을 의미한다.  
이때 `객체의 프로퍼티는 보호되지 않는다.`  
다시 말하자면, 재할당은 불가능하지만 할당된 객체의 내용(프로퍼티의 추가, 삭제, 프로퍼티 값의 변경)은 변경할 수 있다.

```
const user = { name: 'Lee' };

// const 변수는 재할당이 금지된다.
// user = {}; // TypeError: Assignment to constant variable.

// 객체의 내용은 변경할 수 있다.
user.name = 'Kim';
console.log(user); // { name: 'Kim' }
```

객체의 내용이 변경되더라도 객체 타입 변수에 할당된 주소값은 변경되지 않는다.  
따라서 객체 타입 변수 선언에는 const를 사용하는 것이 좋다.  
만약에 명시적으로 객체 타입 변수의 주소값을 변경(재할당)하여야 한다면 let을 사용한다.

### 3.2. 템플릿 리터럴

템플릿 리터럴은 일반 문자열과 비슷해 보이지만, ' 또는 " 같은 통상적인 따옴표 문자 대신 백틱 문자`를 사용한다. 일반적인 문자열에서 줄바꿈은 허용되지 않으며, 공백을 표현하려면 백슬래시(\)로 시작하는 이스케이프 시퀀스를 사용해야 한다. ES6 템플릿 리터럴은 일반적인 문자열과 달리`여러 줄에 걸쳐 문자열을 작성할 수 있으며, 템플릿 리터럴 내의 모든 화이트스페이스는 있는 그대로 적용된다.`

```
const template = `템플릿 리터럴은
'작은 따옴표'와
"큰따옴표"를 혼용할 수 있다.`;
console.log(template);
```

템플릿 리터럴은 + 연산자를 사용하지 않아도 간단한 방법으로 새로운 문자열을 삽입할 수 있는 기능을 제공한다. 이를 `문자열 삽입`이라고 한다.

```
const first = 'Ung-mo';
const last = 'Lee';

// 문자열 연결
console.log('My name is ' + first + ' ' + last + '.');

// 문자열 대압
console.log(`My name is ${first} ${last}.`);
```

`${expression}을 템플릿 대입문`이라 한다.
템플릿 대입문에는 `문자열뿐만 아니라 자바스크립트 표현식을 사용할 수 있다.`

```
// 템플릿 대입문에는 문자열 뿐만 아니라 표현식도 사용할 수 있다.
console.log(`1 + 1 = ${1 + 1}`); // 1 + 1 = 2

const name = 'ungmo';
console.log(`Hello ${name.toUpperCase()}`); // Hello Ungmo
```
### 3.3. 화살표 함수

#### 3.3.1. 화살표 함수의 선언

화살표 함수는 function 키워드 대신 화살표(=>)를 사용하여 간략한 방법으로 변수를 선언할 수 있다.

`매개변수 지정`

```
() => { ... }    // 매개변수가 없을 경우
x => { ... }     // 매개변수가 한 개인 경우, 소괄호 생략 가능
(x, y) => {...}  // 매개변수가 여러 개인 경우, 소괄호 생략 불가능
```

`함수 몸체 지정`

```
x => { return x * x }        // 한줄 블록
x => x * x                   // 함수 몸체가 한 줄의 구문이라면 중괄호를 생략할 수 있으며 암묵적으로 반환된다. 위 표현과 동일하다.

() => { return { a: 1 }; }
() => ({ a: 1})              // 위 표현과 동일하다. 객체 반환 시 소괄호를 사용한다.

() => {                      // 여러 줄 블록
    const x = 10;
    return x * x;
};
```

#### 3.3.2. 화살표 함수의 호출

화살표 함수는 `익명 함수`로만 사용할 수 있다.
따라서 화살표 함수를 호출하려면 함수 표현식을 사용한다.

```
// ES5
var pow = function(x) { return x * x; };
console.log(pow(10)); // 100

// ES6
const pow = x => x * x;
console.log(pow(10)); // 100
```

또는 `콜백함수`로 사용할 수 있다.

```
// ES5
var arr = [1, 2, 3];
var pow = arr.map(function (x) {
    return x * x;
});
console.log(pow); // [1, 4, 9]

// ES6
const arr = [1, 2, 3];
const pow = arr.map(x => x * x);
console.log(pow); // [1, 4, 9]
```

#### 3.3.2.4. this

function 키워드로 생성한 일반 함수와 화살표 함수의 가장 큰 차이점은 this이다.
일반 함수의 경우, 해당 함수를 호출하는 패턴에 따라 this에 바인딩되는 객체가 달라진다.
콜백 함수 내부의 this는 전역 객체 window를 가리킨다.

```
function Prefixer(prefix) {
    this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function(arr) {
    return arr.map(function (x) {
        return this.prefix + ' ' + x; // this : 전역객체 window
    });
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim'])); // ["undefined Lee", "undefined Kim"]
```

콜백 함수 내부의 this가 메소드를 호출한 객체(생성자 함수의 인스턴스)를 가리키게 하려면 아래의 3가지 방법이 있다.

`방법 1: that = this`

```
function Prefixer(prefix) {
    this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function(arr) {
    var that = this; // this : Prefixer 생성자 함수의 인스턴스
    return arr.map(function (x) {
        return that.prefix + ' ' + x;
    });
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim'])); // ["Hi Lee", "Hi Kim"]
```

`방법 2: map(func, this)`

```
function Prefixer(prefix) {
    this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function(arr) {
    return arr.map(function (x) {
        return this.prefix + ' ' + x;
    }, this); // this: Prefixer 생성자 함수의 인스턴스
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim'])); // ["Hi Lee", "Hi Kim"]
```

`방법 3: bind(this)`

```
// Function.prototype.bind()로 this를 바인딩한다.
function Prefixer(prefix) {
    this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function(arr) {
    return arr.map(function (x) {
        return this.prefix + ' ' + x;
    }.bind(this)); // this: Prefixer 생성자 함수의 인스턴스
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim'])); // ["Hi Lee", "Hi Kim"]
```

#### 3.3.2.4. 화살표 함수의 this

화살표 함수는 언제나 자신을 포함하는 외부 스코프에서 this를 계승 받는다.
다시 말해 화살표 함수는 자신만의 this를 생성하지 않고 자신을 포함하고 있는 상위 컨텍스트로부터 this를 계승받는다.
이를 `Lexiccal this`라 한다.

```
function Prefixer(prefix) {
    this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function(arr) {
    return arr.map(x => `${this.prefix} ${x}`);
};

const pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim'])); // ["Hi Lee", "Hi Kim"]
```

#### 3.3.2.5. 화살표 함수를 사용하면 안되는 경우

화살표 함수는 Lexical this를 지원하므로 콜백 함수로 사용하기 편리하다.
하지만 화살표 함수를 사용하는 것이 오히려 혼란을 불러오는 경우도 있으므로 주의하여야 한다.

##### 3.3.2.5.1. 메소드

화살표 함수로 메소드를 정의하는 것은 피해야 한다.

```
const person = {
  name: 'Lee',
  sayHi : () => console.log(`Hi ${this.name}`)
};

person.sayHi(); // Hi undefined
```

메소드로 정의한 `화살표 함수 내부의 this는 메소드를 소유한 객체, 즉 메소드를 호출한 객체를 가리키지 않고 상위 컨텍스트인 전역 객체 window를 가리킨다.`
따라서 화살표 함수로 메소드를 정의하는 것은 바람직하지 않다.

```
const person = {
    name: 'Lee',
    sayHi() { // sayHi : function() {
        console.log(`Hi ${this.name}`);
    }
};

person.sayHi(); // Hi Lee
```

##### 3.3.2.5.2. prototype

화살표 함수로 정의된 메소드를 prototype에 할당하는 경우도 같은 문제가 발생한다.

```
const person = {
    name: 'Lee'
};

Object.prototype.sayHi = () => console.log(`Hi ${this.name}`);

person.sayHi(); // Hi undefined
```

따라서 prototype에 메소드를 할당하는 경우, 일반 함수를 할당한다.

```
const person = {
    name: 'Lee'
};

Object.prototype.sayHi = function() {
    console.log(`Hi ${this.name}`)l
};

person.sayHi(); // Hi Lee
```

##### 3.3.2.5.3. 생성자 함수

화살표 함수는 생성자 함수로 사용할 수 없다.
생성자 함수는 prototype 프로퍼티를 가지며 prototype 프로퍼티가 가리키는 프로토타입 객체의 constructor를 사용한다.
하지만 화살표 함수는 prototype 프로퍼티를 가지고 있지 않다.

```
const Foo = () => {};

// 화살표 함수는 prototype 프로퍼티가 없다
console.log(Foo.hasOwnProrperty('prototype')); // false

const foo = new Foo(); // TypeError : Foo is not a constructor
```

##### 3.3.2.5.4. addEventListener 함수의 콜백 함수

addEventListener 함수의 콜백 함수를 화살표 함수로 정의하면 this가 상위 컨텍스트인 전역 객체 window를 가리킨다.

```
var button = document.getElementById('myButton');

button.addEventListener('click', () => {
    console.log(this == window); // true
    this.innerHTML = 'Clicked button';
});
```

따라서 addEventListener 함수의 콜백 함수에서 this를 사용하는 경우, function 키워드로 정의하나 일반 함수를 사용하여야 한다.
일반 함수로 정의된 addEventListener 함수의 콜백 함수 내부의 this는 이벤트 리스너에 바인딩된 요소를 가리킨다.

```
var button = document.getElementById('myButton');

button.addEventListener('click', () => {
    console.log(this == button); // true
    this.innerHTML = 'Clicked button';
});
```

### 3.4. 파라미터 기본값

ES5에서는 파라미터에 기본값을 설정할 수 없다.
따라서 적절한 인수가 전달되었는지 함수 내부에서 확인할 필요가 있다.

```
// ES5
function plus(x, y) {
    x = y || 0;  // 파라미터 x에 인수를 할당하지 않은 경우, 기본값 0을 할당한다.
    y = y || 0;  // 파라미터 y에 인수를 할당하지 않은 경우, 기본값 0을 할당한다.
    return x + y;
}
console.log(plus()); // 0
console.log(plus(1, 2)); // 3
```

ES6에서는 파라미터에 기본값을 설정하여 함수 내에서 수행하던 파라미터 검사와 초기화를 간소화할 수 있다.

```
// ES6
function plus(x = 0, y = 0) {
    // 파라미터 x, y에 인수를 할당하지 않은 경우, 기본값 0을 할당한다
    return x + y;
}

console.log(plus());
console.log(plus(1, 2));
```
### 3.5. Rest 파라미터

 

#### 3.5.1. 기본 문법

 

Rest 파라미터는 Spread 연산자(...)를 사용하여 파라미터를 정의한 것을 의미한다.

Rest 파라미터를 사용하면 인수 리스트를 함수 내부에서 배열로 전달받을 수 있다.

 

```

function foo(...rest) {

    console.log(Array.isArray(rest)); // true

    console.log(rest); // [1, 2, 3, 4, 5]

}

 

foo(1, 2, 3, 4, 5);

```

 

인수는 순차적으로 파라미터와 Rest 파라미터에 할당된다.

 

```

function foo(param, ...rest) {

    console.log(param); // 1

    console.log(rest); // [2, 3, 4, 5]

}

 

foo(1, 2, 3, 4, 5);

 

function bar(param1, param2, ...rest) {

    console.log(param1); // 1

    console.log(param2); // 2

    console.log(rest); // [3, 4, 5]

}

 

bar(1, 2, 3, 4, 5);

```

 

Rest 파라미터는 반드시 마지막 파라미터여야 한다.

 

```

function foo(...rest, param1, param2) { }

 

foo(1, 2, 3, 4, 5); // SyntaxError: Rest parameter must be last formal parameter

```

 

#### 3.5.2. arguments와 rest 파라미터

 

ES5에서는 인자의 개수를 사전에 알 수 없는 `가변 인자 함수의 경우, arguments 객체를 통해 인수를 확인한다.`

arguments 객체는 함수 호출 시 전달된 인수들의 정보를 담고 있는 순회 가능한 유사 배열 객체이며 함수 내부에서 `지역 변수`처럼 사용할 수 있다.

 

```

// ES5

var foo = function() {

    console.log(arguments);

};

foo(1, 2); // {'0': 1, '1': 2}

```

 

`화살표 함수에는 함수 객체의 arguments 프로퍼티가 없다.`

따라서 화살표 함수로 가변 인자 함수를 구현해야 할 때는 반드시 rest 파라미터를 사용해야 한다.

 

```

var normalFunc = function() {};

console.log(normalFunc.hasOwnProperty('arguments')); // true

 

const arrowFunc = () => {};

console.log(arrowFunc.hasOwnProperty('arguments')); // false

```

 

### 3.6. Spread 연산자

 

#### 3.6.1. 함수의 인자로 사용하는 경우

 

배열을 함수의 인자로 사용하고, 배열의 각 요소를 개별적인 파라미터로 전달하고 싶은 경우, Function.prototype.apply를 사용하는 것이 일반적이다.

 

```

// ES5

function foo(x, y, z) {

    console.log(x); // 1

    console.log(y); // 2

    console.log(z); // 3

}

 

// 배열을 foo 함수의 인자로 전달하려고 한다.

const arr = [1, 2, 3];

 

// apply 함수의 2번째 인자(배열)는 호출하려는 함수(foo)의 개별 인자로 전달된다.

foo.apply(null, arr);

```

 

ES6의 Spread 연산자(...)를 사용한 배열을 함수의 인수로 사용하면 배열의 요소를 개별적으로 분리하여 순차적으로 파라미터에 할당한다.

 

```

// ES6

function foo(x, y, z) {

    console.log(x);

    console.log(y);

    console.log(z);

}

 

// 배열을 foo 함수의 인자로 전달하려고 한다.

const arr = [1, 2, 3];

 

// apply 함수의 2번째 인자(배열)는 호출하려는 함수(foo)의 개별 인자로 전달된다.

foo(...arr);

```

 

#### 3.6.2. 배열에서 사용하는 경우

 

##### 3.6.2.1. concat

 

ES5에서 기존 배열의 요소를 새로운 배열 요소의 일부로 만들고 싶은 경우, 배열 리터럴만으로 해결할 수 없고 concat 메소드를 사용해야 한다.

 

```

// ES5

var arr = [1, 2, 3];

console.log(arr.concat([4, 5, 6])); // [1, 2, 3, 4, 5, 6]

```

 

Spread 연산자를 사용하면 배열 리터럴만으로 기존 배열의 요소를 새로운 배열 요서의 일부로 만들 수 있다.

 

```

// ES6

const arr = [1, 2, 3];

// ...arr은 [1, 2, 3]을 개별 요소로 분리한다

console.log([...arr, 4, 5, 6]); // [1, 2, 3, 4, 5, 6]

```

 

##### 3.6.2.2. push

 

ES5에서 기존 배열에 다른 배열의 개별 요소를 각각 push하려면 아래와 같은 방법을 사용한다.

 

```

// ES5

var arr1 = [1, 2, 3];

var arr2 = [4, 5, 6];

 

// apply 메소드의 2번째 인자는 배열이다. 이건은 개별인자로 push 메소드에 전달된다.

Array.prototype.push.apply(arr1, arr2);

console.log(arr1); // [1, 2, 3, 4, 5, 6]

```

 

spread 연산자를 사용하면 아래와 같이 보다 간편하게 표현할 수 있다.

 

```

// ES6

const arr1 = [1, 2, 3];

const arr2 = [4, 5, 6];

 

// ...arr2sms [4, 5, 6]을 개별요소로 분리한다.

arr1.push(...arr2);

console.log(arr1); // [1, 2, 3, 4, 5, 6]

```

 

##### 3.6.2.3. splice

 

Spread 연산자를 사용하면 아래와 같이 보다 간편하게 표현할 수 있다.

 

```

const arr1 = [1, 2, 3, 6];

const arr2 = [4, 5];

 

// ...arr2는 [4, 5]를 개별 요소로 분리한다.

arr1.splice(3, 0, ...arr2); // arr1.splice(3, 0, 4, 5); 와 같다.

 

console.log(arr1); // [1, 2, 3, 4, 5, 6]

```

 

##### 3.6.2.4. copy

 

ES5에서 기존 배열을 복사하려면 splice 메소드를 사용한다

 

```

// ES5

var arr = [1, 2, 3];

 

var copy = arr.slice();

console.log(copy); // [1, 2, 3]

 

// copy를 변경한다

copy.push(4);

console.log(copy); // [1, 2, 3, 4]

 

// arr은 변경되지 않는다.

console.log(arr); // [1, 2, 3]

```

 

Spread 연산자를 사용하면 아래와 같이 보다 간편하게 표현할 수 있다.

 

```

const arr = [1, 2, 3];

 

const copy = [...arr];

console.log(copy); // [1, 2, 3]

 

// copy를 변경한다.

copy.push(4);

console.log(copy); // [1, 2, 3, 4]

 

// arr은 변경되지 않는다.

console.log(arr); // [1, 2, 3]

```

 

#### 3.6.3. 객체에서 사용하는 경우

 

Spread 연산자를 사용하면 객체를 손쉽게 병합 또는 변경할 수 있다.

 

```

// 객체의 병합

const merged = {...{ x: 1, y: 2 }, ...{ y: 10, z: 3 }};

console.log(merged); // { x: 1, y: 10, z: 3 }

 

// 특정 프로퍼티 변경

const changed = { ...{ x: 1, y: 2 }, y: 100 };

console.log(changed); // { x: 1, y: 100 }

 

// 프로퍼티 추가

const added = { ...{ x: 1, y: 2}, z: 0 };

console.log(added); // { x: 1, y: 2, z: 0 }

```

 

Object.assign 메소드를 사용해도 동일한 작업을 할 수 있다.

 

```

// 객체의 병합

const merged = Object.assign({}, { x: 1, y: 2 }, { y: 10, z: 3 });

console.log(merged); // { x: 1, y: 10, z: 3 }

 

// 특정 프로퍼티 변경

const changed = Object.assign({}, { x: 1, y: 2 }, {y: 100});

console.log(changed); // { x: 1, y: 100 }

 

// 프로퍼티 추가

const added = Object.assign({}, { x: 1, y: 2 }, {z: 0 });

console.log(added); // { x: 1, y: 2, z: 0 }

```

### 3.7. 객체 리터럴 프로퍼티 기능 확장

 

#### 3.7.1. 프로퍼티 축약 표현

 

ES5에서 객체 리터럴의 프로퍼티는 프로퍼티 이름과 프로퍼티 값으로 구성된다.

프로퍼티의 값은 변수에 할당된 값일 수도 있다.

 

```

// ES5

var x = 1, y = 2;

var obj = {

    x : x,

    y : y

};

console.log(obj); // { x: 1, y: 2 }

```

 

ES6에서 프로퍼치 값으로 변수를 사용하는 경우, 프로퍼티 이름을 생략할 수 있다.

이때 프로퍼티 이름은 변수의 이름으로 자동 생성된다.

 

```

// ES6

let x = 1, y = 2;

const obj = {x, y};

console.log(obj); // {x: 1, y: 2}

```

 

#### 3.7.2. 프로퍼티 이름 조합

 

ES5에서 객체 리터럴의 프로퍼티 이름을 문자열이나 변수를 조합하여 동적으로 생성하고 싶을 때, 객체 리터럴 외부에서 프로퍼티 이름을 생성하고 객체에 할당해야 한다.

 

```

// ES5

var i = 0;

var propNamePrefix = 'prop_';

var obj = {};

 

obj[propNamePrefix + ++i] = i;

obj[propNamePrefix + ++i] = i;

obj[propNamePrefix + ++i] = i;

console.log(obj); // { prop_1: 1, prop_2: 2, prop_3: 3 }

```

 

ES6에서는 객체 리터럴 내부에서 프로퍼티 이름을 동적으로 생성할 수 있다.

 

```

// ES6

let i = 0;

const propNamePrefix = 'prop_';

 

const obj = {

    obj[propNamePrefix + ++i] : i,

    obj[propNamePrefix + ++i] : i,

    obj[propNamePrefix + ++i] : i

};

console.log(obj); // { prop_1: 1, prop_2: 2, prop_3: 3 }

```

 

#### 3.7.3. 메소드 축약 표현

 

ES5에서 메소드를 선언하려면 프로퍼티의 값으로 함수 선언식을 사용한다.

 

```

// ES5

var obj = {

    name: 'Lee',

    sayHi: function() {

        console.log(`Hi! ` + this.name);

    }

};

 

obj.sayHi(); // Hi! Lee

```

 

ES6에서는 메소드를 선언할 때 function 키워드를 생략한 축약 표현을 사용할 수 있다.

 

```

// ES6

const obj = {

    name: 'Lee',

    // 메소드 축약 표현

    sayHi() {

        console.log(`Hi! ` + this.name);

    }

};

 

obj.sayHi(); // Hi! Lee

```

 

#### 3.7.4. **proto**프로퍼티에 의한 상속

 

ES5에서 객체 리터럴을 상속하려면 Object.create() 함수를 사용한다.

이를 `프로토타입 패턴 상속` 이라고 한다.

 

```

// ES5

var parent = {

    name: 'parent',

    sayHi : function() {

        console.log(`Hi! ` + this.name);

    }

};

 

// 프로토타입 패턴 상속

var child = Object.create(parent);

child.name = 'child';

parent.sayHi(); // Hi! parent

child.sayHi(); // Hi! child

```

 

ES6에서는 객체 리터럴 내부에서 **proto** 프로퍼티를 직접 설정할 수 있다.

이것은 객체 리터럴에 의해 생성된 객체의 **proto** 프로퍼티에 다른 객체를 직접 바인딩하여 상속을 표현할 수 있음을 의미한다.

 

```

// ES6

const parent = {

    name: 'parent',

    sayHi() {

        console.log('Hi! ' + this.name);

    }

};

 

const child = {

    // child 객체 프로토타입 객체에 parent 객체를 바인딩하여 상속을 구현한다.

    __proto__: parent,

    name: 'child'

};

 

parent.sayHi(); // Hi! parent

child.sayHi(); // Hi! child

```

### 3.8. 디스트럭처링

 

디스트럭처링은 구조화된 배열 또는 객체를 destructuring(비구조화, 파괴)하여 개별적인 변수에 할당하는 것이다.

배열 또는 객체 리터럴에서 필요한 값만을 추출하여 변수에 할당하거나 반환할 때 유용하다.

 

#### 3.8.1. 배열 디스트럭처링

 

ES5에서 배열의 각 요소를 배열로부터 디스트럭처링하여 변수에 할당하기 위한 방법은 아래와 같다.

 

```

// ES5

var arr = [1, 2, 3];

 

var one = arr[0];

var two = arr[1];

var three = arr[2];

 

console.log(one, two, three); // 1 2 3

```

 

ES6의 배열 디스트럭처링은 배열의 각 요소를 배열로부터 추출하여 벼수 리스트에 할당한다.

이때 추출/할당 기준은 배열의 인덱스이다.

 

```

// ES6

const arr = [1, 2, 3];

 

// 배열의 인덱스를 기준으로 배열로부터 요소를 추출하여 변수에 할당

const[one, two, three] = arr;

 

console.log(one, two, three); // 1 2 3

```

 

배열 디스트럭처링을 위해서는 할당 연산자 왼쪽에 배열 형태의 변수 리스트가 필요하다.

 

```

let x, y, z;

[x, y, z] = [1, 2, 3];

// 위의 구문과 같다.

let [x, y, z] = [1, 2, 3];

```

 

왼쪽 변수 리스트와 오른쪽의 배열은 배열의 인덱스를 기준으로 할당된다.

 

```

let x, y, z

 

[x, y] = [1, 2];

console.log(x, y); // 1 2

 

[x, y] = [1];

console.log(x, y); // 1 undefined

 

[x, y] = [1, 2, 3];

console.log(x, y); // 1 2

 

[x, , z] = [1, 2, 3];

console.log(x, z); // 1 3

 

// 기본값

[x, y, z = 3] = [1, 2];

console.log(x, y, z); // 1 2 3

 

[x, y = 10, z = 3] = [1, 2];

console.log(x, y, z); // 1 2 3

 

// Spread 연산자

[x, ...y] = [1, 2, 3];

console.log(x, y); // 1 [ 2, 3 ]

```

 

ES6의 배열 디스트럭처링은 배열에서 필요한 요소만 추출하여 변수에 할당하고 싶은 경우에 유용한다.

아래 코드는 Date 객체에서 연도, 월, 일을 추출하는 예제이다.

 

```

const today = new Date();

const formattedDate = today.toISOString().substring(0, 10);

const [year, month, day] = formattedDate.split('-');

console.log([year, month, day]); // ['2018', '05', '05']

```

 

#### 3.8.2. 객체 디스트럭처링

 

ES5에서 객체의 각 프로퍼티를 객체로부터 디스트럭처링하여 변수에 할당하려면 프로퍼티 이름(키)를 사용해야 한다.

 

```

// ES5

var obj = { firstName: 'Ungmo', lastName: 'Lee' };

var firstName = obj.firstName;

var lastName = obj.lastName;

console.log(firstName, lastName); // Ungmo Lee

```

 

ES6의 객체 디스트럭처링은 객체의 각 프로퍼티를 객체로부터 추출하여 변수 리스트에 할당한다.

이때 할당 기중은 프로퍼티 이름(키)이다.

 

```

// ES6

var obj = { firstName: 'Ungmo', lastName: 'Lee' };

const { firstName, lastName } = obj;

console.log(firstName, lastName); // Ungmo Lee

```

 

객체 디스트럭처링을 위해서는 할당 연산자 왼쪽에 객체 형태의 변수 리스트가 필요하다.

 

```

const { prop1: p1, prop2: p2 } = { prop1: 'a', prop2: 'b' };

console.log(p1, p2);

console.log({ prop1: p1, prop2: p2 }); // {prop1: 'a', prop2: 'b'}

 

// 아래는 위의 축약형이다.

const { prop1, prop2 } = { prop1: 'a', prop2: 'b' };

console.log({ prop1, prop2 }); // {prop1: 'a', prop2: 'b' }

 

// 기본값

const { prop1, prop2, prop3 = 'c' } = { prop1: 'a', prop2: 'b' };

console.log({ prop1, prop2, prop3 }); // { prop1: 'a', prop2: 'b', prop3: 'c' }

```

 

객체 디스트럭처링은 객체에서 프로퍼티 이름(키)으로 필요한 프로퍼티 값만을 추출할 수 있다.

 

```

const todos = [

    {id: 1, content: 'HTML', completed: true },

    {id: 2, content: 'CSS', completed: false },

    {id: 3, content: 'JS', completed: false },

];

 

// todo 배열의 요소인 객체로부터 completed 프로퍼티만을 추출한다.

const completedTodos = todos.filter(({ completed }) => completed);

console.log(completedTodos); // [ { id: 1, content: 'HTML', completed: true } ]

```

 

Array.prototype.filter 메소드의 콜백 함수는 대상 배열(todos)을 순회하며 첫 번째 인자로 대상 배열의 요소를 받는다.

이때 필요한 프로퍼티(completed 프로퍼티)만을 추출할 수 있다.

중첩 객체의 경우는 아래와 같이 사용한다.

 

```

const person = {

    name: 'Lee',

    address : {

        zipCode: '03068',

        city : 'Seoul'

    }

};

 

const { address: { city } } = person;

console.log(city); // 'Seoul'

```

### 3.9. 클래스

 

자바스크립트는 `프로토타입 기반` 객체지향 언어다.

프로토타입 기반 프로그래밍은 클래스가 필요없는 객체지향 프로그래밍 스타일로 프로토타입 체인과 클로저 등으로 객체지향 언어의 상속, 캡슐화(정보 은닉) 등의 개념을 구현할 수 있다.

 

ES5에서는 생성자 함수와 프로토타입을 사용하여 객체지향 프로그래밍을 구현하였다.

 

```

// ES5

var Person = (function() {

    // 생성자

    function Person(name) {

        this._name = name;

    }

 

    // 메소드

    Person.prototype.sayHi = function() {

        console.log('Hi! ' + this._name);

    };

 

    // 생성자 반환

    return Person;

}());

 

var me = new Person('Lee');

me.sayHi(); // Hi! Lee

console.log(me instanceof person); // true

```

 

#### 3.9.1. 클래스 정의

 

ES6 클래스는 class 키워드를 사용하여 정의한다. 앞에서 살펴본 Person 생성자 함수를 클래스로 정의해보자.

 

```

class Person {

    constructor(name) {

        this._name = name;

    }

    sayHi() {

        console.log(`Hi! ${this._name}`);

    }

}

 

const me = new Person('Lee');

me.sayHi(); // Hi! Lee

console.log(me instanceof Person);

```

 

일반적이지는 않지만 표현식으로도 클래스를 정의할 수 있다.

함수와 마찬가지로 클래스는 이름을 가질 수도 있고 갖지 않을 수도 있다.

이때 클래스가 할당된 변수를 사용해 클래스를 생성하지 않고 기명 클래스의 이름을 사용해 생성하면 에러가 발생한다.

이는 함수와 마찬가지로 클래스 표현식에서 사용한 클래스 이름은 외부 코드에서 접근할 수 없기 때문이다.

 

```

const Foo = class MyClass {};

 

const foo = new Foo();

console.log(foo); // MyClass {}

 

new MyClass(); // ReferenceError: MyClass is not defined

```

 

#### 3.9.2. 인스턴스의 생성

 

클래스의 인스턴스를 생성하려면 new 연산자와 함께 constructor(생성자)를 호출한다.

 

```

class Foo {}

const foo = new Foo();

```

 

위 코드에서 new 연산자와 함께 호출한 FOO는 클래스 이름이 아니라 constructor이다.

표현식이 아닌 선언식으로 정의한 클래스의 이름은 constructor와 동일하다.

 

```

console.log(Foo == Foo.prototype.constructor); // true

```

 

new 연산자를 사용하지 않고 constructor를 호출하면 타입 에러가 발생한다.

constructor는 new 연산자 없이 호출할 수 없다.

 

```

class Foo {}

const foo = Foo(); // TypeError: Class constructor Foo cannot be invoked without 'new'

```

 

#### 3.9.3. constructor

 

constructor는 인스턴스를 생성하고 클래스 프로퍼티를 초기화하기 위한 특수한 메소드이다.

constructor는 클래스 내에 한 개만 존재할 수 있으며, 만약 클래스가 2개 이상의 constructor를 포함하면 문법 에러가 발생한다.

인스턴스를 생성할 때 new 연산자와 함께 호출한 것이 바로 constructor이며 constructor의 파라미터에 전달한 값은 클래스 프로퍼티에 할당한다.

 

```

class Foo {}

 

const foo = new Foo();

console.log(foo); // Foo{};

 

// 클래스 프로퍼티의 동적 할당 및 초기화

foo.num = 1;

console.log(foo); // Foo { num: 1 }

```

 

#### 3.9.4. 클래스 프로퍼티

 

클래스 몸체에는 메소드만 선언할 수 있다.

클래스 몸체에 클래스 프로퍼티(멤버변수)를 선언하면 문법 에러가 발생한다.

 

```

class Foo {

    name = ''; //Syntax Error

 

    constructor() {}

}

```

 

클래스 프로퍼티의 선언과 초기화는 반드시 constructor 내부에서 실시한다.

 

```

class Foo {

    constructor(name = '') {

        this.name = name;

    }

}

 

const foo = new Foo('Lee');

console.log(foo); // Foo {name: 'Lee'}

}

```

 

constructor 내부에서 선언한 클래스 프로퍼티는 클래스의 인스턴스를 가리키는 this에 바인딩한다.

이로써 클래스 프로퍼티는 클래스가 생성할 인스턴스의 프로퍼티가 되며, 클래스의 인스턴스를 통해 클래스 외부에서 언제나 참조할 수 있다.

즉, 언제나 public이다.

ES6의 클래스는 다른 객체지향 언어처럼 private, public, protected 키워드와 같은 접근제한자를 지원하지 않는다.

 

```

class Foo {

    constructor(name = '') {

        this.name = name; // public 클래스 프로퍼티

    }

}

 

const foo = new Foo('Lee');

console.log(foo.name); // 클래스 외부에서 참조할 수 있다.

```

 

#### 3.9.5. 호이스팅

 

class 선언문 이전에 클래스를 참조하면 참조 에러가 발생한다.

클래스는 스코프의 선두에서 class의 선언문에 도달할 때까지 `일시적 사각지대`에 빠진다.

따라서 class 선언문 이전에 클래스를 참조하면 참조 에러가 발생한다.

 

```

const foo = new Foo(); // ReferenceError : Foo is not defined

class Foo {}

```

 

#### 3.9.6. getter, setter

 

##### 3.9.6.1 getter

 

getter는 클래스 프로퍼티에 접근할 때마다 클래스 프로퍼티의 값을 조작하는 행위가 필요할 때 사용한다.

getter는 메소드 이름 앞에 get 키워드를 사용해 정의한다.

이때 메소드 이름은 클래스 프로퍼티 이름처럼 사용된다.

다시말해 getter는 호출하는 것이 아니라 프로퍼티처럼 참조하는 형식으로 사용하며 참조 시에 메소드가 호출된다.

 

##### 3.9.6.2. setter

 

setter는 클래스 프로퍼티에 값을 할당할 때마다 클래스 프로퍼티의 값을 조작하는 행위가 필요할 때 사용한다.

setter는 메소드 이름 앞에 set 키워드를 사용해 정의한다.

이때 메소드 이름은 프로퍼티 이름처럼 사용된다.

다시 말해 setter는 호출하는 것이 아니라 프로퍼티처럼 값을 할당하는 형식으로 사용하며 할당 시에 메소드가 호출된다.

 

```

class Foo {

    consturctor(arr = []) {

        this._arr = arr;

    }

 

    // getter : get 키워드 뒤에 오는 메소드 이름 firstElem은 프로퍼티 이름처럼 사용된다.

    get firstElem() {

        // getter는 반드시 무언가를 반환해야 한다.

        return this._arr.length ? this._arr[0] : null;

    }

 

    // setter : set 키워드 뒤에 오는 메소드 이름 firstElem은 프로퍼티 이름처럼 사용된다.

    set firstElem(elem) {

        this._arr = [elem, ...this._arr];

    }

}

 

const foo = new Foo([1, 2]);

 

// 프로퍼티 firstElm에 값을 할당하면 setter가 호출된다.

foo.firstElem = 100;

 

// 프로퍼티 firstElm에 접근하면 getter가 호출된다.

console.log(foo.firstElem); // 100

```

 

#### 3.9.7. 정적 메소드

 

클래스의 정적 메소드를 정의할 때 static 키워드를 사용한다.

정적 메소드는 클래스의 인스턴스가 아닌 클래스 이름으로 호출한다.

따라서 클래스의 인스턴스를 생성하지 않아도 호출할 수 있다.

 

```

class Foo {

    constructor(prop) {

        this.prop = prop;

    }

 

    static staticMethod() {

        return 'staticMethid';

    }

 

    prototypeMethod() {

        return this.prop;

    }

}

 

// 정적 메소드는 클래스 이름으로 호출한다.

console.log(Foo.staticMethod());

 

const foo = new Foo(123);

// 정적 메소드는 인스턴스로 호출할 수 없다.

console.log(foo.staticMethod()); // Uncaught TypeError : foo.staticMethod is not a function

```

 

클래스의 정적 메소드는 인스턴스로 호출할 수 없다.

이것은 `정적 메소드는 this를 사용할 수 없다는 것을 의미한다.`

`일반 메소드 내부에서 this는 클래스의 인스턴스를 가리키며, 메소드 내부에서 this를 사용한다는 것은 클래스의 인스턴스 생성을 전제로 하는 것이다.`

정적 메소드는 클래스 이름으로 호출하기 때문에 클래스의 인스턴스를 생성하지 않아도 사용할 수 있다.

달리 말하면 메소드 내부에서 this를 사용할 필요가 없는 메소드는 정적 메소드로 만들 수 있다.

정적 메소드는 Math 객체의 메소드처럼 애플리케이션 전역에서 사용할 유틸리티 함수를 생성할 때 주로 사용한다.

 

#### 3.9.8. 클래스 상속

 

##### 3.9.8.1. extends 키워드

 

extends 키워드는 부모 클래스를 상속받는 자식 클래스를 정의할 때 사용한다.

 

```

// 부모 클래스

class Circle {

    constructor(radius) {

        this.radius = radius; // 반지름

    }

 

    // 원의 지름

    getDiameter() {

        return 2 * this.radius;

    }

 

    // 원의 둘레

    getPerimeter() {

        return 2 * Matho.PI * this.radius;

    }

 

    // 원의 넓이

    getArea() {

        return Math.PI * Math.pow(this.radius, 2);

    }

}

 

// 자식 클래스

class Cylinder extends Circle {

    constructor(radius, height) {

        super(radius);

        this.height = height;

    }

 

    // 원통의 넒이: 부모 클래스의 getArea 메소드를 오버라이딩하였다.

    getArea() {

        // (원통의 높이 * 원의 둘레) + (2 * 원의 넒이)

        return (this.height * super.getPerimeter()) + (2 * super.getArea());

    }

 

    // 원통의 부피

    getVolume() {

        return super.getArea() * this.height;

    }

}

 

// 반지름이 2, 높이가 10인 원통

const cylinder = new Cylinder(2, 10);

 

// 원의 지름

console.log(cylinder.getDiameter()); // 4

// 원의 둘레

console.log(cylinder.getPerimeter()); // 12.563...

// 원통의 넒이

console.log(cylinder.getArea()); // 150.796...

// 원통의 부피

console.log(cylinder.getVolume()); // 125.663...

// cylinder는 Cylinder 클래스의 인스턴스이다.

console.log(cylinder instanceof Cylinder); // true

// cylinder는 Circle 클래스의 인스턴스이다.

console.log(cylinder instanceof Circle); // true

```

 

프로토타입 체인은 특정 객체의 프로퍼티나 메소드에 접근하려고 할 때 프로퍼티 또는 메소드가 없다면 [[prototype]] 프로퍼티가 가리키는 링크를 따라 자신의 부모 역할을 하는 프로토타입 객체의 프로퍼티나 메소드를 차례대로 검색한다.

그리고 그 검색에 성공하면 그 프로퍼티나 메소드를 사용한다.

 

##### 3.9.8.2. super 키워드

 

super 키워드는 부모 클래스를 참조할 때 또는 부모 클래스의 constructor를 호출할 때 사용한다.

super가 메소드로 사용될 때, 그리고 객체로 사용될 때 다르게 동작하는 것을 알 수 있다.

 

- super 메소드

  super 메소드는 자식 class의 constructor 내부에서 부모 클래스의 constructor를 호출한다.

  즉, 부모 클래스의 인스턴스를 생성한다.

  자식 클래스의 constructor에서 super()를 호출하지 않으면 this에 대한 참조 에러가 발생한다.

 

```

class Parent {}

 

class Child extends Parent {

    constructor(){} // ReferenceError: this is not defined

}

 

const child = new Child();

```

 

- super 키워드

  super 키워드는 부모 클래스에 대한 참조이다.

  부모 클래스의 프로퍼티 또는 메소드를 참조하기 위해 사용한다.

 

```

getVolume() {

    return super.getArea() * this.height;

}

```

 

##### 3.9.8.3. static 메소드와 prototype 메소드의 상속

 

프로토타입 관점에서 바라보면 자식 클래스의 [[Prototype]] 프로퍼티가 가리키는 프로토타입 객체는 부모 클래스이다.

 

```

class Parent {}

 

class Child extends Parent {}

 

console.log(Child.__proto__ === parent); // true

console.log(Child.prototype.__proto === Parent.prototype); // true

```

 

이것은 프로토타입 체인에 의해 부모 클래스의 정적 메소드도 상속됨을 의미한다.

 

```

class Parent {

    static staticMethod() {

        return 'staticMethod';

    }

}

 

class Child extneds Parent {};

 

console.log(Parent.staticMethod()); // 'staticMethod'

console.log(child.staticMethod()); // 'staticMethod'

```

 

자식 클래스의 정적 메소드 내부에서도 super 키워드를 사용하여 부모 클래스의 정적 메소드를 호출할 수 있다.

이는 자식 클래스는 프로토타입 체인에 의해 부모 클래스의 정적 메소드를 참조할 수 있기 때문이다.

### 3.10. 프로미스

 

자바스크립트는 비동기 처리를 위한 하나의 패턴으로 콜백 함수를 사용한다.

전통적인 콜백 패턴은 가독성이 나쁘고 비동기 처리 중 발생한 에러의 예외 처리가 곤란하며, 여러 개의 비동기 처리 로직을 한꺼번에 처리하는 것도 한계가 있다.

ES6에서 비동기 처리를 위한 또 다른 패턴으로 프로미스를 도입하였다.

 

#### 3.10.1. 콜백 패턴의 단점

 

동기식 처리 모델은 task를 직렬로 수행한다.

순차적으로 실행되며, 어떤 작업이 수행중이면 다음 태스크는 대기하게 된다.

 

비동기 처리 모델은 태스크를 병렬로 수행한다.

즉, 태스크가 종료되지 않은 상태더라도 대기하지 않고 즉시 다음 태스크를 실행한다.

 

##### 3.10.1.1. 콜백 헬

 

자바 스크립트에서 빈번하게 사용되는 비동기식 처리 모델은 요청을 병렬로 처리하여 다른 요청이 블로킹 되지 않는 장점이 있다.

하지만 비동기 처리를 위해 콜백 패턴을 사용하면 처리 순서를 보장하기 위해 여러 개의 콜백 함수가 중첩되어 복잡도가 높아지는 `콜백 헬`이 발생하는 단점이 있다.

콜백 헬은 가독성을 나쁘게 하며 실수를 유발하게 하는 원인이 된다.

 

```

step1(function(value1) {ㄴ

    step2(value1, function(value2) {

        step2(value2, function(value3) {

            step2(value3, function(value4) {

                step2(value4, function(value) {

                    //  values5를 사용하는 자리

                });

            });

        });

    });

});

```

 

비동기 처리 모델은 실행 완료를 기다리지 않고 즉시 다음 테스크를 실행한다.

비동기 함수(비동기를 처리하는 힘수) 내에서 처리 결과를 반환(또는 전역 변수에 할당)하면 기대한대로 동작하지 않는다.

 

비동기 함수의 처리 결과를 반환하는 경우, 순서가 보장되지 않기 떄문에 그 반환 결과를 가지고 후속 처리 할 수 없다.

즉, 비동기 함수의 처리 결과에 대한 처리는 비동기 함수의 콜백내에서 처리해야 한다. 이로인해 `콜백 헬`이 발생한다.

 

만일 비동기 함수의 처리 결과를 가지고 다른 비동기 함수를 호출해야 하는 경우, 함수의 호출이 중첩되어 복잡도가 높아지는 현상이 발생하는데, 이를 `콜백 헬`이라 한다.

콜벡 헬은 코드의 가독성을 나쁘게 하고 복잡도를 증가시켜 실수를 유발하는 원인이 되며 에러처리가 곤란하다.

 

##### 3.10.1.2. 에러 처리의 한계

 

콜백 방식의 비동기 처리가 갖는 문제점 중에서 가장 심각한 것은 에러 처리가 곤란하다는 것이다.

함수가 실행되면 1초 후에 콜백 함수가 실행되고 이 콜백 함수는 예외를 발생시키지만, 호출 스택에 해당 함수가 존재하지 않아 catch 블록에서 캐치되지 않는 현상이 발생한다.

이러한 문제를 극복하기 위해 프로미스가 제안되었다.

 

#### 3.10.2. 프로미스의 생성

 

프로미스는 Promise 생성자 함수를 통해 인스턴스화 한다.

Promise 생성자 함수는 비동기 작업을 수행할 콜백 함수를 인자로 전달받는데 이 콜백 함수는 resolve와 reject 함수를 인자로 전달받는다.

 

```

// Promise 객체의 생성

const promise = new Promise((resolve, reject) => {

    // 비동기 작업을 수행한다.

    if(/* 비동기 작업 수행 성공 */) {

        resolve('result');

    }

    else { /* 비동기 작업 수행 실패 */

        reject('failure reason');

    }

});

```

 

프로미스는 비동기 처리가 성공하였는지 또는 실패하였는지 등의 상태 정보를 갖는다.

| 상태 | 의미 | 구현 |

|-----------|-----------------------------------|---------------------------------------------|

| pending | 비동기 처리가 아직 수행되지 않은 상태 | resolve 또는 reject 함수가 아직 호출되지 않은 상태 |

| fulfilled | 비동기 처리가 수행된 상태 (성공) | resolve 함수가 호출된 상태 |

| rejected | 비동기 처리가 수행된 상태 (실패) | reject 함수가 호출된 상태 |

| settled | 비동기 처리가 수행된 상태 (성공 또는 실패) | resolve 또는 reject 함수가 호출된 상태 |

 

Promise 생성자 함수를 인자로 전달받은 콜백 함수는 내부에서 비동기 처리 작업을 수행한다.

이때 비동기 처리가 성공하면 콜백 함수의 인자로 전달받은 resolve 함수를 호출한다.

이때 프로미스는 'fulfilled' 상태가 된다.

비동기 처리가 실패하면 reject 함수를 호출한다.

이때 프로미스는 'rejected' 상태가 된다.

 

```

// 비동기 함수

function get(url) {

    // promise 객체의 생성과 반환

    return new promise((resolve, reject) => {

        // XMLHttpRequest 객체 생성

        const xhr = new XMLHttpRequest();

 

        // 서버 응답 시 호출될 이벤트 핸들러

        xhr.onreadystatechange = function() {

            // 서버 응답 완료

            if(xhr.readyState === XMLHttpRequest.DONE) {

                if(xhr.status === 200) { // 정상 응답

                    // resolve 메소드에 처리 결과를 전달

                    resolve(xhr.response);

                } else { // 비정상 응답

                    // reject 메소드에 에러 메시지를 전달

                    reject('Error: ' + xhr.status);

                }

            }

        };

 

        // 비동기 방식으로 Request 오픈

        xhr.open('GET', url);

        // Request 전송

        xhr.send();

    });

}

```

 

#### 3.10.3. 프로미스의 사용

 

Promise로 구현된 비동기 함수는 Promise 객체를 반환하여야 한다.

Promise로 구현된 비동기 함수를 호출하는 측에서는 Promise 객체의 후속 처리 메소드를 통해 비동기 처리 결과 또는 에러 메시지를 전달받아 처리한다.

Promise 객체는 상태를 갖는다고 하였다. 이 상태에 따라서 후속 처리 메소드를 체이닝 방식으로 호출한다.

Promise 후속처리 메소드는 아래와 같다.

 

- then : 두 개의 콜백 함수를 인자로 전달 받는다. 첫번째 콜백 함수는 성공(fulfilled, resolve 함수가 호출된 상태) 시 호출되고, 두번째 콜백함수는 실패(rejected, reject 함수가 호출된 상태) 시 호출된다.

- catch : 예외 (비동기 처리에서 발생한 에러와 then 메소드에서 발생한 에러)가 발생하면 호출된다.

 

```

<!DOCTYPE html>

<html>

<head>

    <title>Promise example</title>

</head>

<body>

    <h1>Promise example</h1>

    <pre id="result"></pre>

    <script>

    // 비동기 함수

    function get(url) {

        ...

    }

 

    const url = 'http://jsonplaceholder.typicode.com/post/1';

 

    /*

        비동기 함수 get은 Promise 객체를 반환한다.

        Promise 객체의 후속 메소드를 사용하여 비동기 처리 결과에 대한 후속 처리를 수행한다.

    */

    get(url).then(

        // 첫 번째 콜백 함수는 성공(fulfilled, resolve 함수가 호출된 상태) 시 호출된다.

        result => document.getElementById('result').innerHTML = result,

        // 두 번째 함수는 실패(rejected, reject 함수가 호출된 상태) 시 호출된다.

        error => console.log(error)

    );

    </script>

</body>

</html>

```

 

#### 3.10.4. 프로미스의 에러 처리

 

비동기 처리 시 발생한 에러 메시지는 then 메소드의 두 번째 콜백 함수로 전달된다.

Promise 객체의 후속 처리 메소드 catch를 사용하여도 에러를 처리할 수 있다.

 

```

get(url)

    .then(result => document.getElementById('result').innerHTML = result)

    .catch(error => console.log(error));

```

 

catch 메소드는 에러를 처리한다는 점에서 then 메소드의 두번째 콜백 함수와 유사하지만 미묘한 차이가 있다.

 

- then 메소드의 두번째 콜백 함수 : 비동기 처리에서 발생한 에러(reject 함수가 호출된 상태)만을 캐치한다.

- catch 메소드 : 비동기 처리에서 발생한 에러뿐만 아니라, then 메소드 내부에서 발생한 에러도 캐치한다.

 

따라서 에러처리는 catch 메소드를 사용하는 편이 보다 효율적이다.

 

#### 3.10.5. 프로미스 체이닝

 

비동기 함수의 처리 결과를 가지고 다른 비동기 함수를 호출해야 하는 경우, 함수의 호출이 중첩되어 복잡도가 높아지는 콜백 헬이 발생한다.

프로미스는 후속 처리 메소드를 체이닝하여 여러개의 프로미스를 연결하여 사용할 수 있다. 이로서 콜백 헬을 해결한다.

Promise 객체를 반환한 비동기 함수는 프로미스 후속 처리 메소드인 then이나 catch 메소드를 사용할 수 있다.

따라서 then 메소드가 Promise 객체를 반환하도록 하면 여러개의 프로미스를 연결하여 사용할 수 있다.

 

아래는 서버로부터 특정 포스트를 취득한 후, 그 포스트를 작성한 사용자의 아이디로 작성된 다른 포스트를 검색하는 예제이다.

 

```

<!DOCTYPE html>

<html>

<head>

    <title>Promise example</title>

</head>

<body>

    <h1> Promise Example </h1>

    <pre id="result"></pre>

    <script>

        //  비동기 함수

        function get(url) {

            ...

        }

 

        const url = 'http://jsonplaceholder.typicode.com/posts';

 

        // 포스트 id가 1인 포스트를 검색하고 프로미스 반환

        get(`${url}/1`)

        // 포스트 id가 1인 포스트 작성자의 아이디로 작성된 모든 포스트 검색하고 프로미스 반환

        .then(result1 => get(`${url}?userId=${JSON.parse(result1).userId}`))

        // 포스트 검색 결과를 DOM에 반영

        .then(result2 => document.getElementById('result').innerHtml = result2)

        .catch(error => console.log(error));

    </script>

</html>

```
