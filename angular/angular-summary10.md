## 10. 생명주기와 훅 메소드



### 10.1. 생명주기



컴포넌트와 디렉티브는 생명주기를 갖는다.

생명주기란 컴포넌트와 디렉티브가 생성하고 소멸되기까지의 여러 과정을 말하며, Angular에 의해 관리된다.

다시 말해 Angular는 생명주기를 통해 컴포넌트와 디렉티브를 생성하고, 렌더링하며, 프로퍼티의 변화를 체크하고 DOM에서 제거하는 일련의 과정을 관리한다.

개발자는 Angular가 제공하는 생명주기 훅 메소드를 구현하여 생명주기 단계에서 처리하여야 행위를 정의할 수 있다.

Angualr는 다음과 같은 순서(생명주기 시퀀스)대로 생명주기를 관리하고 생명주기 이름 앞에 ng가 붙은 생명주기 훅 메소드를 제공한다.



constructor

ngOnChanges

ngOnInit

ngDoCheck



> ngAfterContentInit

> ngAfterContentChecked

> ngAfterViewInit

> ngAfterViewChecked

> ngOnDestroy



### 10.2. 생명주기 훅 메소드



생명주기 훅 메소드는 인터페이의 형태로 제공된다.

예를 들어 OnInit 생명주기에 처리되어야 할 행위를 정의하기 위해서는 훅 메소드 ngOnInit을 구현한다.



이와 같이 생명주기(OnInit)에는 동일한 이름의 인터페이스(OnInit)이 존재한다.

그리고 인터페이스는 생명주기 이름 앞에 ng 접두어가 붙은 추상 메소드(ngOnInit)을 포함한다.

생명주기에 처리되어야 할 행위를 처리하려면 생명주기 인터페이스의 추상 메소드를 구현한다.



```

import { Component, OnInit } from '@angular/core';

...

export class AppComponent implements OnInit {

   name = 'Lee'



   constructure() {  }



   // 생명주기 OnInit 단계에서 실행할 처리를 구현한다.

   ngOnInit() {...}

}

```



컴포넌트와 디렉티브는 클래스이므로 constructor의 호출에 의해 생성된다.

그 이후, Angular는 특별한 시점에 구현된 생명주기 훅 메소드를 호출한다.

모든 생명주기 훅 메소드를 구현할 필요는 없으며, 특정 생명주기에 처리해야 할 행위가 있을 때, 필요한 생명주기 훅 메소드만 구현하면 된다.

#### 10.2.1. ngOnChanges



부모 컴포넌트에서 자식 컴포넌트의 입력 프로퍼티(@Input 데코레이터로 장식된 프로퍼티)로 바인딩한 값이 초기화 또는 변경되었을 때 실행된다.

따라서 컴포넌트에 입력 프로퍼티가 없을 때는 호출할 필요가 없다.



```

class MyComponent implements OnChanges {

   @Input() prop1: number;

   @Input() prop2: string;



   ngOnChanges(changes: SimpleChanges) {

       // changes는 모든 입력 프로퍼티의 이전 값과 현재 값을 포함한다.

       concole.log(changes);

   }

}

```



ngOnChanges는 ngOnInit 이전에 입력 프로퍼티가 존재하는 경우, 최소 1회 호출된다.

이후에는 입력 프로퍼티가 변경될 때마다 호출된다.

이때의 변경은 입력 프로퍼티의 참조 변경을 말한다.

다시말해 `기본 자료형의 값이 재할당되었을 때와 객체의 참조가 변경되었을 때만 반응한다.`

입력 프로퍼티의 참조 변경에만 반응하므로 입력 프로퍼티가 아닌 일반 컴포넌트 프로퍼티의 내용이 변경되었을 때는 반응하지 않는다.



#### 10.2.2. ngOnInit



ngOnChanges 이후, 입력 프로퍼티를 포함한 모든 프로퍼티의 초기화가 왼료된 시점에 한번만 호출된다.TypeScript에서는 constructor에서 프로퍼티를 초기화하는 것이 일반적이지만, Angular에서 프로퍼티의 초기화 처리는 constructor가 아닌 ngOnInit에서 수행하는 것이 좋다.

(간단한 값으로 프로퍼티를 초기화하는 것은 문제가 되지 않지만, 서버에서 데이터를 가져와 할당하는 것과 같이 복잡한 처리는 constructor가 아닌 ngOnInit에서 수행해야 한다.)



#### 10.2.3. ngDoCheck



ngOnInit 이후, 컴포넌트 또는 디렉티브의 모든 상태 변화가 발생할 때마다 호출된다.

다시 말해 변화 감지 로직이 실행될 때 호출된다.



Angualar는 컴포넌트 클래스의 프로퍼티 값이 변경되는 상황, 즉 DOM 이벤트, Timer 함수의 tick 이벤트, Ajax 통신 등과 같은 비동기 처리가 수행 될 때, 변화 감지 로직을 실행한다. 바로 이때 호출되는 훅 메소드가 ngDoCheck 이다.



ngDoCheck는 Angular의 변화 감지에 의해 감지되지 않거나 감지할 수 없는 변경 사항을 수동으로 더티 체크 하기 위해 사용한다.

커스텀 더티 체크를 통해 사용자 변화 감지 로직을 구현하기 위해서는 Angualr가 제공하는 KeyValueDiffers와 IterableDiffers를 사용한다.



ngDoCheck는 모든 상태 변화가 발생할 때마다 매번 호출되기 때문에 성능에 악영향을 줄 수 있다.

가장 바람직한 것은 Angular의 변화 감지가 상태 변화를 감지하도록 코드를 구현하는 것이지만, ngDoCheck를 사용할 수 밖에 없는 상황이라면 최대한 가벼운 처리로 성능에 무리를 주지 않도록 해야한다.



ngOnChanges는 입력 프로퍼티에 바인딩된 값이 초기화 또는 변경되었을 때만 반응하여 호출되지만, ngDoCheck는 모든 상태의 변경에 의해 호출된다.

#### 10.2.4. ngAfterContentIint



ngContent 디렉티브를 사용하여 외부 컨텐츠를 컴포넌트의 뷰에 콘텐츠 프로젝션한 이후 호출된다.

첫번째 ngDoCheck 호출 이후에 한번만 호출되며 컴포넌트에서만 동작하는 컴포넌트 전용 훅 메소드이다.



#### 10.2.5. ngAfterContentChecked



콘텐츠 프로덕션에 의해 부모 컴포넌트가 전달한 부모 컴포넌트의 템플릿 조각을 체크한 후 호출된다,

ngAfterContentInit 호출 이후, ngDoCheck가 호출된 이후에 호출되며 컴포넌트에서만 동작하는 컴포넌트 전용 훅 메소드이다.



#### 10.2.6. ngAfterViewLint



컴포넌트의 뷰와 자식 컴포넌트의 뷰를 초기화한 이후 호출된다.

첫번째 ngAfterContentChecked 호출 이후 한 번만 호출되며 컴포넌트에서만 동작하는 컴포넌트 전용 훅 메소드이다.



#### 10.2.7. ngAfterViewChecked



컴포넌트의 뷰와 자식 컴포넌트의 뷰를 체크한 이후 호출된다.

첫번째 ngAfterViewInit 호출 이후, ngAfterContentChecked 호출 이후 호출되며 컴포넌트에서만 동작하는 컴포넌트 전용 훅 메소드이다.



#### 10.2.8. ngOnDestroy



컴포넌트와 디렉티브가 소멸하기 이전에 호출된다.

RxJS의 unsubscribe 등 메모리 누수를 방지하기 위한 코드 등을 정의한다.

