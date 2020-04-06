# 기술면접준비 5


## `예외를 처리하는 방법`
첫번째, 실행시 예외를 처리하던가, 두번째, 체크 예외를 처리하는 방법이 있다.

첫번째 방법은 매우 간단해서 `throw`문으로 예외를 작성하는 것 뿐이다.
~~~
public static void int div(int a, int b) {
	if(b == 0) {
		throw new ArithmeticException(); // 예외처리를 던진다!
	}
	return a/b;
}

~~~
두번째, 체크 예외를 처리하기 위해선, `throws 선언`이 필요하다.  
throws 선언을 반드시 해주어야 한다.(선언 안하면, 컴파일 에러남)  
throws에 컴마로 여러개를 지정할 수 있다.

~~~
// 입출력 처리에 관한 예외를 던진다
public int foo() throws IOException {
	...
}

// 입출력과 데이터베이스처리에 대한 예외를 던지는 메소드
public void bar(String s) throws IOException, SQLException {
	if(...) throws new IOException();
	if(...) throws new SQLException();
}
~~~


## `예외 컨스트럭터와 메소드`
예외는 `오브젝트`이므로, 예외 클래스로부터 인스턴스를 만들어 사용한다.  
예외 클래스의 구성도 일반 클래스와 똑같이 컨스트럭터와 메소드가 있다.  
예외 클래스는 어떤 것이든 전부 같은 형식의 컨스트럭터를 가진다.  

컨스트럭터               |설명                                           
-------------------------|-----------------------------------------------
Exception()              |인수가 없는 컨스트럭터                         
Exception(String message)|예외를 설명하는 문자열을 인수로 받는 컨스트럭터

예외 클래스에서 자주 사용되는 클래스 3개이다.  
예외처리에 사용 가능하며, 모든 예외 클래스의 공통 메소드이다.  
왜냐하면, 모든 예외 클래스의 부모클래스인 Throwable클래스로부터 계승한 메소드이기 떄문이다.  
어떤 예외 클래스도 독자적인 메소드를 정의하지 않고, 모두 Throwable클래스로부터 계승받고 있다.  

메소드                   |설명                                           
-------------------------|-----------------------------------------------
toString()               |에러명과 에러 메세지 문자열을 반환한다
printStackTrace()        |에러 내용과 메소드 호출, 그 결과를 실행순으로 표시한다
getMessage()             |에러 메세지 문자열을 반환한다


에러 메세지를 인수로 받는 컨스트럭터의 예시이다.
~~~
public calss ExceptionMessage {
	public static void main(String[] args) {
		try{
			method();
		} catch (Exception e) {
			System.out.println(e.getMessage()); // 예외 메세지를 표시
		}
	}
	
	public static void method() throws Exception {
		throw new Exception("예외가 발생했습니다"); // 메세지가 붙은 예외를 던짐
	}
}
~~~
OUTPUT : 예외가 발생했습니다

체크예외를 던졌기 때문에 `throws`선언을 하고 있다.  
getMessage()메소드로는 에러 메세지를 취득해 표시하고 있다.  
예외를 던질때 에러 메세지를 같이 붙여서 보내면 원인을 알기 쉬워진다.  
