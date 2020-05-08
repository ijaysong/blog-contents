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

## `Path 인터페이스`  
C://job/readme.txt라는 파일 패스가 있다고 가정하자.  
windows에선  C:\\job\readme.txt 이렇게 표현된다. (슬래시 -> 백슬래시)  
Java의 Path인터페이스가 슬래시 -> 백슬래시로 변환처리를 해주기 때문에 슬래시로 표현해도 가능하다.  
그러나, Mac이나 Linux에선 백슬래시로 입력하면 인식을 못하기 때문에 슬래시로만 표현이 가능하다.  

## `Current Directory`  
프로그램 기동 시, 액세스하고 있는 디렉토리  
자바 프로그램에서는 java 커맨드를 실행 시 접근하고 있는 디렉토리가 이에 해당한다.  
Eclipse에서 자바 프로그램 실행 시의 커런트 디렉토리는 프로젝트 폴더(프로젝트가 있는 디렉토리)가 된다.  

##  `절대패스`와 `상대패스`  
절대패스 : 루트로부터 완전한 경로를 기술한 것 C:\\job\docs\readme.txt  
상대패스 : 커런트 디렉토리를 기점으로 경로를 기술한 것  
		    job이 커런트 디렉토리라면, \docs\readme.txt  

## `입출력 스트림 (I/O Stream)`  
입력 : 파일로부터 데이터를 읽어들임  
출력 : 파일에 데이터를 써서 내보냄  
스트림 : 오브젝트를 통해서 데이터가 1바이트씩 흘러가는 모양새로부터 이름이 붙여짐  
입출력 대상: 파일, 네트워크, 문자열 변수, 키보드 입력등..  

## `텍스트 스트림`과 `바이너리 스트림`
텍스트 스트림 : 문자를 다룸  
   	         한 문자 단위로 입출력한다.  
             바이트 배열에서 문자열로의 변환이 필요하다.  
             Reader, Writer  
바이너리 스트림 : 음성이나 화상(그림, 이미지) 등 이외의 것을 다룸  
	            데이터에 손을 대지 않고 그대로 처리함.  
              0과 1의 배열을 1바이트 단위( = 1비트 8개)로 입출력한다.  
              01010101|01010101|01010101...  
			        InputStream, OutputStream  

## `Buffered 스트림`
BufferedInputStream, BufferedOutputStream, BufferedReader, BufferedWriter  
Buffered란 파일로부터 일정량의 데이터를 먼저 읽어들이거나, 먼저 출력해 메모리에 모아두는 기능을 말한다.   
매회 기억장치에 액세스하는 것보다 빠른 속도로 입출력할 수 있다.  

## `Buffered Reader의 사용법`
~~~
FileReader fr = new FileReader(“readme.txt”);
BufferedReader br = new BufferedReader(fr);
~~~
BufferedReader는 입력 버퍼 기능(입력한 데이터를 버퍼에 올려두고 빠르게 읽어들이는 기능)을 가지지만, 입력 기능을 가지고 있지 않기 때문에 단독으로 사용하지 않는다.   
반대로, 다른 텍스트 입력 스트림은 버퍼 기능을 가지고 있지 않기 때문에 속도가 느리다.  
속도를 높이기 위해서 BufferedReader로 Wrapping해 사용하는 것이 최선이다.  

## `Resource가 붙어있는 try-catch문`
<일반적인 try-catch문>
~~~
BufferedReader in = null;

try {
	in = Files.newBufferedReader(path); // 예외가 발생할 가능성이 있음
} catch (IOException e) {
	e.printStackTrace();  // 예외처리
} finally {
	if(in == null) {
		try {
			in.close();  // 예외가 발생할 가능성이 있음
		} catch (IOException e) {
			e.printStackTrace();  // 예외처리
		}
	}
}
~~~
I/O 스트림의 특징은, 처리가 끝난 후, 작업용 메모리를 닫아주는 종료처리가 필요하다.  => close() 메소드  
예외 발생 유무에 상관 없이, 반드시 실행하지 않으면 안되기 때문에 finally에서 실행해주었다.  
기존의 try-catch문도 좋지만 길이가 길다는 단점이 있고, Java7(2011년)부터 리소스가 붙어있는 try-catch문이 도입되었기 때문에 close() 메소드를 쓸 필요가 없다.  

<리소스가 붙어있는 try-catch문>
~~~
try(BufferedReader in = Files.newBufferedReader(path);) { // ()안에서 작성한다
	...
} catch (IOException e) {
	e.printStackTrace();  // 예외처리
}
~~~

()가 붙어있는 try 문을 ARM(Automatic Resource Management) 블록이라고도 부른다.  
() 안에 쓰여져있는 I/O 스트림은 종료시에 자동적으로 close() 메소드가 실행된다. => finall에서 close() 메소드를 실행시킬 필요가 없다.  

## `ObjectInputStream`과 `ObjectOutputStream`
바이너리 스트림의 하나로서, 오브젝트를 파일에 저장하거나, 파일로부터 읽어들인다.  
해당 I/O스트림은 오브젝트를 조작하는 기능은 있지만 읽고 쓰는 기능과 버퍼 기능을 가지고 있지 않기 때문에 다른 I/O스트림을 Wrapping해서 사용한다.  
~~~
ObjectOutputStream out = new ObjectOutputStream(new BufferedOutputStream(new FileOutputStream(“/readme.txt”)));
~~~

## `Serializable 인터페이스`
Serializable를 implements 함으로서 자신이 만든 클래스 Object를 파일로 저장할 수 있다.  
어떤 값을 읽고 쓰는 클래스는 전부 Serializable이 적용되어 있다.  
단순히 마크에 지나지 않으므로 마크 인터페이스라고도 한다.  

~~~
public class MyObject implement Serializable {
	private static final long serialVersionUID = 10L; // 버전 번호

	private static int counter; // 저장되지 않음(인스턴스에 포함되지 않음)
	private double value; // primitive 타입은 저장됨
	private LocalDate date; // Serializable가 적용돼 있으므로 저장됨
	private YourObject obj; // Serializable가 적용돼 있다면, 저장됨
	private transient Foo flag; // 저장안됨(저장 대상으로부터 제외됨)
...
}
~~~

static이 붙어있는 필드변수는 인스턴스에 포함되지 않으므로 저장되지 않는다.  
필드변수에 transient를 붙이면, 저장 대상으로부터 제외한다.  
필드변수에 오브젝트가 포함되어있는 경우, 해당 오브젝트에 Serializable가 적용돼 있어 있어야 한다.  
이것처럼 해당 오브젝트 뿐만 아니라 관련된 오브젝트까지 포함해서 하나의 바이너리 데이터로 변환하는 것을 Serialize라고 한다.  
반대로, 바이너리 데이터로부터 해당 오브젝트와 관련된 오브젝트까지 원래의 형태로 복원시키는 것을  Deserialize라고 한다.  
