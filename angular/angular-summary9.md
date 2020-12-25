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

### 9.3. 체이닝 파이프



여러개의 파이프를 조합하여 결과를 출력하는 것을 체이닝 파이프라고 한다.

예를 들어 슬라이스 파이프와 대문자 파이프를 체이닝 해보자.



```

// app.component.ts

import { Component } from '@angular/core';



@Component({

   selector: 'app-root',

   template: `

       <h3>SlicePipe + UpperCasePipe</h3>

       <p>{{ name | slice:4 | uppercase }}</p>

   `

})

export class AppComponent {

   name = 'Lee ung-mo';

}

```



실행결과

`SlicePipe + UpperCasePipe`

UNG-MO



### 9.4. 커스텀 파이프



사용자가 입력한 문자열을 반전하는 커스텀 파이프를 작성해보자.

Angular CLI를 사용하여 프로젝트를 생성하고 파이프를 추가한다.



```

$ ng new pipe-custom -t -s -S

$ cd pipe-custom

$ ng generate pipe reverse

```



생성된 파이프를 다음과 같이 수정한다.



```

// reverse.pipe.ts

import {{ Pipe, PipeTransform }} from '@angular/core';



@Pipe({

   name: 'reverse'

})

export class ReversePipe implements PipeTransform {

   transform(value = ''): string {

       return value.split('').reverse().join('');

   }

}

```



파이프는 @Pipe 데코레이터가 장식된 클래스이다.

@Pipe 메타데이터 객체의 name 프로퍼티에 파이프의 식별자를 지정한다.

파이프 클래스는 PipeTransform 인터페이스의 추상 메소드 transform을 구현해야 한다.



```

transform(value:any, ...args: any[]): any

```



커스텀 파이프는 모듈의 declarations에 등록해야 하지만, Angular CLI를 사용해서 파이프를 생성하면 모듈에 자동으로 등록된다.



```

// app.module.ts

import { NgModule } from '@angular/core';

import { BrowserModule } from '@angular/platform-browser';

import { FormsModule } from '@angular/forms';



import { AppComponent } from './app.component';

import { ReversePipe } from './reverse.pipe';



@NgModule({

   declarations: [ AppComponent, ReversePipe ],

   imports: [ BrowserModule, FormsModule ],

   bootstrap: [AppComponent]

})

export class AppModule{}

```



커스텀 파이프는 빌트인 파이프와 동일한 방법으로 탬플릿에서 사용한다.

### 9.5. 파이프와 변화 감지



`변화 감지란, 뷰와 모델의 동기화를 유지하기 위해 상태 변화를 감지하고 이를 반영하는 것을 말한다.`

즉, 상태의 변화를 감지하여 뷰에 반영하는 것으로 데이터 바인딩은 변화 감지 매커니즘의 토대 위에서 수행된다.

Angular는 DOM 이벤트(Click, key press, mouse move 등), Timer(setTimeout, setInterval)의 tick 이벤트, 서버와의 Ajax 통신 이후 변화 감지를 통해 데이터 바인딩 대상의 변경 사항을 찾는다.

이것은 시스템에 부하를 증가시키는 작업이다.

Angular는 가능한 부하를 최소한으로 하기 위해 파이프를 사용할 떄는 보다 간단하고 빠른 변경 알고리즘을 사용한다.



간단한 예제를 통해 파이프와 변화 감지에 대해 살펴보겠다.

Angular CLI를 사용해 프로젝트를 생성하고 컴포넌트를 추가한다.



```

$ ng new pipe-change-detection -t -s -S

$ cd pipe-change-detection

$ ng generate component todos --flat

```



루트 컴포넌트를 아래와 같이 수정한다.



```

// app.component.ts

import { Component } from '@angular/core';



@Component({

   selector: 'app-root',

   template: '<app-todos></app-todos>'

})



export class AppComonent {}

```



생성된 컴포넌트를 다음과 같이 수정한다.



```

// todos.component.ts

import { Component } from '@angular/core';



export interface Todo {

   id: number;

   content: string;

   completed: boolean;

}



@Component({

   selector: 'app-todos',

   template: `

       <input #todo type="text">

       <button (click)="add(todo.value)">add</button>

       <ul>

           <li *ngFor="let todo of toods"

           (click)="complete(todo.id)"

           [class.completed]="todos.completed">{{ todos.content }}</li>

       </ul>

       <pre>{{ todos | json }}</pre>

   `,

   styles: [`

       .completed { text-decoration: line-through; }

   `]

})

export class TodosComponent {

   todos: Todo[] = [

       {id: 1, content: 'HTML', completed: false},

       {id: 2, content: 'CSS', completed: false},

       {id: 3, content: 'Javascript', completed: false}

   ]

};



add(content: string) {

   this.todos.push({

       id: this.getNextId(),

       content,

       completed: false

   });

}



complete(id: number) {

   this.todos = this.todos.map(

       todo => todo.id == id ? ({ ...toodo, completed: !todo.completed }) : todo

   );

}

private getNextId(): Number {

   return !thistodos.length ? 1 : Math.max(...this.todos.map(({ id }) => id)) + 1;

}

}

```



새로운 할일을 추가하는 add 버튼을 클릭하면 add 이벤트 핸들러가 동작하고 todos 프로퍼티에 새로운 todo 객체를 push한다.

이때 변화 감지에 의해 todos 프로퍼티의 상태가 템플릿으로 업데이트 된다.



이제 todo list 출력 개수를 제한하는 limit 파이프를 작성해보겠다.



```

$ ng generate pipe limit

```



생성된 파이프를 다음과 같이 수정한다.



```

// limit.pipe.ts

import { Pipe, PipeTransform } from '@angular/core';

import { Todo } from './todos.component';



@Pipe({

   name: 'limit'

})

export class LimitPipe implements PipeTransform {

   transform(todos: Todo[], limit: number): Todo[] {

       return todos.filter((el, i) => i < limit);

   }

}

```



컴포넌트에 limit 파이프를 적용한다.

그리고 변화 감지가 작동하도록 todo 프로퍼티의 참조가 변경되도록 코드를 수정한다.



```

// todos.component.ts

...

<li *ngFor="let todo of (todos | limit: 5)"

   (click)="complete(todo.id)"

   [class.completed]="todo.completed">{{ todo.completed }}</li>

...

add(content: string) {

   /*

       push 메소드는 원본 배열을 직접 변경하지만, 원본 배열의 참조는 변경되지 않기 때문에 파이프에 의해 변화 감지가 되지 않는다.

   */

   //this.todos.push({ id: this.getNextId(), content, completed: false });



   // 파이프에 의해 변화 감지가 작동하도록 todos 프로퍼티의 참조가 변경되도록 수정한다.

   this.todos = [...this.todos, { id: this.getNextId(), content, completed: false }];

}



```
