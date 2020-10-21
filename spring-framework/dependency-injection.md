# 의존관계 주입
의존관계 주입(Dependency Injection)이란, 의존성 주입이라고도 한다.
의존(종속) 오브젝트 주입이라고도 하는데, 영문 약자를 써서 DI라고 한다.

엄말히 말해 오브젝트는 다른 오브젝트에 주입할 수 있는 것이 아니지만. 
DI는 오브젝트 레퍼런스를 오부로부터 제공 받고 이를 통해 여타 오브젝트오 다이내믹하게 의존관계가 만들어지는 것이 핵심이다.

## 런타임 의존관계 설정
### 의존관계
두 개의 클래스 또는 모듈이 의존관계에 있다고 말할 때는 항상 `방향성`을 부여해줘야 한다.
즉, 누가 누구에게 의존하는 관계에 있다는 식이어야 한다.

의존하고 있다는 건 무슨 의미일까?
의존한다는 건 의존대상, B가 변하면 A에 영향을 미친다는 뜻이다.
(B의 기능이 추가되거나 변경되거나, 형식이 바뀌거나 하면 그 영향이 A로 전달된다는 것이다.)

ex) A에서 B에 정의된 메소드를 호출해서 사용하는 경우
(B에 새로운 메소드가 추가되거나 기존 메소드의 형식이 바뀌면 A도 그에 따라 수정되거나 추가되어야 할 것이다.) 

다시 말하지만, 의존관계에는 `방향성`이 있다.
A가 B에 의존하고 있지만, 반대로 B는 A에 의존하지 않는다.
의존하지 않는다는 말은 B는 A의 변화에 영향을 받지 않는다는 뜻이다.

### UserDao의 의존관계
ex)
UserDao는 ConnectionMaker 인터페이스에만 의존하고 있다.
따라서 ConnectionMaker 인터페이스가 변한다면 그 영향을 UserDao가 직접적으로 받게 된다.
하지만 ConnectionMaker 인터페이스를 구현한 클래스, 즉 DConnectionMaker 등이 다른 것으로 바뀌거나 그 내부에서 사용하는 메소드에 변화가 생겨도 UserDao에 영향을 주지 않는다.
(이렇게 인터페이스에 대해서만 의존관계를 만들어두면 인터페이스 구현 클래스와의 관계는 느슨해지면서 변화에 영향을 덜 받는 상태가 된다.)

오브젝트가 만들어지고 나서 런타임 시에 의존관계를 맺는 대상, 즉 실제 사용대상인 오브젝트를 `의존 오브젝트`라고 한다.

의존관계 주입이란 다음과 같은 세가지 조건을 충족하는 작업을 말한다.
* 클래스 모델이나 코드에는 런타임 시점의 의존관계가 들어나지 않는다. 그러기 위해서 인터페이스에만 의존하고 있어야 한다.
* 런타임 시점의 의존관계는 컨테이너나 팩토리 같은 제3의 존재가 결정한다.
* 의존관계는 사용할 오브젝트에 대한 레퍼런스를 외부에서 제공(주입)해줌으로서 만들어진다.

의존관계 주입의 핵심은 설계시점에는 알지 못했던 두 오브젝트의 관계를 맺도록 도와주는 제 3의 존재가 있다는 것이다.
DI에서 말하는 제 3의 존재는 바로 관계설정 책임을 가진 코드를 분리해서 만들어진 오브젝트라고 볼 수 있다.
DaoFactory, 스프링의 애플리케이션, 빈 팩토리, IoC 컨테이너 등이 모두 외부에서 오브젝트 사이의 런타임 관계를 맺어주는 책임을 지닌 제 3의 존재라고 할 수 있다.

## 의존관계 검색과 주입
스프링이 제공하는 IoC 방법에는 의존관계 주입만 있는 것이 아니다.
의존관계를 맺는 방법이 외부로부터의 주입이 아니라 스스로 검색을 이용하기 때문에 `의존관계 검색`이라고 불리는 것이 있다.

의존관계 검색은 자신이 필요로 하는 의존 오브젝트를 능동적으로 찾는다.
(물론 자신이 어떤 클래스의 오브젝트를 이용할지 결정하지 않는다.)
의존관계 검색은 런타임 시 의존관계를 맺을 오브젝트를 결정하는 것과 오브젝트의 생성작업은 외부 컨테이너에게 IoC로 맡기지만, 이를 가져올 때는 메소드나 생성자를 통한 주입 대신 스스로 컨테이너에게 요청하는 방법을 사용한다.

