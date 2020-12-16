## 4. TypeScript

 

### 4.1. TypeScript의 장점

 

#### 4.1.1. 정적 타입

 

```

function(a, b) {

    return a + b;

}

sum('x', 'y'); // 'xy'

```

 

위 함수에서는 두개의 인수를 받고 있지만, 어떤 타입의 인수를 전달하여야 하는지, 어떤 타입의 반환값을 리턴해야 하는지 명확하지 않다.

문자열을 인수로 전달해도 자바스크립트 문법 상 아무런 문제가 없으므로 위 코드를 실행할 것이다.

이러한 이유는 변수나 반환값의 타입을 사전에 지정하지 않는 자바 스크립트의 `동적 타이핑`에 의한 것이다/

하지만 TypeScript는 정적 타입을 지원한다는 큰 특징이 있다.
 

#### 4.1.2. 도구의 지원

 

TypeScript를 사용하는 가장 큰 장점은 IDE(통합개발환경)를 포함한 다양한 도구의 지원을 받을 수 있다는 것이다.

 

#### 4.1.3. 강력한 객체지향 프로그래밍 지원

 

인터페이스, 제네릭 등과 같은 강력한 객체지향 프로그래밍 지원은 크고 복잡한 프로젝트의 코드 기반을 쉽게 구성할 수 있게 한다.

클래스 기반 객체지향 언어에 익숙한 개발자가 자바스크립트 프로젝트를 수행하는 데 진입 장벽을 낮추는 효과도 있다.

 

#### 4.1.4. ES6 / ESNext 지원

 

ES6를 완전히 지원하지 않고 있는 브라우저를 고려하여 Babel 등의 트랜스파일러를 사용해야 하는 수고스러움이 있다.

아직 ECMAScript 표준에 포함되지 않았지만 표준화가 유력한 스펙을 선제적으로 도입하므로 새로운 스펙의 유용한 기능을 안전하게 도입하기에 유리하다.

 

#### 4.1.5. Angular

 

Angular는 TypeScript 뿐만 아니라 자바스크립트(ES5, ES6), Dart로도 작성할 수 있지만, 가장 많이 사용되고 있는 언어는 TypeScript이다.


### 4.2. TypeScript 개발환경 구축

 

#### 4.2.1. TypeScipt 컴파일러 사용법

 

##### 4.2.1.1. 하나의 파일을 컴파일링

 

TypeScript 파일(.ts)은 브라우저에서 동작하지 않으므로 TypeScript 컴파일러(tsc)를 이용해 자바스크립트 파일로 변환해야 한다.

이를 컴파일 또는 `트랜스파일링`이라 한다.

.ts 파일을 트랜스파일링 하면, 같은 디렉터리에 자바스크립트 파일이 생성된다.

 

```

// 트랜스파일링 실행

tsc {확장자를 제외한 파일명}

```

 

이때 트랜스파일링된 자바스크립트 버전은 `ES3`이다.

이는 TypeScript를 트랜스파일링해서 생성되는 자바스클립트의 기본 버전이 ES3이기 때문이다.

만약에 자바스크립트 버전을 변경하려면 컴파일 옵션에 --target 또는 -t를 사용한다.

예를 들어 ES6 버전으로 트랜스파일링을 실행하려면 아래와 같이 옵션을 추가한다.

 

```

tsc {확장자를 제외한 파일명} -t es6

```

 

트랜스파일링이 성공하여 자바스크립트 파일이 생성되었으면 Node.js REPL을 이용해 트랜스파일링된 파일을 실행하여 결과를 확인할 수 있다.

 

```

node {확장자를 제외한 파일명}

```

 

##### 4.2.1.2. 여러개의 파일을 컴파일링

 

여러 개의 TypeScript 파일을 한번에 트랜스파일링 할 수도 있다.

 

```

// 트렌스파일링 실행

tsc {확장자를 제외한 파일명} {확장자를 제외한 파일명}

 

// 결과 확인

node  {확장자를 제외한 파일명}

```

 

와일드카드를 사용하여 모든 TypeScirpt 파일을 한꺼번에 트랜스파일링 할 수도 있다.

 

```

// 파일을 한꺼번에 트랜스파일링

tsc *.ts

```

 

--watch 또는 -w 옵션을 사용하면 트랜스파일링 대상 파일의 내용이 변경되었을 때 이를 감지하여 자동으로 트랜스파일링이 실행된다.

 

```

// 변경사항을 감지하여 트랜스파일링

tsc {확장자를 제외한 파일명} --watch

```

 

파일 변경이 감지되고 자동으로 트랜스파일링이 실행된다.

