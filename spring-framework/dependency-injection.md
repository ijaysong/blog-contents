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

### connectionMaker() 전환
DaoFactory의 connectionMaker() 메소드에 해당하는 빈을 XML로 정의해보자.
connectionMaker()로 정의되는 빈은 의존하는 다른 오브젝트가 없으니 DI 정보 세가지 중 두가지만 있으면 된다.
DI 정의 세 가지 중에서 빈의 이름과 빈 클래스 두 가지를 <bean> 태그의 id와 class 애트리뷰트를 이용해 정의할 수 있다.

다음은 클래스 설정과 XML 설정의 대응항목이다.
|           | 자바 코드 설정 정보         | XML 설정정보                  |
|-----------|------------------------|-----------------------------|
| 빈 설정파일 | @Configuration          | <beans>                     |
| 빈의 이름   | @Bean methodName()     | <bean id="methodName"       |
| 빈의 클래스 | return new BeanClass(); | class="a.b.c... BeanClass"> |

DaoFactory의 @Bean 메소드에 담긴 정보를 1:1로 XML의 태그와 애트리뷰트로 전환 해주기만 하면 된다.
<bean> 태그의 class 애트리뷰트에 지정하는 것은 자바 메소드에서 오브젝트를 만들 때 사용하는 클래스 이름이라는 점을 주의해야 한다.(import문을 대신하여 패키지까지 포함해서 써야한다.)

다음은 connectionMaker()메소드의 <bean> 태그 전환의 내용이다.
~~~
@Bean                               // <bean
public ConnectionMaker
connectionMaker() {                 // id="connectionMaker"
    return new DConnectionMaker();  // class="springbook...DConnectionMaker" />
}
~~~

### userDao()의 전환
자바 빈에서 수정자의 메소드는 프로퍼티가 된다.
프로퍼티 이름은 메소드 이름에서 set을 제외한 나머지 부분을 사용한다.
ex) setConnectionMaker()라는 이름의 메소드가 있다면, connectionMaker라는 프로퍼티를 갖는다고 할 수 있다.

XML에서는 <property> 태그를 사용해 의존 오브젝트와의 관계를 정의한다.
<property> 태그는 name과 ref라는 두 개의 애트리뷰트를 갖는다.
* name : 프로퍼티 이름, 수정자 메소드를 알 수 있음
* ref  : 수정자 메소드를 통해 주입해줄 오브젝트의 빈 이름

~~~
userDao.setConnectionMaker(connectionMaker());
~~~
여기서 userDao.setConnectionMaker()는 userDao 빈의 connectionMaker 프로퍼티를 이용해 의존관계 정보를 주입한다는 뜻이다.
메소드의 파라미터로 넣는 connectionMaker()는 connectionMaker()메소드를 호출해서 리턴하는 오브젝트를 주입하라는 의미이다.

각 정보를 <property> 태그에 대응하면 다음과 같이 전환 가능하다.
~~~
userDao.setConnectionMaker(connectionMaker());
<property name="connectionMaker" ref="connectionMaker" />
~~~

마지막으로 이 <property> 태그를 userDao 빈을 정의한 <bean> 태그 안에 넣어주면 된다.
다음은 userDao 빈을 설정한 XML 정보이다.
~~~
<bean id="userDao" class="springbook.dao.UserDao">
    <property name="connectionMaker" ref="connectionMaker" />
</bean>
~~~

### XML의 의존관계 주입 정보
다음은 완성된 XML 설정 정보이다.
~~~
<beans>
    <bean id="connectionMaker" class="springbook.user.dao.DConnectionMaker" />
    <bean id="userDao" class="springbook.dao.UserDao">
        <property name="connectionMaker" ref="connectionMaker" />
    </bean>
</beans>
~~~

<property> 태그의 name과 ref는 그 의미가 다르다.
* name : DI에 사용할 수정자 메소드의 프로버티 이름이다.
* ref  : 주입할 오브젝트를 정의한 빈의 ID이다.