~~~
public UserDao(ConnectionMaker connectionMaker) {
    DaoFactory daoFactory = new DaoFactory();
    this.connectionMaker = daoFactory.connectionMaker();
}
~~~

이렇게 해도 UserDao는 자신이 어떤 ConnectionMaker를 사용할지 미리 알지 못한다.
코드의 의존대상은 ConnectionMaker 인터페이스 뿐이다.
런타임 시에 DaoFactory가 만들어서 돌려주는 오브젝트와 다이내믹하게 런타임 의존관계를 맺는다.

해당 방법은 외부로부터의 주입이 아니라 스스로 IoC 컨테이너인 DaoFactory에게 요청하는 것이다.
DaoFactory의 경우라면 미리 준비된 메소드를 호출하면 되니까 단순히 요청으로 보이겠지만,
이런 작업을 일반화한 스프링의 애플리케이션 컨텍스트라면 미리 정해놓은 이름을 전달해서 그 이름에 해당하는 오브젝트를 찾게 된다.
따라서 일종의 검색이라고 볼 수 있다.
또한 그 대상이 런타임 의존관계를 가질 오브젝트이므로 의존관계 검색이라고 부른다.

~~~
public UserDao(ConnectionMaker connectionMaker) {
    AnnotaionConfigApplicationContext context = new AnnotationConfigApplicationContext(DaoFactory.class);
    this.connectionMaker = context.getBean("connectionMaker", ConnectionMaker.class);
}
~~~

스프링의 IoC 컨테이너인 애플리케이션 컨텍스트의 getBean()이라는 메소드가 의존관계 검색에 사용되는 것이다.

의존관계 검색과 의존관계 주입을 적용할 때의 중요한 차이점이 있다.
의존관계 검색 방식에서는 검색하는 오브젝트는 자신이 스프링의 빈일 필요가 없다.
반면에 의존관계 주입에서는 반드시 컨테이너가 만드는 빈이여야 한다.
이런 점에서 적용방법에 차이가 있다.

## 의존관계 주입의 응용
의존관계 주입의 장점은 다음과 같다.
코드에는 런타임 클래스에 대한 의존관계가 나타나지 않고, 인터페이스를 통해 결합도가 낮은 코드를 만드므로, 다른 책임을 가진 사용 의존관계에 있는 대상이 바뀌더라도 자신은 영향받지 않으며, 변겨을 통한 다양한 확장 방법에는 자유롭다는 장점이 있다.

UserDao가 ConnectionMaker 라는 인터페이스에만 의존하고 있다는 건 ConnectionMaker를 구현하기만 하고 있다면 어떤 오브젝트든지 사용할 수 있다는 뜻이다.

### 기능 구현의 교환
개발 중에는 로컬에 있는 DB를 사용한다.
로컬 DB에 대한 연결 기능이 있는 LocalDBConnectionMaker라는 클래스를 만들고, 모든 DAO에서 이 클래스의 오브젝트를 매번 생성해서 사용한다고 하자.

그런데 서버에 배포할때는 다시 서버가 제공하는 특별한 DB 연결 클래스를 사용해야 한다.
이미 모든 클래스는 LocalDBConnectionMaker라는 클래스에 의존하고 있고, 이를 서버에 배치하는 시점에서 운영서버에서 DB에 연결할 때 필요한 ProductionDBConnectionMaker라는 클래스로 변경해야 한다.
DAO가 100개라면 최소한 100군데의 코드를 수정해야 할 것이다. (하나라도 빼먹거나 잘못 고치면 서버에서 오류가 발생할 것이다.)

모든 DAO가 생성 시점에 ConnectionMaker타입의 오브젝트를 컨테이너로부터 제공받는다.
다음은 개발 시의 DaoFactory 코드이다.
~~~
@Bean
public ConnectionMaker connectionMaker() {
    return new LocalDBConnectionMaker();
}
~~~

이를 서버에 배포할 때는 어떤 DAO 클래스와 코드도 수정할 필요가 없다.
단지 서버에서 사용할 DaoFactory를 다음과 같이 수정해주기만 하면 된다.
~~~
@Bean
public ConnectionMaker connectionMaker() {
    return new ProductionDBConnectionMaker();
}
~~~

### 부가기능 추가
DAO가 DB를 얼마나 많이 연결해서 사용하는지 파악하고 싶다고 해보자.
DAO의 코드를 수정하는 것을 지금까지 가장 피해왔던 일이며, DB 연결횟수를 세는 일은 DAO의 관심사항이 아니다.
DI 컨테이너를 활용하여 DAO와 DB 커넥션을 만드는 오브젝트 사이에 연결횟수를 카운팅 하는 오브젝트를 하나 더 추가하는 것이다.
기존 코드는 수정하지 않아도 되며, 컨테이너가 사용하는 설정정보만 수정해서 런타임 의존관계만 새롭게 정의해주면 된다.

