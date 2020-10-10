# 싱글톤 레지스트리
new 연산자를 사용하면 매번 다른 오브젝트가 출력됨을 당연히 알 수 있다.
~~~
DaoFactory factory = new DaoFactory();
UserDao dao1 = factory.userDao();
UserDao dao2 = factory.userDao();

System.out.println(dao1);
System.out.println(dao2);
~~~
출력 :
spring.book.dao.UserDao@118f375
spring.book.dao.UserDao@117a8bd


스프링의 애플리케이션 컨텍스트에 DaoFactory를 설정정보로 등록하고,
getBean()메소드를 이용해 userDao라는 이름으로 등록된 오브젝트를 가져와보면,
여러번 호출해도 동일한 오브젝트가 출력됨을 알 수 있다.
스프링은 여러 번에 걸쳐 빈을 요청하더라도 매번 동일한 오브젝트를 돌려준다는 것이다.
~~~
ApplicationContext context = new AnnotationConfigApplicationContext(DaoFactory.class);

UserDao dao3 = context.getBean("userDao", UserDao.class);
UserDao dao4 = context.getBean(("userDao", UserDao.class);

System.out.println(dao3);
System.out.println(dao3);
~~~
출력 :
spring.book.dao.UserDao@ee22f7
spring.book.dao.UserDao@ee22f7

## 싱글톤 레지스트리로서의 애플리케이션 컨텍스트

### 싱글톤 패턴이란?
어떤 클래스를 애플리케이션 내에서 제한된 인스턴스 개수, 이름처럼 주로 하나만 존재하도록 강제하는 패턴이다.
이렇게 하나만 만들어지는 클래스의 오브젝트는 애플리케이션 내에서 전역적으로 접근이 가능하다.
단일 오브젝트만 존재해야 하고, 이를 애플리케이션의 여러 곳에서 공유하는 경우에 주로 사용한다.

### 서버 애플리케이션과 싱글톤
스프링은 별다른 설정을 하지 않으면 내부에서 생성하는 빈 오브젝트를 모두 싱글톤으로 만든다.
왜 스프링은 싱글톤으로 빈을 만드는 것일까?

스프링이 주로 적용되는 대상이 자바 엔터프라이즈 기술을 사용하는 서버 환경이기 때문이다.
스프링이 처음 설계됐던 대규모의 엔터프라이즈 서버환경은 서버 하나당 최대로 초당 수십에서 수백번씩 브라우저나 여타 시스템으로부터의 요청을 받아 처리할 수 있는 높은 성능이 요구되는 환경이었다.
하나의 요청을 처리하기 위해 매번 클라이언트로부터 요청이 올때마다 오브젝트를 새로 만들어 사용한다면, 서버에 큰 부하가 걸리게 되기 때문에 사용자의 요청을 담당하는 여러 스레드에서 하나의 오브젝트를 공유해 동시에 사용하도록 한 것이다.

### 싱글톤 패턴의 구현
* 클래스 밖에서는 오브젝트를 생성하지 못하도록 private으로 만든다.
* 생성된 싱글톤 오브젝트를 저장할 수 있는 자신과 같은 타입의 스태틱 필드를 정의한다.
* 스태틱 팩토리 메소드인 getInstance()를 만들고 이 메소드가 최도로 호출되는 시점에서 한번만 오브젝트가 만들어지게 한다. 생성된 오브젝트는 스태틱 필드에 저장된다. 또는 스태틱 필드의 초기값으로 오브젝트를 미리 만들어둘 수도 있다.
* 한번 오브젝트(싱글톤)가 만들어지고 난 후에는 getInstance() 메소드를 통해 이미 만들어져 스태틱 필드에 저장해둔 오브젝트를 넘겨준다.

~~~
public class UserDao {
    private static UserDao INSTANCE;

    private ConnectionMaker connectionMaker;

    private UserDao(ConnectionMaker connectionMaker) {
        this.connectionMaker = connectionMaker;
    }

    public static synchronized UserDao getInstance() {
        if (INSTANCE == null) INSTANCE = new UserDao(???);
        return INSTANCE;
    }
}
~~~

UserDao에 싱글톤을 위한 코드가 추가되었다.
private으로 바뀐 생성자는 외부에서 호출할 수 없기 때문에 DaoFactory에서 UserDao를 생성하여 Connectionmaker 오브젝트를 넣어주는게 이제는 불가능해졌다.

### 싱글톤 패턴의 한계
일반적으로 싱글톤 패턴 구현 방식에는 다음과 같은 문제가 있다.

* private 생성자를 갖고 있기 때문에 상속할 수 없다.
싱글톤 패턴은 생성자를 private으로 제한한다.
문제는 private 생성자를 가진 클래스는 다른 생성자가 없다면 상속이 불가능하다.
객체지향의 장점인 상속과 이를 적용한 다형성을 적용할 수 없다.
오브젝트의 경우 싱글톤으로 만들었을 때 객체 지향적인 설계의 장점을 적용하기가 어렵다는 점은 심각한 문제이다.

* 싱글톤은 테스트하기가 힘들다
싱글톤은 만들어지는 방식이 제한적이기 때문에 테스트에서 사용하기 힘들다.
싱글톤은 초기화 과정에서 생성자 등을 통해 사용할 오브젝트를ㄹ 다이내믹하게 주입하기도 힘들기 때문에 필요한 오브젝트는 직접 오브젝트를 만들어 사용할 수 밖에 없다.
이런 경우 테스트용 오브젝트로 대체하기 힘들다.

* 서버환경에서는 싱글톤이 하나만 만들어지는 것을 보장하지 못한다.
서버에서 클래스 로더를 어떻게 구성하고 있는냐에 따라서 싱글톤 클래스임에도 하나 이상의 오브젝트가 만들어 질 수 있다.
여러 개의 JVM에 분산돼서 설치가 되는 경우에도 각각 독립적으로 오브젝트가 생기기 때문에 싱글톤으로서의 가치가 떨어진다.

* 싱글톤의 사용은 전역 상태를 만들 수 있기 때문에 바람직하지 못하다.
싱글톤은 사용하는 클라이언트가 정해져 있지 않다.
싱글톤의 스테틱 메소드를 이용해 언제든지 싱글톤에 쉽게 접근할 수 있기 때문에 에플리케이션 어디서든지 사용될 수 있고, 그러다보면 자연스럽게 전역 상태로 사용되기 쉽다.
아무 객체나 자유롭게 접근하고 수정하고 공유할 수 있는 전역 상태를 갖는 것은 객체지향 프로그래밍에서는 권장되지 않는 프로그래밍 모델이다.
그럴바에는 아예 스태틱 필드와 메소드로만 구성된 클래스를 사용하는 편이 낫다.


### 싱글톤 레지스트리
