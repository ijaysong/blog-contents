# 자바 내용 정리 7

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
람다식으로 간단한 지시를 적엇, 리스트로부터 추출하거나 정렬하는 것이 가능하다.  
오브젝트의 스트림과 Primitive 타입의 스트림이 있다.  
|종류                | 설명                   |
|------------------|-----------------------|
|Stream<T>    |오브젝트의 스트림 |
|IntStream       |int의 스트림         |
|LongStream   |long의 스트림      |
|DoubleStream|double의 스트림  |

stream() 메소드는 Collection 인터페이스의 디폴트 메소드이기 때문에, 모든 List나 Set에서 사용할 수 있다.  
스트림의 가장 큰 특징은 	`스트림에 대해서 다양한 처리를 수행하는 메소드가 준비되어 있다`는 점이다.  
처음부터 메소드가 지정되어 있기 때문에, 사용할 때 람다식으로 조건이나 동작을 지정하는 것만으로 가능하다.  

예를 들어, filter를 사용해 70,000원 이상의 상품을 추출한다고 해보자.  
첫번째 인덱스부터 차례대로 스트림에 리스트의 요소가 스트림의 형태로 filter() 메소드에 흘러들어오는 이미지이다.  
filter는 `중간조작`이라는 종류의 메소드로, 점점 아래로 흘려보낸다.  
중간조작의 모든 메소드는 Stream을 리턴값으로 반환한다.  
최종적으로 흐름을 멈추게 하는 처리를 `종단조작`이라고 부른다.	 
여기서 종단 조작은 forEach() 메소드로, 콘솔에 값을 출력한다.  
~~~
public static main(String[] args) {
   List<Product> list = Arrays.asList() {
      new Product(“PRODUCT_A01”, “상품 A”, 50000, “A_01”);
      new Product(“PRODUCT_B01”, “상품 B”, 110000, “B_01”);
      new Product(“PRODUCT_C01”, “상품 C”, 75000, “C_01”);
      new Product(“PRODUCT_D01”, “상품 D”, 80000, “D_01”);
      new Product(“PRODUCT_E01”, “상품 E”, 30000, “E_01”);
   };

   // filter를 사용해, 70,000원 이상의 상품을 추출해 콘솔에 출력한다.
   list.stream().filter(product -> product.getPrice() >= 70000).forEach(System.out::println);
}
~~~
스트림에 대해서 추출이나 정렬등 중간조작을 수행해, forEach등의 종단조작으로 처리를 종료한다.  
다수의 중간조작과 종단조작이 준비되어 있다.  
스트림은 다음과 같이 작성할 수 있다.  

|작성방법           | 작성 예                                                                                          |
|-----------------|------------------------------------------------------------------------------------------------|
|List, Set에서 작성 |List<Book> books = ~; <br> Stream<Books> stream = books.stream();                               |
|배열로부터 작성      |String[] array = { ~ }; <br> Stream<String> stream = Arrays.stream(array);                      | 
|직접생성           |IntStream istream = Integer.range(1, 100); <br> IntStream istream = IntStream.of(5, 12, 4, 11); |

## `중간조작이란?`
중간 조작은 스트림을 반환하므로, 메소드 체인으로 반환할 수 있다.  
`books.filter(b -> b.getPrice > 2000).sorted(Book::getName). ...`
|중간조작                           |기능              |사용 예                            |
|---------------------------------|-----------------|---------------------------------|
|filter(Predicate<T>)             |추출              |filter (b -> b.getPrice() < 2000)|
|map(Function<T>)                 |변환              |map(Book::getTitile)             |
|distinct()                       |중복을 삭제         |distinct()                       |
|sorted(Comparator<T>)            |정렬              |sorted(comparing(PC::getName))   |
|flatMap(Function<T, Stream<R>>)  |평균화            |flatMap(List::stream)             |
|skip(long n)                     |n개 스킵          |skip(3)                           |
|limit(long n)                    |n개까지           |limit(3)                          |
|mapToInt(ToIntFunction<T>)       |IntStream 변환    |mapToInt(Book::getPrice)         |
|mapToLong(ToLongFunction<T>)     |LongStream 변환   |mapToLong(Obj::getLongValue)     |
|mapToDouble(ToDoubleFunction<T>) |DoubleStream 변환 |mapToDouble(Obj::getDoubleValue) |