다음은 연결횟수 카운팅 기능이 있는 클래스이다.
~~~
public class CountingConnectionMaker implements ConnectionMaker {
    int counter = 0;
    private ConnectionMaker realConnectionMaker;

    public CountingConnectionMaker(ConnectionMaker realConnectionMaker) {
        this.realConnectionMaker = realConnectionMaker;
    }

    public Connection makeConnection() throws ClassNotFoundException, SQLException {
        this.counter++;
        return realConnectionMaker.makeConnection();
    }

    public int getCounter() {
        return this.counter;
    }
}
~~~

UserDao는 ConnectionMaker 인터페이스에만 의존하고 있기 때문에 ConnectionMaker 인터페이스를 구현하고 있다면 어떤 것이든 의존성 주입이 가능하다.
CountingConnectionMaker 클래스는 ConnectionMaker 인터페이스를 구현했지만 내부에서 직접 DB 커넥션을 만들지 않는다.
대신 DAO가 DB 커넥션을 가져 올 때마다 호출하는 makerConnection()에서 DB 연결횟수 카운터를 증가시킨다.

새로운 의존관계를 컨테이너가 사용할 설정정보를 이용해 만들어보자.
CountingFactory라는 이름의 설정용 클래스를 만든다.
다음은 CountingConnectionMaker 의존관계가 추가된 의존성주입 설정용 클래스이다.
~~~
@Configuration
public class CountingDaoFactory {
    @Bean
    public UserDao userDao() {
        // 모든 DAO는 connectionMaker()에서 만들어지는 오브젝트의 의존성을 주입받는다.
        return new UserDao(connectionMaker());
    }

    @Bean
    public ConnectionMaker connectionMaker() {
        return new CountingConnectionmaker(realConnectionMaker());
    }

    @Bean
    public ConnectionMaker realConnectionMaker() {
        return new DConnectionMaker();
    }
}
~~~

다음은 커넥션 카운팅을 위한 실행 코드이다.
~~~
public class UserDaoConnectionCountingTest {
    public static void main(String[] args) throws ClassNotFoundException , SQLException {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(CountingDaoFactory.class);
        UserDao dao = context.getBean("userDao", UserDao.class);

        // Dao 사용 코드
        // 의존관계 검색을 사용하면 이름을 이용해 어떤 빈이든 가져올 수 있다.
        CountingConnectionMaker ccm = context.getBean("connectionMaker", CountingConnectionMaker.class);
        System.out.println("Connection counter : " + ccm.getCounter());
    }
}
~~~

지금은 DAO가 하나뿐이지만 DAO가 수십, 수백개여도 상관없다.
의존관계 주입의 장점은 관심사를 분리함으로서 높은 응집도를 가지는 것이기 때문에,
모든 DAO가 직접 의존해서 사용할 ConnectionMaker 타입의 오브젝트는 DaoFactory의 connectionMaker() 메소드에서 만든다.
따라서 CountingConnectionMaker의 의존관계를 추가하려면 이 메소드만 수정하면 된다.

## XML을 이용한 설정
XML로 의존관계 설정 정보를 만들 수 있다.
XML은 단순한 텍스트 파일이기 때문에 다루기 쉽다.
쉽게 이해할 수 있으며 컴파일과 같은 별도의 빌드 작업이 없다는 것도 장점이다.
환경이 달라져서 오브젝트의 관계가 바뀌는 경우에도 빠르게 변경사항을 반영할 수 있다.

### XML 설정
XML 파일은 <beans>를 루트 엘리먼트로 사용한다.
<beans>안에 여러 개의 <bean>을 정의할 수 있다.
XML 설정은 @Configuration과 @Bean이 붙은 자바 클래스로 만든 설정과 내용이 동일하다.
@Bean 메소드를 통해 얻을 수 있는 빈의 의존관계 주입 정보는 다음 세가지 이다.

* 빈의 이름
@Bean 메소드 이름이 빈의 이름이다. 이 이름은 getBean()에서 사용된다.

* 빈의 클래스
빈 오브젝트를 어떤 클래스를 이용해서 만들지를 정의한다.

* 빈의 의존 오브젝트
빈의 생성자 메소드를 통해 의존 오브젝트를 넣어준다.
의존 오브젝트도 하나의 빈이므로 이름이 있을 것이고, 그 이름에 해당하는 메소드를 호출해서 의존 오브젝트를 가져온다. 의존 오브젝트는 하나 이상일 수도 있다.