보통 프로퍼티 이름과 DI되는 빈의 이름이 같은 경우가 많다.
프로퍼티 이름은 주입할 빈 오브젝트의 인터페이스를 따르는 경우가 많다.
하지만 프로퍼티 이름이나 빈의 이름은 인터페이스 이름과 다르게 정해도 상관없다.
단, 빈의 이름을 바꾸는 경우, 그 이름을 참조하는 다른 빈의 <property> ref 애트리뷰트의 값도 함께 변경해줘야 한다.

만약, connectionMaker 빈을 myConnectionMaker라는 이름으로 변경했다면 다음과 같이 userDao 빈의 connectionMaker 프로퍼티 ref 값도 바꾸어줘야 한다.
connectionMaker 빈을 DI하는 DAO가 여러개라면 모두 변경해야 한다.
~~~
<beans>
    <bean id="myConnectionMaker" class="springbook.user.dao.DConnectionMaker" />
    <bean id="userDao" class="springbook.dao.UserDao">
        <property name="myConnectionMaker" ref="connectionMaker" />
    </bean>
</beans>
~~~

혹은, 같은 인터페이스를 구현한 의존 오브젝트를 여러 개 정의해두고 그중에서 원하는 걸 골라서 DI하는 경우도 있다.
이때는 각 빈의 이름을 독립적으로 만들어두고 ref 애트리뷰트를 이용해 DI 받을 빈을 지정해주면 된다.
(같은 인터페이스를 구현한 빈이 여러개이므로 빈의 이름을 의미있게 구분해서 정해줄 필요가 있다!)

다음은 같은 인터페이스 타입의 빈을 여러개 정의한 경우이다.
~~~
<beans>
    <bean id="localDBConnectionMaker" class="...LocalDBConnectionMaker" />
    <bean id="testDBConnectionMaker" class="...TestDBConnectionMaker" />
    <bean id="productDBConnectionMaker" class="...ProductionDBConnectionMaker" />

    <bean id="userDao" class="springbook.user.dao.UserDao">
        <property name="connectionMaker" ref="localDBConnectionMaker" />
    </bean>
</beans>
~~~

## XML을 이용하는 애플리케이션 컨텍스트
XML에서 빈의 의존관계 정보를 이용하는 IoC/DI 작업에는 GenericXmlApplicationContext를 사용한다. 
GenericXmlAppliCationContext의 생성자 파라미터로 XML파일의 클래스패스를 지정해주면 된다.
XML 설정파일은 클래스패스 최상단에 두면 편하다.
클래스패스를 시작하는 /는 넣을 수도 있고 생략할 수도 있다.
(시작하는 /가 없는 경우에도 항상 루트에서부터 시작하는 클래스패스이다!)
~~~
ApplicationContext context = new GenericXmlApplicationContext("applicationContext.xml");
~~~

애플리케이션 컨텍스트가 사용하는 XML 설정파일의 이름은 관례를 따라 applicationContext.xml이라고 만든다.
다음은 XML 설정정보를 담은 applicationContext.xml 파일 정보이다.
~~~
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
                http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">
    <bean id="connectionMaker" class="springbook.user.dao.DConnectionMaker" />

    <bean id="userDao" class="springbook.user.dao.UserDao">
        <property name="connectionMaker" ref="connectionMaker" />
    </bean>
</beans>
~~~

GenericXmlApplicationContext 외에도 ClassPathXmlApplicationContext를 이용해 XML로부터 설정정보를 가져오는 애플리케이션 컨텍스트를 만들 수 있다.
ClassPathXmlApplicationContext는 클래스패스의 경로정보를 클래스에서 가져오게 할 수 잉ㅆ다.
sprirngbook.user.dao 패키지 안에 daoContext.xml이라는 설정파일을 만들었다고 해보자.

GenericXmlApplicationContext는 클래스패스 루트로부터 파일의 위치를 지정해야 하므로 다음과 같이 작성해야 한다.
~~~
new GenericXmlApplicationContext("springbook/user/dao/daoContext.xml");
~~~