#### `추출 (filter)`
filter는 중간조작 메소드로, 인수는 Predicate<T> 타입이다.  
인수의 람다식으로 조건을 지정해, 추출하는 메소드이다.  
조건과 일치하는 것만 스트림으로 출력한다.  
~~~
public static void main(String[] args) {
	List<PC> list = PC.getList(); // 테스트용 리스트

   // Apple에서 만든 PC만 추출한다.
   list.stream()
      .filter(pc -> “Apple”.equals(pc.getMakker())) // Apple사의 PC만
      .forEach(System.out::println);
}
~~~

forEach로 콘솔에 출력하는 것말고도, Apple사의 PC만 포함하는 새로운 리스트를 작성하는 것도 가능하다.  
`collect 메소드`를 사용해 새로운 리스트를 만들 수 있다.  
collect 메소드는 인수로 부터 결과를 다양한 타입으로 새로 저장하는 것이 가능하다.  
collect 메소드로 toList() 메소드를 인수로 사용해, 추출 결과를 List를 만드는 것이 가능하다.  
static 메소드를 임포트해서, 클래스명인 Collectors를 생략할 수 있다.  
~~~
import static java.util.stream.Collectors.toList; // static 임포트
   public class FileterExample {
      public static void main(String[] args) {
      List<PC> list = PC.getList();

      List<PC> maker_apple = list.stream()
         .filter(pc -> “Apple”.equals(pc.getMaker())) 
         .collect(toList()); // Collectors.toList()이지만, Collectors를 생략하고 있다
   }
}
~~~

#### `변환 (map)`
람다식에서 지정한 처리를 각 요소에 적용하고, 새로운 요소로 변환하는 메소드이다.  
map의 인수는 Function<T, R> 타입이다.   
T타입의 인수를 무언가 연산을 해서 R타입으로 반환한다는 연산이 된다.  
~~~
public static void main(String[] args) {
	List<PC> list = PC.getList(); // 테스트용 리스트

	// PC타입에서 String 타입의 리스트로 변환된다.
	List<String> pcMakers = list.stream()
					.map(PC::getMaker)
					.collect(toList()); 	
	pcMakers.forEach(name -> System.out.print(name + “ ”));
}
~~~

#### `중복 삭제 (distinct)`
스트림으로부터 중복된 요소를 제거하는 메소드이다.  
같은 내용의 요소가 하나만 되도록 한다.  
해당 메소드에 인수는 없다.  
~~~
public static void main(String[] args) {
	List<PC> list = PC.getList(); // 테스트용 리스트

	// map에서 제조사명 스트림을 만든 후, distinct로부터 중복된 제조사를 삭제한다.
	List<String> makers = list.stream()
				.map(PC::getMaker)
				.distinct()
				.collect(toList()); 	
	makers.forEach(name -> System.out.print(name + “ ”));
}
~~~

#### `정렬 (sorted)`
List의 sort 메소드와 같이 스트림에 대해서 정렬을 수행하는 메소드이다.  
Comparator<T> 타입을 인수로 받는다.  
Comparator 인터페이스의 static 메소드인 comparing 메소드를 사용해, 오브젝트의 특정 항목을 기준으로 정렬을 수행한다.  
sorted에 특정 인수를 지정하지 않아도 자연스러운 순서(숫자순, 사전순 등등)로 정렬한다.  
~~~
public static void main(String[] args) {
	List<PC> list = PC.getList(); // 테스트용 리스트

	// 가격 순으로 정렬한다.
	List<String> sortedPCs = list.stream()
					.sorted(comparing(PC::getPrice))
					.collect(toList()); 	
	sortedPCs.forEach(System.out::println);
}
~~~