다음과 같은 메시지가 기록된다.

 

```

21:34:39 - File change detected. Starting incremental compiltion...

21:24:39 - Compilation complete. Watching for file changes.

```

 

```

function(a: number, b: number) {

    return a + b;

}

sum('x', 'y'); // error TS2345: Argument of type '"X"' is not assignable to parameter of type 'number'.

```

 

TypeScript는 정적 타입을 지원하므로 컴파일 단계에서 오류를 포착할 수 있는 장점이 있다.

이는 코드의 가독성을 높이고 디버깅을 쉽게 한다.

### 4.3. 정적 타이핑

 

#### 4.3.1. 타입 선언

 

TypeScript는 다음과 같이 변수명 뒤에 타입(자료형)을 명시하는 것으로 타입을 선언 할 수 있다.

 

```

// 변수 foo는 string 타입이다.

let foo: string = 'hello';

```

 

선언한 타입에 맞지 않는 값을 할당하면 컴파일 시점에 에러가 발생한다.

 

```

let bar: number = true; // error TS2322: Type 'true' is not assignable to type 'number'.

```

 

이러한 타입 선언은 개발자가 코드를 예측할 수 있도록 돕는다.

또한 타입 선언은 강력한 타입 체크를 가능하게 하여 문법 에러나 타입과 일치하지 않는 값의 할당 등 기본적인 오류를 런타임 이전에 검출한다.

 

`자바스크립트와 TypeScript의 타입`

| 타입 | JS | TS | 설명 |

|-----|----|----|-----|

| boolean | o | o | true와 false |

| null | o | o | 값이 없다는 것을 명시 |

| undefined | o | o | 값을 할당하지 않은 변수의 초깃값 |

| number | o | o | 숫자(정수와 실수, Infinity, NaN) |

| string | o | o | 문자열 |

| symbol | o | o | 고유하고 수정 불가능한 데이터 타입이며 주로 객체 프로퍼티의 식별자로 사용(ES6에서 추가) |

| object | o | o | 객체형(참조형) |

| array | | | 배열 |

| tuple | | | 고정된 요소 수만큼의 자료형을 미리 선언 후 배열을 표현 |

| enum | | | 열거형. 숫자 값 집합에 이름을 지정한 것 |

| any | | | 타입 추론할 수 없거나 타입 체크가 필요 없는 변수에 사용. var 키워드로 선언한 변수와 같이 어떤 타입의 값이라도 할당 가능 |

| void | | | 일반적으로 함수에서 반환값이 없을 때 사용 |

| never | | | 결코 발생하지 않는 값 |

 

다양한 타입을 선언하는 방법은 다음과 같다.

타입은 대문자, 소문자를 구별하므로 주의가 필요하다.

TypeScript가 기본 제공하는 타입은 모두 소문자이다.

 

```

// boolean

let isDone: boolean = false;

 

// null

let n: null = null;

 

// undefined

let u: undefined = undefined;

 

// number

let decimal: number = 6;

let hex : number = 0xf00d;

let binary: number = 0b1010;

let octal: number = 0o744;

 

// string

let color: string = "blue";

color = 'red';

let myName: string = 'Lee'; // ES6 템플릿 문자열

let greeting: string = `Hello, my name is ${ myName }.` // ES6 템플릿 대입문

 

// object

const obj: object = {};

 

// array

let list1: any[] = [1, 'two', true];

let list2: number[] = [1, 2, 3];

let list3: Array<number> = [1, 2, 3]; // 제네릭 배열 타입

 

/* tuple : 고정된 요소 수만큼의 타입을 미리 선언 후 배열을 표현

    첫 번째 요소는 string 타입이고 두 번째 요소는 number 타입 */

let tuple: [string, number];

tuple = ['hello', 10]; // OK

tuple = [10, 'hello']; // Error

tuple = ['hello', 10, 'world', 100]; // Error

tuple.push(true); // Error

 

// enum : 열거형은 숫자 값 집합에 이름을 지정한 것이다.

enum Color1 {Red, Green, Blue};

let c1: Color1 = Color1.Green;

console.log(c1); // 1

enum Color2 {Red = 1, Green, Blue};

let c2: Color2 = Color12Green;

console.log(c2); // 2

enum Color3 {Red = 1, Green = 2, Blue = 4};

let c3: Color3 = Color3.Green;

console.log(c3); // 4

 

/* any: 타입 추론(type inference) 할 수 없거나 타입 체크가 필요 없는 변수에 사용한다.

    var 키워드로 선언한 변수와 같이 어떤 타입의 값이라도 할당할 수 있다,

*/

let notSure: any = 4;

notSure = 'maybe a string instead';

notSure = false; // okay, definitely a boolean

 

// void : 일반적으로 함수에서 반환값이 없을 때 사용한다.

function warnUser(): void {

    console.log("This is my warning message");

}

 

// never : 결코 발생하지 않는 값

function infiniteLoop(): never {

    while(true) {}

}

 

function error(message: string): never {

    throw new Error(message);

}

```

 

