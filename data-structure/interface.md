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