#### `처리의 스킵과 제한 (skip, limit)`
skip은 n개의 요소를 무시하고, 스트림으로 부터 버린다.  
limit은 요소가 많이 있어도 n개까지만 스트림으로 흘러갈 수 있도록 한다.  
skip과 limit은 long 타입의 정수 n개를 인수로 한다.  
~~~
public static void main(String[] args) {
	List<PC> list = PC.getList(); // 테스트용 리스트

	// 정렬 후, 3개를 스킵, 마지막 3개까지 스트림으로 흘러가도록 한다.
	List<String> limitedPCs = list.stream()
					.sorted(comparing(PC::getPrice))
					.skip(3) // 3개 스킵
					.limit(3) // 3개까지만 스트림으로 흘러가도록 함
					.collect(toList()); 	
	limitedPCs.forEach(System.out::println);
}
~~~

#### `평균화 (flatMap)`
map메소드와 비슷하지만, 각각의 변환 결과가 단일의 값이 아니라, 배열이나 리스트가 되는 경우에 사용한다.  
flatMap<T, Stream<R>>의 형태로, T 타입의 오브젝트를 입력해서 R타입의 스트림을 출력하는 조작이다.  
~~~
public class Department {
	private String name; // 부서명
	private String manager; // 관리자명
	private List<String> employees; // 직원명의 리스트

	public static void main(String[] args) {
		List<Department> list = Department.getList(); // 테스트용 리스트
		
		List<String> employees = list.stream()
						.map(Department::getEmployees) // List의 스트림을
						.flatMap(List::stream) // String 스트림으로 변환
						.collect(toList());
		employees.forEach(e -> System.out.print(e + “”));
	}

	public static List<Department> getList() {
		List<Department> list = Arrays.asList(
			new Department(“경영지원”, “김철수”, Arrays.asList(“김XX”, “이XX”, “박XX”)),
			new Department(“영업”, “김영희”, Arrays.asList(“최XX”, “정XX”, “윤XX”)),
			new Department(“IT개발”, “홍길동”, Arrays.asList(“조XX”, “강XX”, 송XX”))
		);
	}
}
~~~
map으로 List를 요소로 스트림을 만들어 놓고, flatMap으로 각 List를 String의 스트림으로 변환해 출력한다.  
List::stream은 (List<String> ls) -> ls.stream()의 의미이다.  
flatMap으로부터 출력된 부분 스트림은 어떤 것도 모두 String 타입의 스트림으로 전체가 하나의 String 스트림이 된다.  
즉, 문자열 스트림이 평균화 된다는 의미이다. collect에 의해서 모든 것을 한데 모아 String타입의 List로 하는 것이 가능하다.  
* Arrays.stream(배열) : 배열로부터 스트림을 만든다.  
* (String[] array) -> Arrays.stream(array)라는 의미이다.  


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

#### `조건에 매치하는지 조사하는 종단조작`
`anyMatch, noneMatch, allMatch`는 인수 람다식으로 조건을 표현하고, 조건에 해당하는 요소가 스트림 상에 있는지 없는지 조사해, 결과를 true 혹은 false로 반환한다.
* anyMatch : 하나라도 해당하는 경우, true 반환
* noneMatch : 하나도 해당하지 않는 경우, true 반환
* allMatch : 모든것이 해당하는 경우, true 반환

~~~
public static void main(String[] args) {
	List<PC> pcList = PC.getList(); // 테스트용 리스트

	// Macbook이라는 컴퓨터가 하나라도 있는지 조사
	if (pcList.stream().anyMatch(pc -> “Macbook”.equals(pc.getName()))) {

	// Macbook이라는 컴퓨터가 전혀 없는지 조사
	// if (pcList.stream().noneMatch(pc -> “Macbook”.equals(pc.getName()))) {
	// 모든요소가 Macbook이라는 컴퓨터인지 조사
	// if (pcList.stream().anyMatch(pc -> “Macbook”.equals(pc.getName()))) {
	System.out.println(“Macbook이라는 컴퓨터가 있습니다.”);
	} else {
		System.out.println(“Macbook이라는 컴퓨터가 없습니다.”);
	}
}
~~~

#### `존재 유무를 조사해 결과를 반환하는 종단조작`
filter 메소드로 특정 조건에 맞는 결과 값을 추출하고 싶을 때, 의도치 않게 결과가 0건이 반환되는 경우가 있다.  
ex) Apple사의 컴퓨터를 추출하고 싶지만, Applee이라고 조건을 잘못 지정한 경우 등등…  
그럴 때, filter에 `findAny, findFirst`를 활용하면 스트림에 해당 요소가 존재하는지 아닌지 체크할 수 있다.  