#### 4.3.2. 정적 타이핑

 

C나 Java 같은 C-family 언어는 변수를 선언할 때 변수에 할당할 값의 타입에 따라 사전에 타입을 명시적으로 선언해야 하며,

선언된 타입에 맞는 값을 할당해야 한다. 이를 `정적 타이핑`이라 한다.

 

반면에 자바스크립트는 동적 타입 언어 혹은 느슨한 타입 언어이다.

이것은 변수의 타입 선언 없이 값이 할당되는 과정에서 동적으로 타입을 추론한다는 의미이다.

동적 타입 언어는 타입 추론에 의해 변수의 타입이 결정된 후에도 같ㅇㄴ 변수에 여러 타입의 값을 교차하여 할당할 수 있다.

이를 `동적 타이핑`이라 한다.

 

동적 타이핑은 사용하기 간편하지만 코드를 예측하기 힘들어 예상치 못한 오류를 만들 가능성이 높다.

또는 IDE와 같은 도구가 변수나 매개변수, 함수의 반환값의 타입을 알 수 없어 코드 어시스트 등의 기능을 지원할 수 없다.

 

```

var foo;

console.log(typeof foo); // undefined

 

foo = null;

console.log(typeof foo); // object

 

foo = {};

console.log(typeof foo); // object

 

foo = 3;

console.log(typeof foo); // number

 

foo = 3.14;

console.log(typeof foo); // number

 

foo = "Hi there";

console.log(typeof foo); // String

 

foo = true;

console.log(typeof foo); // boolean

```

 

TypeScript의 가장 독특한 특징은 정적 타이핑을 지원한다는 것이다.

정적 타입 언어는 타입을 명시적으로 선언하며, 타입이 결정된 후에는 타입을 변경할 수 없다.

잘못된 타입의 값이 할당 또는 반환되면 컴파일러는 이를 감지해 에러를 발생시킨다.

정적 타이핑은 변수는 물론 함수의 매개변수와 반환값에도 사용할 수 있다.

 

정적 타이핑의 장점은 `코드 가독성, 예측성, 안정성`이라고 볼 수 있으며, 이는 대규모 프로젝트에 매우 적합하다.

 

#### 4.3.3. 타입 추론

 

타입 선언을 생략하면 값이 할당되는 과정에서 동적으로 타입이 결정된다. 이를 `타입 추론`이라고 한다.

 

```

let foo = 123; // foo는 number 타입

```

 

변수 foo에 타입을 선언하지 않았으나 타입 추론에 의해 변수의 타입이 결정된다.

동적 타입 언어는 타입 추론에 의해 변수의 타입이 결정된 후에도 같은 변수에 여러 타입의 값을 교차하여 할당할 수 있지만,

정적 타입의 언어는 타입이 결정된 후에는 타입을 변경할 수 없다. -> 에러가 발생함.

 

타입 선언을 생략하고 값도 할당하지 않아서 타입을 추론할 수 없으면 any 타입이 된다.

any 타입의 변수는 자바스크립트의 var ㅣ쿼드로 선언한 변수처럼 어떤 타입의 값도 재할당이 가능하다.

이는 TypeScript를 사용하는 장점을 없애기 때문에 사용하지 않는 편이 좋다.

 

```

let foo; // let foo: any와 같음

foo = 'Hello';

console.log(typeof foo); // string

foo = true;

console.log(typeof foo); // boolean

```

### 4.4. 클래스

 

#### 4.4.1. 클래스 정의

 

ES6 클래스는 클래스 몸체에 메소드만 포함할 수 있다.

클래스 몸체에 클래스 프로퍼티를 선언할 수 없고, 반드시 생성자 내부에서 클래스 프로퍼티를 선언하고 초기화한다.

TypeScript 클래스는 몸체에 클래스 프로퍼티를 사전에 선언해야 한다.

 

```

class Person {

    // 클래스 프로퍼티를 사전에 선언하여야 한다.

    // ES6에서는 사전에 선언하지 않아도 된다.

    name : string;

 

    constructor(name: string) {

        // 클래스 프로퍼티에 값을 할당

        this.name = name;

    }

 

    walk() {

        console.log(`${this.name} is walking.`);

    }

}

 

const person = new Foo('Lee');

person.walk(); // Lee is walking

```

 

