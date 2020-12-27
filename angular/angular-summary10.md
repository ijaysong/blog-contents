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
