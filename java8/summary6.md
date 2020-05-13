# IT 기술면접 준비6

## `Collection	프레임워크`
리스트, 셋, 맵 3가지 데이터 구조를 제공하는 Java 라이브러리이다.  
* 리스트 (List) : 사이즈가 자동으로 확대 됨.   
* 셋 (Set) : 같은 값은 하나밖에 등록되지 않음.  
* 맵 (Map) : 키와 값을 쌍으로 저장하며 키로 오브젝트를 검색하는 것이 가능하다.  

## `각 클래스의 특징`
Hash, Linked, Tree의 접두사가 붙은 클래스
* Hash : (해쉬 알고리즘에 의한) 검색 기능
* Linked : (리스트 알고리즘에 의한) 입력순서 저장 기능 
* Tree : 정렬 기능

1.List  
1.1 ArrayList : 사이즈가 자동으로 확장하는 배열. 같은 요소를 중복해서 저장가능. 순서대로 저장됨.  
1.2 LinkedList : ArrayList의 특징 + 요소의 추가, 삭제의 효율이 좋음.  

2. Set  
2.1 HashSet : 같은 요소를 중복해서 저장X. 요소의 순서가 정해져 있지 않음.  
2.2 LinkedHashSet : 요소 중복 불가. 순서대로 저장됨.  
2.3 TreeSet : 요소 중복 불가. 정렬된 상태에서 데이터를 뽑아낼 수 있음.  

3. Map  
3.1 HashMap : 키-값의 형태로 저장. 키로 검색 가능. 요소의 순서가 정해져 있지 않음.  
3.2 LinkedHashMap : 검색 가능. 순서대로 저장됨.  
3.3 TreeMap : 검색 가능. 키로 정렬된 상태에서 데이터를 뽑아낼 수 있음.  

## `ArrayList란?`
전체 사이즈가 자동적으로 확대되는 배열.  
초기 Default 사이즈는 10이지만, 요소를 추가하면 자동으로 확대된다.  

**<ArrayList의 작성>**  
좌변은 ArrayList가 아니라 List타입으로 지정하는 것이 일반적이다.  
~~~
List<String> list = new ArrayList<>();
~~~

**<ArrayList 관련 메소드>**  
* add() 메소드 : 오브젝트를 추가. 등록 순서에 따라 저장된다.  
* size() 메소드 : 리스트의 길이를 반환한다.  
* get(i) 메소드 : 리스트의 i번째 데이터를 반환한다.  
~~~
list.add(“A”);
list.add(“B”);
list.add(“C”);

int length = list.size(); // 리스트의 길이를 반환

int value = list.get(0); // 리스트의 0번째 데이터가 반환 -> A
~~~

## `Wrapper 클래스 타입의 리스트`
int나 double 등 primitive타입의 데이터는 오브젝트가 아니기 때문에 리스트에 추가가 안된다.  
primitive타입의 데이터를 오브젝트화 해서 등록할 필요가 있는데, primitive타입의 데이터를 오브젝트로 감싸서 등록한다고 하여 Wrapper 클래스라고 한다.  
| primitive타입 | Wrapper 클래스 |
|------------------|----------------------|
| char              | Character         |
| byte              | Byte                  |
| short             | Short                |
| int                 | Integer              |
| long              | Long                  |
| float              | Float                  |
| double          | Double               |
| boolean        | Boolean             |

~~~
List<Integer> list = new ArrayList<>(); // Integer 타입의 리스트

list.add(109); // 숫자를 리스트에 추가
list.add(201);
list.add(300);

for(int i : list) {
  System.out.println(i); // 리스트에서 값을 꺼내 출력
}
~~~

primitive타입과 Wrapper 클래스는 자동 형변환을 하기때문에 Integer 타입의 리스트에서 Int 타입의 값을 출력할 수 있는 것이다.  
* 오토박싱 (Autoboxing) : primitive타입 -> Wrapper 클래스
* 오토언박싱 (Autounboxing) : Wrapper 클래스 -> primitive타입