* findAny : 조건에 맞는 요소가 존재한다면, 해당 요소 중 임의의 1건을 반환
* findFirst : 조건에 맞는 요소가 존재한다면, 해당 요소 중 맨 처음에 있는 1건을 반환
* findAny, findFirst 모두 Optional 타입의 값을 반환한다.

~~~
public static void main(String[] args) {
	List<PC> pcList = PC.getList(); // 테스트용 리스트

	// 존재하지 않을 때 사용할 Dummy 인스턴스를 만들어둔다
 	PC nonePC = new PC();
	nonePC.setName(“No-exist”);

	// Apple을 Applee이라고 잘못 지정
	Optional<PC> anyPc = pcList.stream()
				.filter(pc -> “Applee”.equals(pc.getMaker()))
				.findAny();
	// 취득한 컴퓨터 명을 표시한다
	System.out.println(anyPc.orElse(nonePC).getName());
}
~~~
OUTPUT : No-exist

findAny()에서 취득한 값은 Optional 클래스의 인스턴스에 넣어서 반환한다.  
Optional 클래스는 컨테이너 클래스로, 제네릭 타입이다.  
제네릭 타입이므로 해당 예제에서 Optional<PC> 타입으로 값을 반환한다.  
Optional 클래스는 데이터가 없는 경우를 대비하여, 값을 어떻게 추출할 것인지 지정하는 메소드가 있다.  

###### `Optional 클래스`
값을 넣는 컨테이너 타입의 클래스.   
Optional 타입에 값을 넣어두고, 값이 존재하는지 아닌지 체크를 생략해서 할 수 있다는 이점이 있다.
|종류 |설명 |
|------|------|
|Optional<T> <br> OptionalInt <br> OptionalLong <br> OptionalDouble | 오브젝트 <T>의 컨테이너 <br> int의 컨테이너 <br> long의 컨테이너 <br> double의 컨테이너 |

호출하는 메소드에 의해서 값을 꺼낸다.
|메소드                |값이 없는 경우                                  |값이 있는 경우     |
|--------------------|---------------------------------------------|----------------|
|get()<br> getAsXXX()|예외가 발생한다<br> primitive 타입의 Optional의 경우 |해당 값을 반환한다. |
|orElse(값)           |파라미터로 지정한 값이 반환된다.                     |                |
|orElseGet(람다식)     |파라미터로 지정한 람다식에서 생성한 값이 반환된다.        |                |
|orElseThrow(람다식)   |파라미터로 지정한 람다식에서 생성한 예외가 발생한다.      |               |

* get : 값이 존재하는 것을 알 때 사용한다. 값이 없을 때 실행하면 예외가 발생한다.
* orElse : 값이 존재하는지 애매 할 때 사용한다. 지정한 값을 반환한다.
* orElseThrow : 값이 존재하는지 애매 할 때 사용한다. 람다식에서 작성한 예외를 발생시키는 것이 가능하다.

~~~
public static void main(String args[]) {
	List<PC> pcList = PC.getList(); // 테스트용 리스트

	// 존재하지 않을 때 사용할 Dummy 인스턴스를 만들어둔다
	PC nonePC = new PC();
	nonePC.setName(“No-exist”);

	// Apple을 Applee이라고 잘못 지정
	Optional<PC> anyPc = pcList.stream()
				.filter(pc -> “Applee”.equals(pc.getMaker()))
				.findAny();

	// 값을 취득한다
	PC pc = anyPc.get();
	// 값을 취득하지만, 취득값이 없는 경우, nonePC를 반환한다
	PC pc = anyPc.orElse(nonePC);
	// 값을 취득하지만, 취득값이 없는 경우, PC인스턴스를 만들어서 반환한다
	PC pc = anyPc.orElseGet(PC::new);
	// 값을 취득하지만, 취득값이 없는 경우, RuntimeException을 발생시킨다.
	PC pc = anyPc.orElseThrow(() -> new RuntimeException(“해당하는 값이 없습니다.”));
}
~~~

