## 9. 파이프



### 9.1. 파이프란?



`데이터가 화면에 표시되는 형식만 변경하고 싶을 때 사용한다.`

애플리케이션이 관리하는 데이터는 사용자가 실생활에서 익숙한 형태가 아닐때가 많다.

예를 들어 Date 생성자 함수가 리턴하는 인스턴스를 문자열화 하면 아래와 같다.



```

const today = new Date();

console.log(today.toString()); // Thu December 17 2020 18:23:31 GMT+0900 (KST)

```



Date 생성자 함수가 리턴한 인스턴스를 문자열로 나타내면 사용자가 읽기 쉬운 형식은 아니다.

파이프를 이용해서 데이터를 사용자가 읽기 쉬운 형태로 변경할 수 있다.



```

// app.component.ts

import { Component } from '@angular/core';



@Component({

   selector: 'app-root',

   template: `

       <h2>{{ today }}</h2>

       <h2>{{ today | date }}</h2>

       <h2>{{ today | date 'y년 MM월 dd일 HH시 mm분 ss초' }}</h2>

   `

})

export class AppComponent {

   today = new Date();

}

```



파이프를 사용한 위 컴포넌트의 출력 결과는 다음과 같다.



```

Thu Dec 17 2020 18:23:31 GMT+0900 (KST)

Dec 17, 2020

2020년 12월 17일 18시 23분 31초

```



파이프의 사용방법은 다음과 같다.



```

{{ value | PipeName }}

{{ value | PipeName : Option : OptionValue }}

{{ value | PipeName1 | PipeName2 }}

```



파이프의 대상 값 뒤에 파이프 연산자 |를 붙인 후, 원하는 파이프를 지정한다.

콜론(:)으로 구분하여 파이프 옵션을 지정할 수 있고, 파이프 연산자 |를 연이어 체이닝 방식으로 파이프를 추가할 수도 있다.



또 다른 예로 문자열을 대문자로 변환하여 보겠다.



```

// app.component.ts

import {{ Component }} from '@angular/core';



@Component({

   selector : 'app-root',

   template: '{{ name | uppercase }}'

})

export class AppComponent {

   name = 'lee';

}

```



실행결과 : LEE



### 9.2. 빌트인 파이프



Angular는 uppercase 이외에도 아래와 같은 빌트인 파이프를 지원한다.

|파이프 | 의미 |

|-----|-----|

| date | 날짜 형식 변환 |

| json | JSON 형식 변환 |

| uppercase | 대문자 변환 |

| lowercase | 소문자 변환 |

| currency | 통화 형식 변환 |

| percent | 퍼센트 형식 변환 |

| decimal | 자리수 형식 변환 |

| slice | 문자열 추출 |

| async | 비동기 객체 출력 |



빌트인 파이프의 사용 예제는 다음과 같다.



```

// app.component.ts

import {{ Component }} from '@angular/core';

import {{ interval }} from 'rxjs';



@Component({

   selector : 'app-root',

   template: '

       <h3>Date Pipe</h3>

       <p>{{ today | date: 'y년 MM월 dd일 HH시 mm분 ss초' }}</p>



       <h3>CuurencyPipe</h3>

       <!-- 한국 원: 통화 기호 표시: 소수점 위 최소 1자리 소수점 아래 1~2 -->

       <p>{{ price | currency: 'KRW':'symbol':'1.1-2' }}</p>



       <h3>SlicePipe : array</h3>

       <ul>

           <li *ngFor="let i of collection | slice:1:3">{{i}}</li>

       </ul>



       <h3>SlicePipe : string</h3>

       <p>{{ str | slice:0:4 }}</p>



       <h3>JsonPipe</h3>

       <pre>{{ object | json }}</pre>



       <h3>DecimalPipe</h3>

       <p>{{ pi | number:'3.5' }}</p>



       <h3>PercentPipe</h3>

       <p>{{ num | percent:'3.3' }}</p>



       <h3>UpperCasePipe</h3>

       <p>{{ str | uppsercase }}</p>



       <h3>LowerCasePipe</h3>

       <p>{{ str | lowercase }}</p>



       <h3>AsyncPipe</h3>

       <p>{{ second$ | async }}</p>

   '

})

export class AppComponent {

   today = new Date();

   price = 0.1234;

   collection = ['a', 'b', 'c', 'd'];

   str = 'abcdefghij';

   object = { foo: 'bar', baz: 'qux', nested: { xyz: 3 } };

   pi = 3.141592;

   num = 1.3495;

   // 1s마다 값을 방출하고 10개를 take한다. (0~9)

   second$ = interval(1000).pipe(take(10))

}

```



실행결과:

`DatePipe`

2020년 12월 17일 18시 59분 40초

`CurrentPipe`

\0.12

`SlicePipe : array`

b

c

`SlicePipe : string`

abcd

`JsonPipe`

{

"foo": "bar",

"baz": "qux",

"nested": {

"xyz": 3

}

}

`DecimalPipe`

003.14159

`PercentPipe`

134.950%

`UpperCasePipe`

ABCDEFGHIJ

`LowerCasePipe`

abcdefghij

`AsyncPipe`

998
