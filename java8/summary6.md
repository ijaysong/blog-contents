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