값을 꺼내는 것이 아니라, if문 처럼 2개의 처리를 선택적으로 실행하는 것도 가능하다.  
`ifPresentOrElse()`메소드는 Optional 타입의 값을 반환하지 않지만, 값의 유무에 따라서 처리를 달리하고 싶을 때 사용한다.  
Java9(2017년)부터 사용한 기능으로, if문과 비슷하게 움직이는 메소드이다.  

|ifPresentOrElse 메소드의 API                                                         |
|-----------------------------------------------------------------------------------|
|ifPresentOrElse(Consumer<T> c, Runnable r) <br>
값이 있는 경우 ---- 값을 받아서 처리를 실행한다. 처리는 Consumer 타입으로, T -> void의 형식이다. <br>
값이 없는 경우 ---- 값 없이 무언가 처리를 실행한다. 처리는 Runnable 타입으로, () -> void의 형식이다. |

~~~
public static void main(String args[]) {
	List<PC> pcList = PC.getList(); // 테스트용 리스트

	// 존재하지 않을 때 사용할 Dummy 인스턴스를 만들어둔다
 	PC nonePC = new PC();
	nonePC.setName(“No-exist”);

	// Apple을 Applee이라고 잘못 지정
	Optional<PC> anyPc = pcList.stream()
				.filter(pc -> “Applee”.equals(pc.getMaker()))
				.findAny();
				
	anyPc.ifPresentOrElse(
	PC -> System.out.println(pc.getName()),            // 해당하는 값이 있을 때
	() -> System.out.println(“해당하는 값이 없습니다.”));   // 해당하는 값이 없을 때
}
~~~

###### `하나의 값으로 한다 (reduce)`
reduce는 스트림을 하나의 값으로 변환해서 반환하는 범용 메소드 이다.  
스트림의 선두 2개의 요소에 연산(op)을 적용하고, 그 결과와 3번째 요소에 연산을 적용한다.  
그 결과와 4번째 요소에 연산 적용… 스트림의 마지막 요소까지 반복 적용한다.  
파라미터에 (T, T) -> T 의 람다식을 지정해서 스트림 처리를 지정한다.  
예를 들어, 숫자라면 합계의 최대값이나 최소값을 구할 수가 있고, 문자라면 하나로 연결하는 것도 가능하다.  
Optional 타입의 결과를 반환한다.  

~~~
public static void main(String args[]) {
	List<PC> pcList = PC.getList(); // 테스트용 리스트

	Optional<String> names = list.stream()
					.map(PC::getName) // 컴퓨터 모델명을 추출
					.reduce((a, b) -> a + “, ” + b); // 문자열을 연결
	System.out.println(names.get());
}
~~~
OUTPUT : Macbook, Gram, Surface Go, FLEX 

a는 스트림의 첫번째 요소로, b는 2번째 요소이다.   
연산이 반복되고 난 후에 a는 연산의 중간결과 값이고, b는 스트림으로부터 추출한 다음 요소이다.  
위의 예에서 a는 문자열 연결의 중간결과 값이고, 그것에 연결할 다음 문자열이 b이다.   

Optional 이외의 값을 반환하고 싶을 때 초기값을 지정하여 reduce를 실행하면 결과는 String 타입으로 반환된다.  
~~~
String names = list.stream()
			.map(PC::getName) // 컴퓨터 모델명 추출
			.reduce(“”, (a, b) -> a + “, ” + b); // 문자열 연결
~~~

###### `기본적인 계산(count, sum, average, max, min)`

`Primitive 타입의 스트림`
| Primitive 타입의 스트림 | 작성예                                                                                                | 
|----------------------|-----------------------------------------------------------------------------------------------------|
| IntStream            |IntStream is = IntStream.of(10, 15, 3); <br> IntStream is = IntStream.range(1, 100); <br> IntStream is = PC.getList.stream().mapToInt(PC::getPrice); <br><br> ※LongStream, DoubleStream에 대해서도 of, rang, mapToLong, mapToDouble을 사용해 작성할 수 있다. |
| LongStream           |                                                                                                     |
| DoubleStream         |                                                                                                     |

