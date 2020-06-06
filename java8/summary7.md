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
하나의 메소드만 호출하는 람다식은 메소드 참조로 표현하는 것도 가능하다.  
메소드 참조는 `클래스 명(메소드가 소속되어 있는 곳) :: 메소드 명`으로 표현한다.  
메소드 명에 `()`를 붙이지 않는다.   
좌변의 인수가 모두 메소드의 인수로 사용될 것을 가정하고 있기 때문이다.  
~~~
(double x) -> Math.sqrt(x)                ===> Math::sqrt
(double a, double b) -> Math.pow(a, b)    ===> Math::pow
(Book book) -> System.out.println(book)   ===> System.out::println
~~~
외부 인스턴스 변수의 메소드를 사용하는 경우에만 `인스턴스 변수명 :: 메소드 명`으로 지정한다.  
컨스트럭터도 `클래스 명 :: new `의 형식으로 사용하는 것이 가능하다.  
좌변의 모든 인수를 우변에 컨스트럭터를 생성하는데 사용할 것을 알기 때문에 인수의 지정은 생략한다.  
~~~
() -> new Book()                  ===> Book::new
(String code) -> new Book(code)   ===> Book::new
~~~

## 람다식의 메소드 체인
Predicate 인터페이스(`~이다`라는 조건을 기술할 때 사용)는 다음과 같은 default 메소드를 가지고 있다.  
해당 default 메소드를 사용해 여러 조건을 연결해서 사용할 수 있다.  
* and : 그리고
* or : 혹은
* negate : 부정(~이 아니다)

and, or, negate 메소드를 도트로 연결해서 사용한다.   
이러한 사용법을 `메소드 체인`이라고도 부른다.  
맨처음에 지정하는 조건만 인수 없이 사용하고, 나머지 조건은 메소드에 인수를 지정한다.  
~~~
Predicate<Book> min15000 = (book -> book.getPrice() >= 15000); // 15,000원 이상인 책
Predicate<Book> korean = (book -> “korean”.equals(book.getLanguage())); // 한국어로 된 책
Predicate<Book> english = (book -> “english”.equals(book.getLanguage()));  // 영어로 된 책

// 조건은 왼쪽에서부터 차례로 해석된다.
// (!min15000 && korean) || english
listup(list, min15000.negate()); // 15,000원이 아닌 책
listup(list, min15000.and(korean).or(english));
~~~

## Comparator 인터페이스의 static 메소드
람다식에서 static메소드를 사용할 때는 `static 임포트`를 지정해 클래스명도 생략하는 것이 일반적이다.  
인터페이스의 static 메소드를 사용할 때, static 임포트 해두면 클래스 명 지정이 생략되어 작성이 간단해진다.  
그렇게 해두면 Comparator.comparing이 아니라 comparing이라는 메소드 명 하나만으로 지정 가능하다.  
import 문에 static을 붙여서, 패키지 명부터 메소드 명까지 지정할 필요가 있다.  
~~~
import static java.util.function.Comparator.comparing; // static 임포트
~~~

`comparing( 람다식 )`
comparing 메소드를 사용하면 정렬 조건을 간단하게 지정할 수 있다.  
정렬의 키 항목을 반환하는 람다식을 인수로 지정한다.  
~~~
list.sort(comparing( Book :: getPrice )); // 가격순으로 정렬
list.sort(comparing( Book :: getLanguage )); // 사용언어순으로 정렬
~~~

## Comparator 인터페이스의 default 메소드

`thenComparing ( 람다식 )`
thenComparing 메소드는 정렬의 2차 키를 지정할 수 있다.  
첫번째 정렬에서 같은 순위의 값이 있다면 thenComparing으로 지정한 키로 한번더 정렬하는 것이다.  
comparing 메소드의 뒤에 메소드체인(도트)으로 연결하여 사용한다.  
~~~
list.sort( comparing( Book :: getPrice ) ) // 가격순으로 정렬
.thenComparing( Book :: getCode )); // 가격이 같다면 등록번호 순으로 정렬
~~~

