# 인터페이스

## 리스트가 두 종류인 이유
왜 자바는 List 인터페이스에 두 가지 구현을 제공할까?

## 자바 interface
자바 인터페이스는 메서드 집합을 의미한다.
인터페이스를 구현하는 클래스는 인터페이스의 메서드를 제공해야 한다.

Comparable 인터페이스의 경우 다음과 같다.
~~~
public interface Comparable<T> {
    public int compareTo(T o);
}
~~~

Comparable 인터페이스를 구현하려면 클래스는 다음과 같아야 한다.
* T 타입을 명시해야 한다
* T 타입의 객체를 인자로 받고, int를 발환하는 compareTo() 메서드를 제공해야 한다.

예를 들어, java.lang.Integer 클래스의 소스코드는 다음과 같다.
~~~
public int compareTo(Integer anotherInteger) {
    int thisVal = this.value;
    int anotherVal = anotherInteger.value;
    return (thisVal<anotherVal ? -1 : (thisVal==anotherVal? 0 : 1));
}
~~~

이 클래스는 Number 클래스를 확장하여, Number 클래스의 메서드와 인스턴스 변수를 상속 받아 Comparable<Integer> 인터페이스를 구현한다.
따라서, Integer 객체를 인자로 받고 int를 반환하는 compareTo 메서드를 제공한다.

클래스가 인터페이스를 구현한다고 선언하면 컴파일러는 인터페이스가 정의한 모든 메소드를 제공하는지 확인한다. 

## 리스트 interface
자바 컬렉션 프레임워크는 List라는 인터페이스를 정의하고, ArrayList와 LinkedList라는 두 구현 클래스를 제공한다.
인터페이스는 리스트가 된다는 의미가 무엇인지를 정의한다.
이 인터페이스를 구현하는 클래스는 add, get, remove와 약 20가지 메서드를 포함한 특정 메서드 집합을 제공해야 한다.
ArrayList와 LinkedList 클래스는 이러한 메서드를 제공하므로 상호교환 할 수 있다.
List로 동작하는 메서드는 ArrayList와 LinkedList 또는 List를 구현하는 어떤 객체와도 잘 동작한다.

~~~
public ListClientExample() {
    list = new LinkedList();
}

private List getList() {
    return list;
}

public static void main(String[] args) {
    ListClientExample lce = new ListClientExample();
    List list = lce.getList();
    System.out.println(list);
}
~~~

ListClientExample 클래스의 생성자는 새로운 LinkedList 객체를 만들어 리스트를 초기화 한다.
getList 메서드는 게터 메서드로 List 참조를 반환한다.

이 소스에서 눈여겨 볼 점은
LinkedList나 ArrayList 같은 구현 클래스를 사용핳지 않고 가능한 한 List 인터페이스를 사용한다는 점이다.
예를 들어, 인스턴스 변수는 List 인터페이스로 선언하고 getList 메서드도 List 형을 반환하지만 구체적인 클래스는 언급하지 않는다.
마음을 바꿔 ArrayList 클래스를 사용하고자 한다면 생성자만 바꾸면 되고 그 외에는 그대로 두면 된다.

이러한 스타일을 인터페이스 기반 프로그래밍 or 인터페이스 프로그래밍이라고 한다.
여기서 인터페이스는 자바 인터페이스가 아닌 일반적인 개념의 인터페이스를 말한다.

라이브러리를 사용할 때 코드는 오직 List와 같은 인터페이스만 의존하고 ArrayList 와 같은 특정 구현에 의존하지 않아야 한다.
이러한 방식으로 하면 나중에 구현이 변경되어도 인터페이스를 사용하는 코드는 그대로 사용할 수 있기 때문이다.

반면에 인터페이스가 변경되면 인터페이스를 의존하는 코드는 변경되어야 한다.
이것이 꼭 필요한 일이 아니면 라이브러리 개발자가 인터페이스를 변경하지 않는 이유이다.

## 실습