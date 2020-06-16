# 자바 내용 정리 4


## `추상클래스`란?
오버라이드 하고자 하는 메소드를 가지는 클래스를 말한다.  
클래스 선언에 abstract를 붙인 클래스이다.  
보통의 클래스에서 추상클래스를 오버라이드 하면 컴파일 에러가 나기 때문에, 서브클래스에서 깜빡잊고 오버라이드 안하는 것을 방지하는 역할을 한다.  
new 연산자를 사용해 인스턴스를 만드는 것이 불가능하다.   
컨스트럭터는 protected를 붙여 만든다.  
부모클래스에서 자식클래스로 상속 받았을 때, 상속 받은 부모 클래스를 초기화할 때 이외에는 사용하지 않으므로 protected를 붙인다.  
추상 클래스에 추상 메소드는 필수가 아니다.  일반 메소드도 쓸 수 있다.  
추상 클래스의 서브클래스로 추상클래스로 사용하지 않아도 된다.  
일반 클래스의 서브클래스로 추상클래스를 쓸 수 있다.

## `추상메소드`란?
abstract를 붙인 메소드이다.  
추상메소드는 추상클래스에서만 사용할 수 있다.  
추상메소드는 선언만 하고, 메소드 처리 내용을 작성하지 않는다. ({} 안쪽부분.)
~~~
public abstract class Foo {  // 추상 클래스의 선언
	private String name;

	protected Foo(String name) { // 컨스트럭터
		this.name = name;
	}	

	public abstract void show(); // 추상메소드의 선언
	
	public void setName(String name) { // 일반 메소드
		this.name = name;
	}
}
~~~

## `인터페이스`란?
추상클래스와 닮아 있지만, abstract class의 대신에 interface를 쓴다.  
접근제한자는 public (패키지 액세스 가능) 으로, private과 protected는 사용할 수 없다.  
당연하지만, 클래스가 아니므로 new 연산자를 사용해서 인스턴스를 생성할 수 없다.  
추상메소드를 정의한다.  
인터페이스의 추상메소드는 항상 public abstract이므로 접근제한자 기입을 생략한다.  
클래스에 같은 인터페이스를 지정해놓으면 오버라이드한 메소드의 움직임이 다 다르다. 다형성(폴리모피즘)의 한 예이다.

~~~
Public interface Version { // Version의 인터페이스
	String getVersion(); // 버전의 문자열을 리턴하는 추상메소드
}
~~~

클래스 선언에 `implements  인터페이스 명`을 지정해 구현할 수 있다.  
반드시 public을 붙여서 추상 메소드를 상속할 수 있도록 한다.

~~~
Public class Member implements Version {
	public String getVersion() {
		return “Member Class version 1.0”;
	}
}
~~~

인터페이스를 적용하면서 동시에 상속할 수도 있다.  
2개의 인터페이스를 지정할 수도 있다.

~~~
Public class Bar extends Foo implements Version, Visible {
	…
}
~~~

인터페이스를 적용하면 본래 클래스 형 타입과 동시에 인터페이스 형 타입을 가지게 된다.  
같은 인터페이스를 적용한 클래스들은 해당 인터페이스 형 타입을 모두 가지게 되므로, 공통의 형 타입을 가진다는 이점이 있다.  
인터페이스 타입으로 대체 가능하므로 확장성이 넓어진다.  
예를 들어,   
Member 클래스가Version 인터페이스를 사용한다면, 아래와 같이 Version 인터페이스 타입에 대입할 수 있다.

~~~
Version ver = mem;
~~~

~~~
Public class CheckType {
	public static void main(string[] args) {
		Member mem = new Member();
		if(mem instanced Member) {
			System.out.println(“Member 타입 입니다”);
		}
		if(mem instanceof Version) {
			System.out.println(“Version 타입 입니다”);
		}
	}
}
~~~

OUTPUT: Member 타입 입니다  
        Version 타입 입니다

동일한 인터페이스를 적용해도 클래스별로 오버라이드한 메소드의 움직임(기능)이 다르기 때문에 `다형성`이 구현 된다.