스트림은 of, range 와 같은 메소드로 직접 작성할 수 없지만, 보통은 스트림으로부터 mapToInt등 메소드로 요소를 추출해내 primitive 타입의 스트림으로 하는 것이 일반적이다.  
Integer 등의 Wrapper 클래스로 감싸여인채로 사용하는 것보다 계산 시 효율이 좋기 때문이다.  
스트림으로부터 primitive 타입의 요소를 추출하여 primitve 타입의 스트림으로 작성하는 메소드는 다음과 같다.  

* mapToInt
* mapToLong
* mapToDouble

~~~
public static void main(String args[]) {
	List<PC> pcList = PC.getList(); // 테스트용 리스트
	
	// 건수
	long count = list.stream().count(); 
	// 합계
	int sum = list.stream()
	.mapToInt(PC::getPrice) // IntStream이 된다.
	.sum(); 

	// 평균
	OptionalDouble ave = list.stream()
				.mapToInt(PC::getPrice)  // IntStream이 된다.
				.average();

	// 최대
	OptionalInt max = list.stream()
				.mapToInt(PC::getPrice)
				.max();   // IntStream이 된다.

	// 최소
	OptionalInt max = list.stream()
				.mapToInt(PC::getPrice)
				.min();   // IntStream이 된다.

	System.out.println(“건  수=” + count);
	System.out.println(“합  계=” + sum);
	System.out.println(“평  균=” + ave.getAsDouble());
	System.out.println(“최대값=” + max.getAsInt());
	System.out.println(“최소값=” + min.getAsInt());
}
~~~
OUTPUT : 건  수=11  
합  계=685000  
평  균=62272.727272  
최대값=98000  
최소값=12000  

최대, 최소와 아래와 같은 방법으로도 추출할 수 있다.  
* sorted 메소드로 정렬 후 findFirst메소드로 첫번째 요소를 추출 -> 최소값  
* Comparator 파라미터를 받는 max 메소드를 이용해 Optional타입의 값을 취득 -> 최대값  
* Comparator 파라미터를 받는 min 메소드를 이용해 Optional타입의 값을 취득 -> 최소값

~~~
Optional<PC> mmin = list.stream()
				.sorted(comparing(PC::getPrice))
				.findFirst();

Optional<PC> min = list.stream().min(comparing(PC::getPrice));
Optional<PC> max = list.stream().max(comparing(PC::getPrice));

System.out.println(“최소=” + min.get());
System.out.println(“최대=” + max.get());
~~~


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


## `Date and Time API`
날짜와 시간은 Java8(2014년)부터 새로운 라이브러리를 사용하게 되었다.  
날짜, 시간, 기간을 다루는 새로운 라이브러리를 Date and Time API라고 한다. 대부분의 클래스가 java.time 패키지에 존재한다.  
날짜와 시간의 계산(예: 2일 뒤의 날짜, 2일 전의 날짜, 2번째 화요일의 날짜) 및 비교가 간단하게 이루어진다.  
UTC(협정 세계시)를 표준으로 사용하며, 다음과 같은 클래스가 있다. 일반적으로 1번을 주로 사용한다.  

1. 로컬 시간을 사용한다                    : LocalDate, LocalTime, LocalDateTIme
2. UTC와의 시차를 포함해서 다루는 클래스이다   : OffsetTime, OffsetDateTime
3. 타임존을 포함해서 다루는 클래스이다         : ZonedDateTime

위의 1,2,3번 클래스를 사용해서 같은 날짜와 시간을 출력하면 다음과 같이 표현된다.

[OUTPUT]
1. 로컬시간            : 2020-10-09T10:33:35.808345100
2. 시차를 사용한 시간    : 2020-10-09T10:33:35.808345100+09:00
3. 타임존을 사용한 시간   : 2020-10-09T10:33:35.808345100+09:00[Asia/Seoul]
*T는 날짜와 시간을 구분하는 기호이다.

## `날짜 만드는 방법`
날짜를 나타내는 LocalDate 클래스의 인스턴스는 new가 아니라, 클래스의 static 메소드로 작성한다.  
클래스의 인스턴스를 반환하다는 메소드를 `팩토리 메소드`라고 한다.

