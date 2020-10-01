# 스프링의 원칙과 패턴

## 개방 폐쇄 원칙
개방 폐쇄 원칙(OCP, Open-Closed Principle)이란, 깔끔한 설계를 위해 적용 가능한 객체지향 설계 원칙 중 하나다.
클래스나 모듈은 확장에는 열려 있어야 하고 변경에는 닫혀 있어야 한다는 것이 개방 폐쇄 원칙이다.

ex) UserDao는 DB 연결 방법이라는 기능을 확장하는 데는 열려있다. (N사, D사)
UserDao에 전혀 영향을 주지 않고도 얼마든지 기능을 확장할 수 있게 되어있다.
동시에 UserDao 자신의 핵심 기능을 구현한 코드는 그런 변화에 영향을 받지 않고 유지할 수 있으므로 변경에는 닫혀있다고 할 수 있다.

### 객체 지향 설계 원칙(SOLID)
객체 지향 설계 원칙이란, 객체지향의 특징을 잘 살릴 수 있는 설계의 특징을 말한다.
* S : SRP(The Single Responsibility Principle) 단일 책임 원칙 
* O : OCP(The Open Closed Principle) 개방 폐쇄 원칙
* L : LSP (The Liskov Substitution Principle) 리스코프 치환 원칙
* I : ISP (The Interface Segregation Principle) 인터페이스 분리 원칙
* D : DIP (The Dependency Inversion Principle) 의존관계 역전 원칙

## 높은 응집도와 낮은 결합도

### 높은 응집도 란?
응집도가 높다는 것은 하나의 모듈, 클래스가 하나의 책임 또는 관심사에만 집중되어 있어 있다는 뜻이다.
변화가 일어날 때 해당 모듈에서 변화는 부분이 크다는 것이다.

반대로, 모듈의 일부분에만 변경이 일어나도 된다면, 모듈 전체에서 어떤 부분이 바뀌어야 하는지 파악하고, 
그 변경으로 인해 바뀌지 않는 부분에는 다른 영향을 미치지는 않는지 확인해야 하는 이중 부담이 생긴다.

ex) ConnectionMaker 인터페이스를 이용해서 DB 연결 기능을 독립시킨 경우라면,
DConnectionMaker를 일부 수정하더라도 전체적으로 무엇이 일어나고 무엇을 변경할지 명확하며, 기능에 영향을 주지 않는다는 사실을 손쉽게 확인할 수 있다.
DB 연결방식에 변경이 일어난 경우에는 이를 검증하려고 한다면, 변경한 ConnectionMaker 구현 클래스를 직접 테스트 해보는 것만으로도 충분하다.
기존의 NConnectionMaker를 개선해서 버전 2.0을 만들었다고 하자. 모든 DAO를 일일이 테스트 하지 않아도 되며, 새로 만든 NConnectionMaker를 직접 테스트 하는 것만으로 충분하다.

### 낮은 결합도 란?

## 전략 패턴