## `Linked 리스트란?`
ArrayList는 요소를 메모리 상에 연속해서 나열한 단순한 배열의 형태.  
LinkedList는 하나의 요소에 다음 요소의 참조값(메모리 상의 위치), 저장할 데이터로 구성되어 있다.  
ArrayList에선 삽입과 삭제를 하기 위해 대량의 데이터를 이동시켜야 하기 때문에 효율이 좋지 않다.  
LinkedList는 삽입과 삭제를 하기 위해 다음요소의 참조값만 바꾸면 되기 때문에 빨리 처리할 수 있다.  
값을 참조하는 것이 주요 목적이라면 ArrayList를, 값의 삽입과 삭제가 이루어진다면 LinkedList를 활용하는 것이 적절하다.  

## `배열 -> 리스트 만들기`
`Arrays.asList() 메소드`는 리스트를 만드는 간단한 메소드이다.
~~~
// 예시1
List<Member> list = Arrays.asList(new Member(‘101’, ‘홍길동’),
new Member(‘102’, ‘김갑돌’),
new Member(‘103’, ‘김갑순’));

// 예시2
int[] numbers = {1, 2, 3, 4, 5};
List<Integer> list2 = Arrays.asList(numbers);
~~~

## `변하지 않는 리스트`
`of()메소드`는 처음에 모든 요소를 추가해놓고, 값을 참조하기만 할때 가장 많이 사용된다.

~~~
// 비어있는 리스트 작성
List<String> list = List.of();

// 요소를 ,(쉼표)로 구분해서 작성
List<String> list2 = List.of(“111”, “222”, “333”);

// 배열로부터 작성
String[] array = {“test1”, “test2”, “test3”};
List<String> list3 = List.of(array); 
~~~

of() 메소드로 작성된 리스트는 참조용이라서 요소의 추가, 변경, 삭제, 정렬이 되지 않는 불변의 리스트이다.  
리스트가 외부로부터 변경되지 않도록 하고 싶을 때 사용된다.  
of() 메소드는 Java9(2017년)부터 사용됨.  
~~~
List<String> list = List.of(“홍길동”, “김갑돌”); // 리스트 작성

try {
  list.add(“김갑순”); // 요소 추가
} catch(RunTimeException e) {
  System.out.println(“List에 등록되지 않았습니다.”);
}
~~~
OUTPUT : List에 등록되지 않았습니다.

## `리스트 정렬`
`sort(<comparator>) 메소드`를 통해서 지정한 항목을 기준으로 리스트의 요소를 정렬하는 것이 가능하다.  
구체적으로는 comparator(정렬에서 사용하는 비교 메소드를 가지고 있는 오브젝트)를 implements한 클래스를 지정해 실행 한다.  

java.util 패키지의 comparator 인터페이스
~~~
public interface Comparator<T> {
  int compareTo(T o1, T o2);
}
~~~

comparator인터페이스를  implements한 클래스를 작성한다.
~~~
public class NameComparator implements Comparator<Member> {
  public int compare(Member o1, Member o2) {

    String s1 = o1.getName();
    String s2 = o2.getName();

    return s1.compareTo(s2); // 이름을 비교해서 음수, 0, 정수를 반환한다.
  } 
}
~~~ 

List에 등록한 Member오브젝트를 이름순으로 정렬한다.
~~~
public class sortExample {
  public static void main(String[] args) {
    List<Member> list = Arrays.asList(new Member(‘101’, ‘홍길동’),
                                      new Member(‘102’, ‘김갑돌’),
                                      new Member(‘103’, ‘김갑순’));

    NameComparator comp = new NameComparator(); // Comparator 작성
    list.sort(comp); // 정렬

    for(Member m : list) {
      System.out.print(m.getName + “\t”);
    }
  }
}
~~~
OUTPUT : 김갑돌 김갑순 홍길동	

## `Set 계열 클래스의 특징`
데이터의 집합으로 같은 요소가 포함될 수 없다.   
데이터의 정렬이나 대소관계는 없다.  
Set을 implements한 클래스 중에 HashSet은 집합을 표현하는 클래스, LinkedHashSet은 정렬 기능을 추가한 것, TreeSet은 대소관계를 다루는 기능을 추가한 것이다.

## `HashSet 클래스`
~~~
Set<String> ids = new HashSet<>();
ids.add(“apple”);
ids.add(“cookie”);
ids.add(“dragon”);
ids.add(“banana”); // 중복값 등록

for(String id : ids) {
	System.out.print(id + “\t”);
}
~~~
OUTPUT : dragon banana cookie apple