`LocalDate 인스턴스를 작성하는 클래스 메소드의 API`
|메소드                | 처리 내용                                                         |
|--------------------|-----------------------------------------------------------------|
|now()               |오늘의 날짜를 반환한다.                                                |
|of(y, m, d)         |y년, m월, d일의 날짜를 한다.                                          |
|parse( str )        |문자열 str이 나타내는 날짜를 반환한다. (문자열은 `XXXX-XX-XX` 형식이여야 한다.) |
|from( temporal )    |다른 날짜로부터 새로운 날짜를 작성해 반환한다.                               |
|with( adjuster )    |주요 날짜의 달력 처리를 수행한다.                                        |


~~~
public static void main(String[] args) {
	// 오늘의 날짜
	LocalDate today = LocalDate.now();
	System.out.println(today);

	// 년월일을 지정해서 작성
	LocalDate date = LocalDate.of(2021, 12, 8);
	System.out.println(date);

	// 문자열로부터 날짜를 작성
	LocalDate date2 = LocalDate.parse("2020-05-01"); // 올바르게 지정함
	LocalDate date3 = LocalDate.parse("2020-5-1"); // 컴파일 되지만, 실행시 에러 발생
}
~~~
OUTPUT : 2020-06-14  
		 2021-12-08

## 	`날짜 편집`
LocalDate의 format() 메소드를 사용하면 `y년 m월 d일 e요일`처럼 편집해서 출력할 수 있다.  

~~~
public class FormatExample {
	public static void main(String[] args) {
		LocalDate date = LocalDate.of(2021, 7, 13);
		// 서식을 작성한다
		DateTimeFormatter fmt = DateTimeFormatter.ofPattern("y년MM월dd일 eeee");
		// 서식을 사용해 편집하고, 출력한다
		System.out.println(date.format(fmt));
	}
}
~~~
OUTPUT : 2021년 07월 13일 화요일

y, m, d, e와 같은 것을 `패턴 문자`라고 한다.  
대문자, 소문자 구별에 주의가 필요하며 월만 대문자 M이고 나머지는 다 소문자이다.  

#### `패턴 문자`
문자열을 편집할 때 아래와 같은 패턴 문자를 사용한다.

|문자 | 뜻              | 내용                                                         |
|------|--------------|-------------------------------------------------------------|
|y     |년             |yy로 년도를 2자리 수로 표현한다.                                   |
|M     |월             |MM은 월을 2자리 수로 표현한다.                                    |
|d     |일             |dd는 일을 2자리 수로 표현한다.                                    |
|a     |오전, 오후의 구별 |                                                            |
|h     |시 (12시간제)   |hh는 시간을 2자리 수로 표현한다.                                   |
|H     |시 (24시간제)   |HH는 시간을 2자리 수로 표현한다.                                   |
|e     |요일           |e, ee는 요일 번호, eee는 요일을 짧게 표시, eeee는 요일을 길게 표시 한다. |
|m     |분            |mm은 분을 2자리 수로 표현한다.                                     |
|s     |초            |ss는 초를 2자리 수로 표현한다.                                     |
|S     |1초이하의 부분   |최대 9자리수까지 S를 표현하는 것이 가능하다.                           |


## `날짜 조작`
#### `날짜로부터 값 추출`
날짜로부터 년, 월, 일의 값을 각각 추출해내는 것이 가능하다.

~~~
public class GetValue {
	LocalDate date = LocalDate.of(2022, 07, 30);
	System.out.println(date);
	System.out.println(date.getYear()); // 연도를 추출
	System.out.println(date.getMonthValue()); // 월을 추출
	System.out.println(date.getDayOfMonth()); // 일을 추출
}
~~~
OUTPUT : 2022-07-30  
2022  
7  
30  

getXxx() 라는 메소드로 값을 추출해내는 것이 가능하지만, getYear()이외에 나머지 것들은 메소드 명이 조금 복잡하다.

`LocalDate 클래스 : 날짜 요소를 취득하는 인스턴스 메소드`
|메소드                     | 기능                             |
|-------------------------|---------------------------------|
|int getYear()            | 연도 값을 반환한다.                  |
|int getMonthValue()      | 월(Month) 값을 반환한다.            |
|int getDayOfMonth()      | 일(Day) 값을 반환한다.              |
|DayOfWeek getDayOfWeek() | 요일의 값(DayOfWeek 타입)을 반환한다. |

