# IT 기술면접 준비7

## `람다식이란?`
람다식이란 익명 클래스와 같은 것이다.  
람다식은 함수형 인터페이스의 추상 메소드를 오버라이드해서 그 인스턴스를 반환한다.  
람다식에는 추상 메소드의 인수와 오버라이드 부분만 쓰여진다.

## `함수형 인터페이스`
함수형 인터페이스는 추상 메소드가 하나밖에 없는 인터페이스이다.  
함수형 인터페이스는 default 메소드, static 메소드가 몇개인가 가지고 있을 수 있다.  
인터페이스 타입의 인수를 가지는 메소드에서 그것이 함수형 인터페이스라면, 인수에 람다식을 반환하는 것이 가능하다.

## `람다식 쓰는 법`
`( 인수 ) -> 식` 혹은 `( 인수 ) -> { 식; }`의 형식.  
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
 