중복된 값은 Set에 하나만 등록된다.  
등록된 순서대로 출력되지 않다. Set 내부적으로 배치를 결정하는 알고리즘이 없기 때문이다.  
순서대로 출력하고 싶다면, LinkedHashSet을 사용하면 된다.  

## `LinkedHashSet 클래스`
~~~
Set<String> ids = new LinkedHashSet<>(); // HashSet에서 LinkedHashSet으로 변경
ids.add(“apple”);
ids.add(“cookie”);
ids.add(“dragon”);
ids.add(“banana”); // 중복값 등록

for(String id : ids) {
	System.out.print(id + “\t”);
}
~~~
OUTPUT : apple cookie dragon banana

추가한 순서를 기억하는 Set.  
HashSet처럼 중복이 존재하지 않는 것은 동일하지만, 등록한 순서대로 출력된다는 점이 다름.  

## `TreeSet 클래스`
~~~
Set<String> ids = new TreeSet<>(); // LinkedHashSet에서 TreeSet으로 변경
ids.add(“apple”);
ids.add(“cookie”);
ids.add(“dragon”);
ids.add(“banana”); // 중복값 등록

for(String id : ids) {
	System.out.print(id + “\t”);
}
~~~
OUTPUT : apple banana cookie dragon

등록한 요소를 자연스러운 순서로 정렬하는 Set.  
문자열의 경우, 사전순으로 정렬된다.  
TreeSet에서도 같은 요소를 등록하는 것이 불가능하지만, 사전순으로 출력하고 있다. 이것이 TreeSet의 특징.  
정렬이 되려면 Comparable 인터페이스를 Implements했거나, 컨스트럭터로 정렬방법을 지정해줄 필요가 있다.  

## `변하지 않는 Set`
`of() 메소드`를 사용하면 내용이 변하지 않는 Set을 만들 수 있다.  
Java9(2017년)부터 사용하기 시작한 기능.  
of() 메소드의 인수로 등록할 요소를 컴마로 구분하여 입력하거나, 요소의 배열을 지정한다.  
~~~
// 요소를 컴마로 구분하여 입력
Set<String> set = Set.of(“홍길동”, “김갑돌”, “김갑순”);

// 요소의 배열을 지정
String[] names = {“홍길동”, “김갑돌”, “김갑순”};
Set<String> set2 = Set.of(names);
~~~

요소에 null이나 중복된 값은 지정할 수 없음. 실행하면 예외가 발생함.
~~~
Set.of(“홍길동”, null, “김갑순”); // null 입력
Set.of(“홍길동”, “김갑돌”, “김갑순”, “김갑순”); // 중복된 값 입력
~~~
OUTPUT : 에러 발생

더불어서, add()메소드나 remove()메소드를 실행할 수 없다. 실행하면 예외가 발생함.  
of()메소드는 HashSet, LinkedHashSet, TreeSet와 같은 클래스를 지정해서 사용할 수 없다.  
Set인터페이스의 인스턴스에서만 사용할 수 있다.  

## `Map계열 클래스의 특징`
키와 값을 쌍으로 등록한다.  
키로 검색하여 값을 추출해낼 수 있다. 해쉬 알고리즘을 통해서 빠르게 검색이 가능하다.  
일반적으로 HashMap을 사용하지만 Map에서 요소를 하나씩 빼낼 때 등록된 순서로 추출되지 않는다.  
등록 순서대로 추출하고 싶다면 LinkedHashMap 클래스를 사용한다.  
자연스러운 순서(ex. 사전순)로 정렬되어 추출되길 원한다면 TreeMap 클래스를 사용한다.  

* HashMap : 키와 값을 쌍으로 등록, 키로 값 검색 가능
* LinkedHashMap : 검색 가능, 저장한 순서대로 추출
* TreeMap : 검색 가능, 키로 정렬된 상태에서 추출

## `미등록 키로 검색한 경우 & 중복 키를 등록한 경우`
미등록 키로 검색한 경우, null이 반환된다.  
이것을 피하고 싶다면 get()메소드가 아닌 getOrDefault() 메소드를 사용한다.  
중복 키를 등록한 경우, 나중에 등록된 키 값이 덮어씌워진다.  

~~~
Map<Integer, String> map = new HashMap<>();
map.put(115, “홍길동”);
map.put(120, “김갑돌”);
map.put(108, “김갑순”);
map.put(115, “김철수”);