#### `날짜 계산`
LocalDate 클래스에는 년, 월, 일 각각에 대해서 값을 더하거나 빼는 메소드가 있다.  
예를 들어, 오늘로부터 150일 후는 몇월 몇일인지 등을 단순하게 계산할 수 있다.

~~~
public class Calculation {
	public static void main(String[] args) {
		LocalDate today = LocalDate.now(); // 오늘의 날짜
		LocalDate newDay = today.plusDay(150); // 150일 후 날짜
		System.out.println(today);
		System.out.println(newDay); 
	}
}
~~~
OUTPUT : 2017-12-10  
2018-05-09

혹은 `3년 8개월 10일 후`의 날짜를 구하고 싶다면 단순하게 계산 할 수 있다.  
plusXxxs(n) 의 메소드는 LocalDate 타입의 인스턴스를 반환하므로, 다음과 같이 연결해서 메소드를 적용할 수 있다.

~~~
LocalDate newdate = today.plusYears(3).plusMonths(8).plusDays(10);
~~~

`LocalDate 클래스 : 날짜 계산을 하는 인스턴스 메소드`
|메소드 | 기능 |
|------|----|
|LocalDate plusYears(Long n) <br> LocalDate plusMonths(Long n) <br> LocalDate plusDays(Long n) | n년 후의 날짜를 반환 <br> n월 후 <br> n일 후 |
|LocalDate minusYears(Long n) <br> LocalDate minusMonths(Long n) <br> LocalDate minusDays(Long n) | n년 전의 날짜를 반환 <br> n월 전 <br> n일 전 |

#### `날짜 비교`
특정 날짜가 어떤 날보다 전인지 후인지, 혹은 같은지 비교해서 true/false를 반환하는 메소드이다.  
윤년도 조사하는 것이 가능하다.  

~~~
public class CompareExample {
	public static void main(String[] args) {
		LocalDate date1 = LocalDate.of(2020, 1, 10); // 2020-01-10
		LocalDate date2 = LocalDate.of(2019, 12, 6); // 2019-12-06
		System.out.println(date1.isAfter(date2)); // date1은 date2보다 이후?
		System.out.println(date1.isBefore(date2)); // date1은 date2보다 이전?
		System.out.println(date1.isEqual(date2)); // date1과 date2가 동일한 날짜?
		System.out.println(date1.isLeapYear()); // 윤년인가?
	}
}
~~~
OUTPUT : true  
false  
false  
true  

`LocalDate 클래스 : 날짜 비교를 수행하는 인스턴스 메소드`
|메소드                             | 기능                                     |
|---------------------------------|-----------------------------------------|
|boolean isAfter(LocalDate date)  |date 이후 날짜라면 true, 아니면 false를 반환    |
|boolean isBefore(LocalDate date) |date 이전 날짜라면 true, 아니면 false를 반환    |
|boolean isEqual(LocalDate date)  |date와 동일한 날짜라면 true, 아니면 false를 반환 |
|boolean isLeapYear()             |윤년이라면 true, 아니면 false를 반환           |

#### `기간 계산`


## `Date and TIme 관련 클래스`
|클래스 명          | 내용                                                                                               |
|-----------------|---------------------------------------------------------------------------------------------------|
|DateTimeFormatter|날짜, 시간의 서식을 나타내는 클래스 이다. <br> DateTimeFormatter fmt = DateTimeFormatter.ofPatter(서식문자열); |
|Period           |날짜의 기간을 나타내는 클래스 이다.<br> Period p = Period.between(date1, date2);                           |
|Duration         |시간의 기간을 나타내는 클래스이다. <br> Duration d = Duration.between(time1, time2);                       |
|ChronoUnit       |날짜, 시간의 간격을 나타내는 클래스이다. <br> long days = ChronoUnit.DAYS.between(time1, time2);            |
|DayOfWeek        |요일을 나타낸다. <br> DayOfWeek.SUNDAY ~ DayOfWeek.SATURDAY                                           |