반면에 ClassPathXmlApplicationContext는 XML 파일과 같은 클래스패스에 있는 클래스 오브젝트를 넘겨서 클래스패스에 대한 힌트를 제공할 수 있다.
UserDao는 springbook.user.dao 패키지에 있으므로 daoContext.xml과 같은 클래스 패스위에 있다.
이 UserDao를 함께 넣어주면 XML 파일의 위치를 UserDao의 위치로부터 상대적으로 지정할 수 있따.
~~~
new ClassPathXmlApplicationContext("daoContext.xml", UserDao.class);
~~~

이 방법으로 클래스패스를 지정해야 할 경우가 아니라면 GenericXmlApplicationConext를 사용하는 편이 무난하다.

## DataSource 인터페이스로 변환
### DataSource 인터페이스 적용
ConnectionMaker는 DB 커넥션을 생성해주는 기능 하나만 정의한 매우 단순한 인터페이스다.
지금까지는 ConnectionMaker를 사용했지만 DataSource 인터페이스로 변환하려한다.
자바에서는 DB 커넥션을 가져오는 오브젝트의 기능을 추상화해서 비슷한 용도로 사용할 수 있게 만들어진 DataSource라는 인터페이스가 존재한다.
DAO에서 DataSource의 getConnection() 메소드를 사용해 DB 커넥션을 가져오면 된다.
DataSource의 getConnection()은 SQLException만 던지기 때문에 makeConnection()메소드의 throws 에 선언했던 ClassNotFoundException은 제거해도 된다.

다음은 DataSource를 사용하는 UserDao 이다.
~~~
import javax.sql.DataSource;

public class UserDao {
    private DataSource dataSource;

    public void setDataSource(DataSource dataSource) {
        this.dataSource = dataSource;
    }

    public void add(User user) throws SQLException {
        Connection c = dataSource.getConnection();
        ...
    }
    ...
}
~~~

### 자바 코드 설정 방식
다음은 SimpleDriverDataSource를 사용하도록 만든 DataFactory의 dataSource()메소드 이다.
DataSource 타입의 dataSource 빈을 정의하는 메소드이다.
~~~
@Bean
public DataSource dataSource() {
    SimpleDriverDataSoure dataSource = new SimpleDriverDataSource();

    // DB 연결정보를 수정자 메소드를 통해 넣어준다. 이렇게 하면 오브젝트 레벨에서 DB 연결 방식을 변경할 수 있다.
    dataSource.setDriverClass(com.mysql.jdbc.Driver.class);
    dataSource.setUrl("jdbc:mysql://localhost/springbook");
    dataSource.setUsername("spring");
    dataSource.setPassword("book");

    return dataSource;
}
~~~

DaoFactory의 userDao() 메소드를 다음과 같이 수정한다.
이제 UserDao는 DataSource 타입의 dataSource()를 DI 받는다.

~~~
@Bean
public UserDao userDao() {
    UserDao userDao = new UserDao();
    userDao.setDataSource(datdaSource);
    return userDao;
}
~~~

### XML 설정 방식
XML 설정방식으로 변경해보자면, 먼저 id가 connectionMaker인 <bean>을 없애도 dataSource라는 이름의 <bean>을 등록한다.
그리고 클래스를 SimpleDriverDataSource로 변경하면 다음과 같이 된다.
~~~
<bean id="dataSource"
    class="org.springframework.jdbc.datasource.SimpleDriverDataSource" />
~~~

문제는 이 <bean>설정으로 SimpleDriverDataSource의 오브젝트를 만드는 것까지는 가능하지만, dataSource() 메소드에서 SimpleDriverDataSource 오브젝트의 수정자로 넣어준 DB 접속 정보는 나타나 있지 않다는 점이다.
UserDao처럼 다른 빈에 의존하는 경우에는 <property> 태그와 ref 애트리뷰트로 의존할 빈 이름을 넣어주면 된다.

하지만 SimpleDriverDataSource 오브젝트의 경우, 단순 Class 타입의 오브젝트나 텍스트 값이다.
그렇다면 XML에서는 어떻게 해서 dataSource()메소드에서처럼 DB 연결정보를 넣도록 설정을 만들 수 있을까?