System.out.print(map.get(108) + ”, ”);
System.out.print(map.get(115) + ”, ”);
System.out.print(map.getOrDefault(811, “미등록”));
~~~
OUTPUT : 김갑순, 김철수, 미등록

## `Map의 모든 요소를 뽑아내기`
`entrySet() 메소드`는 Map의 모든 엔트리를 모은 Set을 반환한다.  
다만, 각 엔트리는 키와 값을 세트로 저장한 Map.entry타입의 인스턴스다.  
따라서 확장 for문에서는 Set으로부터 순서대로 Map.entry타입의 인스턴스를 추출해내는 처리가 된다.  
Map.entry타입에는 키를 뽑아내는 `getKey() 메소드`와 값을 뽑아내는 `getValue() 메소드`가 있다.  

~~~
Map<Integer, String> map = new HashMap<>();
map.put(115, “홍길동”);
map.put(120, “김갑돌”);
map.put(108, “김갑순”);

for(Map.Entry<Integer, String> entry : map.entrySet()) {
	System.out.println(entry.getKey() + “, ” + entry.getValue());
}
~~~ 
OUTPUT : 115 = 홍길동
108 = 김갑순
120 = 김갑돌

## `Map.Entry타입`
Map 인터페이스 내부에 Entry 인터페이스가 정의되어 있다. (특이한 케이스)  
Map.Entry는 Map과의 관계를 표현하기 위해 Map 인터페이스 내부에 선언되어 있다.  
인터페이스 안에 인터페이스가 정의된 형태이므로, `내부 인터페이스`라고도 부른다.  
기능적인 측면에서는 다른 인터페이스들과 동일하지만, 인터페이스를 그룹화해 유지되기 쉽게함과 동시에 Map과의 관계를 강하게 강조하는 이점이 있다.  

## `LinkedHashMap과 TreeMap`
등록 순서대로 추출하고 싶다면 LinkedHashMap 클래스를 사용한다.
~~~
Map<Integer, String> map = new LinkedHashMap<>(); // 등록된 순서대로 출력된다.
map.put(115, “홍길동”);
map.put(120, “김갑돌”);
map.put(108, “김갑순”);

for(Map.Entry<Integer, String> entry : map.entrySet()) {
	System.out.println(entry.getKey() + “, ” + entry.getValue());
}
~~~ 
OUTPUT : 115 = 홍길동  
120 = 김갑돌  
108 = 김갑순

자연스러운 순서(ex. 사전순)로 정렬되어 추출되길 원한다면 TreeMap 클래스를 사용한다.  
~~~
Map<Integer, String> map = new TreeMap<>(); // 번호순서대로 출력된다.
map.put(115, “홍길동”);
map.put(120, “김갑돌”);
map.put(108, “김갑순”);

for(Map.Entry<Integer, String> entry : map.entrySet()) {
	System.out.println(entry.getKey() + “, ” + entry.getValue());
}
~~~ 
OUTPUT : 108 = 김갑순  
115 = 홍길동  
120 = 김갑돌

## `불변의 Map을 만드는 of()와 ofEntries()메소드`
`of()메소드` 혹은 `ofEntries()메소드`를 사용하면 내용이 바뀌지 않는 맵을 만들 수 있다.  
Java9(2017년) 부터 사용하게 된 기능이다.  
불변의 맵은 일단 작성하면, 추가, 삭제, 변경이 불가능하다. 또, 키값으로 null을 지정할 수 없다.  
of()메소드는 키와 값을 번갈아가며 최대 10개까지 지정하여 불변의 맵을 만들 수 있다.  
ofEntries()메소드는 키와 벨류를 가지는 엔트리를 지정하여 불변의 맵을 만들 수 있으며, 지정할 엔트리의 개수는 제한이 없다.  

~~~
// 키와 값을 번갈아가며 지정 (최대 10개까지)
Map<Integer, String> map = Map.of(1, “TEST1”, 2, “TEST2”, 3, “TEST3”); // 3개의 엔트리를 지정함.

// Map.Entry타입의 요소를 나열해서 지정(제한 없음, 배열을 지정해도 가능함)
Map<Integer, String> map2 = Map.ofEntries(Map.entry(1, “TEST1”)
, Map.entry(2, “TEST2”)
, Map.entry(3, “TEST3”));
~~~