~~~
class Foo implements Version {
	@Override
	public String getVersion() {
		return "Foo 클래스";
	}
}

class Bar implements Version {
	@Override
	public STring getVersion() {
		return "Bar 클래스";
	}
}

public class Polymorphism {
	public static void main(String[] args) {
		Foo foo = new Foo();
		Bar bar = new Bar();
		display(foo);
		display(bar);
	}
	
	public static void display(Version ver) {
		System.out.println(ver.getVersion());
	}
}
~~~

OUTPUT: Foo 클래스  
        Bar 클래스

인터페이스끼리의 상속이 가능하다.  
클래스끼리의 상속처럼 복잡하지 않으며, 같은 이름의 메소드가 중복 상속되면 하나로 정리되는 정도이다.

~~~
interface A {
	void talk();
}

interface B {
	void hello();
}

interface C extends A, B {
	void bye();
}

class X implements C {
	@Override
	public void talk() {
		System.out.println("talk");
	}
	
	@Override
	public void hello(){
		System.out.println("hello");
	}
	
	@Override
	public void bye() {
		System.out.println("bye");
	}
}
~~~

## `예외`란?
여러 원인으로 실행중인 프로그램이 정지해버리는 상황을 `예외가 발생`했다고 한다.  
에러 발생시, 호출된 곳에 에러를 통지하는 것을 `예러 처리`한다고 한다.

## `throw문`이란?
에러를 해결할 수 없는 상황에, 에러정보를 가진 오브젝트를 호출된 곳의 메소드에 보내서 에러 처리를 맡기는 방법이다.  
throw문은 return문처럼 움직인다. 다만, 메소드의 리턴타입에 상관 없이 예외만을 가지고 리턴한다는 것이다.  
`throw new 예외 클래스()`  
`throw new 예외 클래스("임의의 에러메세지");`

~~~
public static int div(int a, int b) {
	if(b == 0) {
		throw new ArithmeticException(); // 호출된 곳으로 예외처리를 맡김
	}
	return a/b;
}
~~~

## `try catch문`란?
호출할 메소드가 예외발생 가능성이 있을 경우, try-catch문을 적어 그 안에서 해당 메소드를 부르도록 한다.

~~~
try { // try 블럭
	// 예외가 발생할지도 모르는 처리
	// 그 외, 관련 처리
	
} catch(예외타입 변수) { // catch 블럭
	// 예외에 대응하는 처리
}
~~~

~~~
public static void main(String[] args) {
	int a = 10;
	int b = 0;
	
	try {
		int ans = div(a, b); // 예외가 발생할 가능성이 있는 메소드를 호출함
		System.out.println(a + "/" + b + "=" + ans); // 예외 발생시, 해당 처리는 스킵되어 실행되지 않음
		
	} catch(ArithmeticException e) {
		System.out.println("0으로 나눠지지 않습니다."); // 예외 처리
	}
}

~~~

## `예외의 종류`
1. 시스템 에러  
	회복불가능한 치명적 에러  
	메모리 부족이나, 프로그램 버그 등이 원인  
	에러 발생시, 프로그램을 종료하는 것 밖에 안됨.  
	프로그램에서 예외처리를 하지 않음.  
	
1. 체크 에러
	일반적으로 예외라고 한다면 체크 에러를 가리킨다.  
	반드시 try catch문을 사용해서 예외처리를 한다.(컴파일러가 예외처리를 작성하고 있는지 체크하기 떄문에, 작성하지 않으면 컴파일러 에러가 난다.)  
	
1. 실행시 에러(비체크 에러)  
	주로 JVM이 던지는 예외로, 표준 클래스의 메소드가 던질 때도 있다.  
	프로그램 실행 중, 오류를 감지했을 때 발생한다.  
	범위 외 배열번호를 사용했거나, 액세스한 변수가 null이거나 프로그램 로직상의 미스가 원인  


어플리케이션 고유의 예외처리를 만들고 싶은 경우에는 예외 클래스를 계승해서 새로운 것을 만들 수도 있다.

