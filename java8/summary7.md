# IT 기술면접 준비7

## `람다식이란?`
람다식이란 익명 클래스에서 불필요한 정보를 삭제해 놓은 것과 같은 것이다.  
람다식은 함수형 인터페이스의 추상 메소드를 오버라이드해서 그 인스턴스를 반환한다.  
람다식에는 추상 메소드의 인수와 오버라이드 부분만 쓰여진다.

## `함수형 인터페이스`
람다식을 사용하기 위해선 인터페이스가 추상 메소드를 하나만 가져야 한다는 전제가 있다.   
추상 메소드가 하나밖에 없는 인터페이스를 함수형 인터페이스라고 한다.  
인터페이스 타입의 인수를 가지는 메소드에서 그것이 함수형 인터페이스라면, 인수에 람다식을 반환하는 것이 가능하다.

## `함수형 인터페이스의 종류`
* Predice : True 혹은 False를 판정결과로 반환한다 (test)
* Consumer : 넘겨받은 인수를 사용해서 무엇인가를 처리하고, 값을 반환하지 않는다 (accept)
* Supplier : 인수는 없지만, 무엇인가 값을 작성해서 반환한다 (get)
* Function : 인수를 다른 타입 값을 변환해서 반환한다 (apply)
* UnaryOperator : 인수와 같은 타입의 값을 반환한다 (apply)
* Bi~ : 처리는 같지만, 인수는 2개가 있다

## `람다식을 사용하는 이유`
인터페이스 타입의 인수를 가지는 메소드는 인수가 바뀌면 동작도 바뀌는 특징이 있다.   
다양한 람다식을 지정해, 메소드 동작을 바꾸는 것이 가능하다.  
인터페이스의 다형성! 덕분이다.  
다형성은 Java가 가지는 본질적인 기능이지만 람다식 덕분에 더 간편하게 사용할 수 있게 되었다.                                                         

## `람다식을 사용하는 장소`
람다식의 실체는 인스턴스이기 때문에 변수에 대입하는 것도 가능하지만, 대체로 메소드의 인수로서 사용된다.

~~~
import java.time.LocalDate;
import java.util.Array;
import java.util.List;

// 인터페이스
interface Predicate {
   boolean test(Book book);
}

public class MyList {
   public static void main(String[] args) {
      List<Book> list = Arrays.asList(
         new Book(120, “람다식을 배워보자 A”),
         new Book(121, “람다식을 배워보자 B”),
         new Book(122, “람다식을 배워보자 C”),
         new Book(123, “람다식을 배워보자 D”)
      );

      listup(list, book -> book.getBookNumber() <= 121); // 책 번호가 121 이하인 것
   }

   // listup 처리
   public static void listup(List<Book> list, Predicate p) {
      for(Book book : list) {
         if(p.test(book)) { // 인터페이스의 메소드를 실행해 판정한다. 람다식의 -> 우변이 실행됨
            System.out.println(book); // 출력
         }
      }
   }
}
~~~
OUTPUT : Book [ bookNumber=120, title=람다식을 배워보자 A ]  
Book [ bookNumber=121, title=람다식을 배워보자 B ]

## `람다식 쓰는 법`
`( 인수 ) -> 식` 혹은 `( 인수 ) -> { 식; }`의 형식.  
* `;`를 안붙이는 경우 : 변수, 연산자, 메소드 호출
* `;`를 붙이는 경우 : 대입식, 메소드 호출, 오브젝트 작성식
~~~
(a, b) -> a+b                  // 인수와 식. 식에는 ;를 붙이지 않는다 
(String s) -> s.length()   // 인수에 타입을 지정해도 괜찮지만 ()가 필요하다
s -> s.length()                // 인수가 하나라면 ()는 생략 가능
~~~

인수가 하나라면, ()를 생략할 수 있다.  
(Book book, String s) 처럼 인수에 타입을 지정하거나, (book, s) 처럼 타입을 지정하지 않을 수도 있다.  
함수기술자는 람다식의 인수와 반환값의 타입을 나타낸다.

## `메소드 참조`
람다식에서 하나의 메소드만 호출하는 것은 메소드 참조로 표현하는 것도 가능하다.  
메소드 참조는 `클래스 명 :: 메소드 명`으로 메소드 명에 ()를 붙이지 않는다.  
외부 인스턴스 변수의 메소드를 사용하는 경우에만 `인스턴스 변수명 :: 메소드 명`으로 지정한다.  
컨스트럭터도 `클래스 명 :: new `의 형식으로 사용하는 것이 가능하다.

## 람다식의 편리한 사용방법
인터페이스의 static 메소드를 사용할 때, static 임포트 해두면 작성이 간단해진다.  
~~~
import static java.util.function.Comparator.comparing;
~~~

Predicate 인터페이스의 default 메소드를 사용하면, 조건을 맞춰서 사용할 수 있다.  
조건은 왼쪽에서부터 차례로 해석된다.
~~~
listup(list, min5000.negate()); // min5000이 아님
listup(list, min5000.and(korean).or(english));
~~~

comparing을 사용하면 정렬이 간단해진다.
~~~
list.sort(comparing( Book :: getPrice )); // 가격순으로 정렬
list.sort(comparing( Book :: getLanguage )); // 사용언어순으로 정렬
~~~

thenComparing은 sort의 2차 키를 지정할 수 있다.
~~~
list.sort( comparing( Book :: getPrice ) ) // 가격순으로 정렬
.thenComparing( Book :: getCode )); // 가격이 같다면 등록번호 순으로 정렬
~~~

reversed는 역순으로 정렬한다.
~~~
list.sort( comparing( Book :: getPrice ) // 가격순으로 정렬
.thencomparing( Book :: getCode ) // 가격이 같으면 등록 번호 순으로 정렬
.reversed() ); // 역순으로 정렬
~~~
 