#### 4.4.2. 접근 제한자

 

TypeScript 클래스는 클래스 기반 객체지향 언어가 지원하는 접근 제한자 public, private, protected를 지원하며 의미 또한 기본적으로 동일하다.

접근제한자를 명시하지 않았을 때 TypeScript의 클래스 프로퍼티와 메소드는 암묵적으로 public이 선언된다.

 

#### 4.4.3. readonly 키워드

 

TypeScript는 readonly 키워드를 사용할 수 있다.

readonly가 선언된 클래스 프로퍼티는 선언 시 또는 생성자 내부에서만 값을 할당할 수 있다.

그 외의 경우에는 값을 할당할 수 없고 오직 읽기만 가능한 상태가 된다.

이를 이용하여 상수 선언에 사용한다.

 

```

class Foo {

    private readonly MAX_LEN: number = 5;

    private readonly MSG: string;

 

    constructor() {

        this.MSG = 'hello';

    }

 

    log() {

        // readonly가 선언된 프로퍼티는 재할당이 금지된다.

        this.MAX_LEN = 10; /* Cannot assign to 'MAX_LEN' because it is a constant or a read-only property. */

        this.MSG = 'Hi'; /* Cannot assign to 'MSG' because it is a constant or a read-only property. */

        console.log(`MAX_LEN: ${this.MAX_LEN}`); // MAX_LEN: 5

        console.log(`MSG: ${this.MSG}`); // MSG: hello

    }

}

 

new Foo().log();

```

 

#### 4.4.4. static 키워드

 

static 키워드는 클래스의 정적 클래스를 정의한다.

정적 메소드는 클래스의 인스턴스가 아닌 클래스 이름으로 호출한다.

따라서 클래스의 인스턴스를 생성하지 않아도 호출할 수 있다.

 

```

class Foo {

    constructor(prop) {

        this.prop = prop;

    }

 

    static staticMethod() {

        /*

            정적 메소드는 this를 사용할 수 없다.

            정적 메소드 내부에서 this는 클래스의 인스턴스가 아닌 클래스 자신을 가리킨다.

        */

        return 'staticMethod';

    }

 

    prototypeMethod() {

        return this.prop;

    }

}

 

// 정적 메소드는 클래스 이름으로 호출한다.

console.log(Foo.staticMethod());

 

const foo = new Foo(123);

// 정적 메소드는 인스천스로 호출할 수 없다.

console.log(foo.staticMethod()); // Uncaught TypeError: foo.staticMethod is not a function.

```

 

TypeScript에서는 static 키워드를 클래스 프로퍼티에도 사용할 수 있다.

정적 메소드와 마찬가지로 정적 클래스 프로퍼티는 인스턴스가 아닌 클래스 이름으로 호출하며 클래스의 인스턴스를 생성하지 않아도 호출할 수 있다.

 

```

class Foo {

    // 생성된 인스턴스의 개수

    static instanceCounter = 0;

 

    constructor() {

        // 생성자가 호출될 때마다 카운터를 1씩 증가시킨다.

        Foo.instanceCounter++;

    }

}

 

var foo1 = new Foo();

var foo2 = new Foo();

 

console.log(Foo.instanceCounter); // 2

console.log(foo2.instanceCounter); // error TS2339: Property 'instanceCounter' does not exist on type 'Foo'.

```

 

#### 4.4.5. 추상 클래스

 

추상 클래스는 하나 이상의 추상 메소드를 포함하며 일반 메소드도 포함할 수 있다.

추상 메소드는 내용이 없이 메소드 이름과 타입만 선언된 메소드를 말하며, 선언할 때 abstract 키워드를 사용한다.

추상 클래스를 선언할 때는 abstract 키워드를 사용하며, 직접 인스턴스를 생성할 수 없고 상속만을 위해 사용된다.

추상 클래스를 상속한 클래스는 추상 클래스의 추상 메소드를 반드시 구현해야 한다.

 

```

abstract class Animal {

    // 추상 메소드

    abstract makeSound(): void;

 

    // 일반 메소드

    move(): void {

        console.log('roaming the earth...');

    }

}

 

// 직접 인스턴스를 생성할 수 없다.

// new Animal();

// error TS2511: Cannot create an instance of the abstract class 'Animal'.

 

class Dog extends Animal {

    // 추상 클래스를 상속한 클래스는 추상 클래스의 추상 메소드를 반드시 구현하여야 한다.

    makeSound() {

        console.log('bowwow~');

    }

}

 

const myDog = new Dog();

myDog.makeSound();

myDog.move();

```
