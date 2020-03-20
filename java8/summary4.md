# 기술면접준비 4


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

OUTPUT: Member 타입 입니다. 
        Version 타입 입니다