`reversed ( )`
reversed 메소드는 역순으로 정렬한다.  
다른 정렬 조건의 뒤에 메소드체인(도트)으로 연결하여 사용한다.  
~~~
list.sort( comparing( Book :: getPrice ) // 가격순으로 정렬
.thencomparing( Book :: getCode ) // 가격이 같으면 등록 번호 순으로 정렬
.reversed() ); // 역순으로 정렬
~~~

## `forEach 메소드`
List 인터페이스의 메소드로, 인수에 지정한 람다식을 모든 요소에 순서대로 적용한다.  
for문으로 출력하는 것과 비교하면 매우 간단하게 지정할 수 있다.  
~~~
list.forEach( Book::System.out ); // 모든 요소를 출력
list.forEach( book -> System.out.println(book.getAuthor()) ); // 저자명만 출력
~~~

## `스트림이란?`
스트림은 데이터의 흐름을 말한다.  
오브젝트의 스트림과 Primitive 타입의 스트림이 있다.  
|종류                | 설            |
|-------------------|---------------|
|Stream<T>          |오브젝트의 스트림  |
|IntStream          |int의 스트림     |
|LongStream         |long의 스트림    |
|DoubleStream       |double의 스트림  |

스트림에 대해서 추출이나 정렬등 중간조작을 수행해, forEach등의 종단조작으로 처리를 종료한다.  
다수의 중간조작과 종단조작이 준비되어 있다.  
스트림은 다음과 같이 작성할 수 있다.  

|작성방법           | 작성 예                                                                                         |
|-----------------|-----------------------------------------------------------------------------------------------|
|List, Set에서 작성 |List<Book> books = ~; <br> Stream<Books> stream = books.stream();                              |
|배열로부터 작성      |String[] array = { ~ }; <br> Stream<String> stream = Arrays.stream(array);                     | 
|직접생성           |IntStream istream = Integer.range(1, 100); <br> IntStream istream = IntStream.of(5, 12, 4, 11); |

## `중간조작이란?`
중간 조작은 스트림을 반환하므로, 메소드 체인으로 반환할 수 있다.  
`books.filter(b -> b.getPrice > 2000).sorted(Book::getName). ...`
|중간조작                           |기능               |사용 예                           |
|---------------------------------|-----------------|---------------------------------|
|filter(Predicate<T>)             |추출              |filter (b -> b.getPrice() < 2000)|
|map(Function<T>)                 |변환              |map(Book::getTitile)             |
|distinct()                       |중복을 삭제         |distinct()                       |
|sorted(Comparator<T>)            |정렬              |sorted(comparing(PC::getName))   |
|flatMap(Function<T, Stream<R>>)  |평균화             |flatMap(List::stream)            |
|skip(long n)                     |n개 스킵           |skip(3)                          |
|limit(long n)                    |n개까지            |limit(3)                         |
|mapToInt(ToIntFunction<T>)       |IntStream 변환    |mapToInt(Book::getPrice)         |
|mapToLong(ToLongFunction<T>)     |LongStream 변환   |mapToLong(Obj::getLongValue)     |
|mapToDouble(ToDoubleFunction<T>) |DoubleStream 변환 |mapToDouble(Obj::getDoubleValue) |

