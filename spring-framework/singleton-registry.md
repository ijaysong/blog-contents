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
* 싱글톤은 테스트하기가 힘들다
* 서버환경에서는 싱글톤이 하나만 만들어지는 것을 보장하지 못한다.
* 싱글톤의 사용은 전역 상태를 만들 수 있기 때문에 바람직하지 못하다.


### 싱글톤 레지스트리
