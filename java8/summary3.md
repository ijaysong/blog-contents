# IT 기술면접 준비3


## `형변환`이란?  
형변환의 대상이은 오브젝트가 아니라 오브젝트의 참조값이다.  
부모 클래스로부터 상속받은 부분만 쓰고, 자식 클래스에서 확장한 부분을 사용하지 않으면 자식 클래스의 인스턴스를 부모 클래스의 인스턴스로 사용하는 것이 가능하다.  
이 경우, 인스턴스 변수의 참조값은 부모 클래스 참조값을 가리킨다. (오브젝트 자체는 아무것도 변하지 않는다)

~~~
StudentMember stmem = new StudentMember(100, 'hongkd');   // 인스턴스를 만듦
Member mem = stmem;                                       // 부모클래스형 ← 자식클래스형
~~~

## `업캐스팅(Upcasting)`이란?  
자식 클래스에서 부모 클래스로 형변환 하는 것.  
상기 내용에서의 형변환이 이에 해당한다.  

## `다운캐스팅(Downcasting)`이란?  
부모 클래스에서 자식클래스로 형변환 하는 것.  
형변환이 안된다.  
자식클래스에서 추가한 변수나 클래스가 부모클래스에는 없기때문에 에러가 나는 것.  
캐스팅연산자를 사용해서 강제형변환 할수도 있다.  

~~~
StudentMember stmem = new Member(100, 'hongkd');   // 컴파일 에러 발생
StudentMember stmem = (StudentMember) mem;         // 강제형변환이 가능하다
~~~

## `instanceof 연산자`란?
변수의 실제 타입이 지정한 형타입인지 아닌지 확인하는 연산자로 `변수 instanceof 형타입`으로 표현한다.  
형타입이 일치한다면 true를 반환하고, 아닐경우에는 false를 반환한다.  
* true  : 타입 일치 / 혹은 우변의 클래스가 부모클래스일 경우
* false : 타입 불일치 / 혹은 우변의 클래스가 자식클래스일 경우

~~~
mem instanceof StudentMember // mem는 StudenMember형인가?
~~~

if문으로 아래처럼 사용하는 것이 일반적이다.
~~~
if(mem instanceof StudentMember) {             // 체크해서
	StudentMember stmem = (StudentMember) mem; // 형변환 한다
}
~~~


## `오버로딩(Overloading)`이란?
`클래스 안에 같은 이름의 메소드를 여러개 만드는 것.`  
인수의 구성을 바꿈으로서 같은 이름이지만 다른 기능의 메소드를 추가한다.  
부모클래스에서 상속 받은 메소드와 같은 이름의 메소드를 만드는 것도 가능하다. (인수 구성의 변화가 필요함)  
* `인수 구성의 변화`란 : 인수의 타입, 수, 나열 중 어느 것 하나

~~~
public void add() {  // 원래부터 있었던 메소드
	number++;        // number를 1 늘림
}

public void add(int val) {  // 오버로딩한 add 메소드
	number += val;          // number에 인수 val를 더함
}
~~~

## `오버라이딩(OverRiding)`이란?
부모 클래스로부터 상속받은 메소드의 기능을 바꾸는 것.  
오버로드와 달리, 메소드 명, 리턴 타입, 접근제한자, 인수 구성등이 변해선 안된다.  
완전히 일치해야 됨.  
메소드 내용만 달라짐.  

~~~
class Foo {                                       // 부모클래스
	public void show() {                          // 원래 있던 show 메소드
		System.out.println("Foo클래스 입니다.");
	}
}

class Bar extends Foo {                           // 서브클래스
	@Override
	public void show() {                          // 오버라이드한 show 메소드
		System.out.println("Bar클래스 입니다.");
	}
}
~~~

⇒ 출력 : Bar클래스 입니다.

**※예외**
* 접근제한자: 공개 범위가 넓어지는 것이라면 변경가능함. (public > protected > 패키지접근 > private)
* 리턴 타입: 오브젝트 타입을 리턴한다면, 같은 타입이거나 자식클래스타입으로 변경가능함.


## `다이나믹바인딩(Dynamic Binding)`이란?
오버라이딩으로 인해, `인스턴스 안에 같은 시그니쳐(메소드명, 인구구성)를 가지는 메소드가 있을 경우, 어떤 메소드를 실행시킬 것인가를 실행시 결정하는 구조`를 말한다.  
자식 클래스에서 부모클래스 방향을 향해서 같은 메소드가 있나 검색해, 가장 처음에 발견한 메소드를 실행한다.  
항상 마지막에 오버라이드 된 메소드가 실행된다.  


## `어노테이션(annotation)`이란?
주석이라는 의미로, Java에서는 컴파일러에게 어노테이션을 전달해 무언가를 시키는데 사용한다.  


## `@override 어노테이션`이란?
오버라이딩한 것으로서 옳은지 아닌지 컴파일러에게 체크하도록 시키는 것.  


## `다형성(Polymorphism)`이란?★★★
자식클래스의 인스턴스를 부모클래스 타입의 변수에 대입하면, 오버라이딩된 메소드는 부모클래스에서 정의된 메소드와 다른 움직임을 가진다.  
즉, 오버라이딩에 의해서 부모클래스의 기능이 변경된 것이다.  
만약에 자식클래스가 1개가 아니라 여러개라면, `어떤 자식클래스를 사용하는지에 따라서, 부모클래스의 기능을 바꾸는 것`이 가능하다.  
이것이 다향성이라고 불리는 오브젝트 지향의 가장 큰 특징이다.  

~~~
class Foo {
	public void show() {
	}
}
class Bar extends Foo {
	@Override
	public void show() {
		System.out.println("★Bar클래스입니다.");
	}
}
class Baz extends Foo {
	@Override
	public void show() {
		System.out.println("☆Baz클래스입니다.");
	}
}
public class PolymorphismDemo {
	public static void main(String[] args) {
		Foo foo = new Bar();  // Bar 클래스의 인스턴스를 사용
		foo.show();
		foo = new Baz();      // Baz 클래스의 인스턴스를 사용
		foo.show();
	}
}
~~~

⇒ 출력 : ★Bar클래스입니다.
          ☆Baz클래스입니다.

자식 클래스를 바꿔가며 다형성을 확장시켜주는 범용 메소드도 구현할 수 있다.
~~~
public class Polymorphism {
	public static void main(String[] args) {
		Bar bar = new Bar();
		Baz baz = new Baz();
		useAny(bar);
		useAny(baz);
	}
	pubilc static void useAny(Foo foo) {
		foo.show();
	}
}
~~~

⇒ 출력 : ★Bar클래스입니다.
          ☆Baz클래스입니다.

다형성의 대표적인 예로 println(Object o)메소드가 있다.  
`println메소드`는 출력하려는 데이터의 타입에 따라서 오버라이딩 되어진다.  
Object 클래스는 모든 클래스의 부모 클래스이므로 어떤 클래스의 인스턴스라도 `println메소드`에서 출력된다.  


## `오브젝트 지향의 3대요소`란?★★★
* 캡슐화 : 여러 데이터를 한데 모아 관리하며, 공개를 제한함.
* 다형성 : 커스터마이즈가 용이하고, 재이용가능한 시스템 구축.
* 상속 : 오브젝트의 계열을 만드는 관계 구축.