## `기본적인 종단조작`
|종단조작 |기능|
|-----------|-----|
|boolean anyMath(Predicate<T>) <br> boolean noneMatch(Predicate<T>) <br> boolean allMatch(Predicate<T>) | 조건에 일치하는지 안하는지 확인한다. <br> 어떤것도 조건에 일치하는지 안하는지 확인한다. <br> 모든 조건에 일치하는지 안하는지 확인한다. |
|Optional<T> findAny() <br> Optional<T> findFirst() | 스트림에서 임의로 하나를 반환한다. <br> 스트림의 선두에서 하나를 반환한다. | 
|Optional<T> reduce(BinaryOperator<T>) | (T, T) -> T가 되도록 변환한다. <br> 누적해서 연산한 결과를 반환한다. |
|long count() | 데이터 조건을 반환한다. |
|int sum() |IntStream의 합계를 반환한다. |
|OptionalDouble average() | 평균값을 반환한다. (평균값은 항상 double 타입) |
|OptionalXXX max() | 최대값을 반환한다.|
|OptionalXXX min() | 최소값을 반환한다.|
|void forEach(Consumer<T>) | 모든 요소의 인수에 람다식을 적용한다. |
|collect(Collector<T, A, R>) | List, Set, Map 등에 정리해서 반환한다. |

## `collect에 의한 종단조작`
collect(Collectors.~) 처럼 사용해, 종단조작에 스트림을 집약하기 위해서 사용한다.  
static 임포트 해서, 클래스 명을 생략해 사용하면 기술이 간단해진다.   
|집약조작|기능|
|----------|------|
|groupingBy(분류기준의 람다식 [, 2차조작]) | 그룹을 나눠 결과를 Map으로 하여 반환한다. |
|partitioningBy(분류기준의 람다식 [, 2차조작]) |두 부류로 부류 결과를 Map으로 하여 반환한다. |
|toList() |List로 결과를 반환한다. |
|toSet() |Set로 결과를 반환한다. |
|toMap(Key의 람다식, Value의 람다식) |Map로 결과를 반환한다. |
|joing([seperate 문자]) |하나의 문자열로 연결하여 반환한다. |
|counting() |long의 건수를 반환한다. |
|summingXX(집계항목의 람다식) |xxx타입의 합계를 반환한다. |
|averagingXXX(집계항목의 람다식) |xxx타입의 합계를 반환한다. |
|maxBy(Comparator의 람다식) |Optional<T>타입으로, 최대 오브젝트를 반환한다. |
|minBy(Comparator의 람다식) |Optional<T>타입으로, 최소 오브젝트를 반환한다. |
|summarizingXXX() |XXXSummaryStatistics타입으로 통계값을 반환한다. |

## `Optional`
값을 넣는 컨테이너 타입  
Optional 타입에 값을 넣어두고, 값이 존재하는지 아닌지 체크를 생략해서 할 수 있다는 이점이 있다.
|종류 |설명 |
|------|------|
|Optional<T> <br> OptionalInt <br> OptionalLong <br> OptionalDouble | 오브젝트 <T>의 컨테이너 <br> int의 컨테이너 <br> long의 컨테이너 <br> double의 컨테이너 |

호출하는 메소드에 의해서 값을 꺼낸다.
|값을 호출하는 메소드 | 값이 없을 때 | 값이 있을 때 |
|--------------------------|----------------|-----------------|
|get() <br> getAsXXX() | get()을 사용하면 예외가 발생한다. <br> primitive 타입의 Optional의 경우 |저장하고 있는 값을 반환한다. |
|orElse(값) | 인수의 값을 이미 정해진 값으로서 반환한다. |저장하고 있는 값을 반환한다. |
|orElseGet(람다식) |인수의 람다식으로 생성한 값을 반환한다. |저장하고 있는 값을 반환한다. |
|orElseThrow(람다식) |인수의 람다식으로 생성한 예외를 날린다. |저장하고 있는 값을 반환한다. |

값을 꺼내는 것이 아니라, if문 처럼 2개의 처리를 선택적으로 실행하는 것도 가능하다.
|ifPresentOrElse 메소드의 API |
|---------------------------------------|
|ifPresentOrElse(Consumer<T> c, Runnable r) <br>
값이 있는 경우 ---- 값을 받아서 처리를 실행한다. 처리는 Consumer 타입으로, T -> void의 형식이다. <br>
값이 없는 경우 ---- 값 없이 무언가 처리를 실행한다. 처리는 Runnable 타입으로, () -> void의 형식이다. |

