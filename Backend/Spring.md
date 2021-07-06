# Spring



**Spring Framework**: 

- Java 플랫폼을 위한 오픈소스 애플리케이션 프레임워크로서 Enterprise Application을 개발하기 위한 모든 기능을 종합적으로 제공하는 경량화된 솔루션
- 자바객체를 담고 있는 경량 컨테이너



**IoC(Inversion of Control)**: 제어의 역전

- 의존 관계의 제어를 개발자가 직접해주는 것이 아닌 컨테이너가 대신 해줌
  - 컨테이너: 객체의 **생성, 사용, 소멸**에 해당하는 LifeCycle을 관리
  - DI(Dependency Injection): 유연하게 확장 가능한 객체를 만들어 두고 객체 간의 의존관계는 외부에서 동적으로 설정
    - xml(설정파일), annotation을 통해서 객체 간의 의존 관계를 설정할 수 있음
- 객체 간의 연결 관계를 런타임에 결정 
- 객체 간의 결합도를 낮춤(loose Coupling)

![image](https://user-images.githubusercontent.com/55429912/124600668-e8b1cf00-dea1-11eb-9c2b-39b808630403.png)



Spring DI Container

- Bean: Spring DI Container가 관리하는 객체
- Bean Factory: Bean들의 LifeCycle을 관리



**XML**

**Bean 등록 과정**

1. Runtime 시점에 ComponentScan이 설정 파일들(applicationContext.xml)을 읽음

   - ```java
     ApplicationContext context = new ClassPathXmlApplicationContext("com/ws/configuration/applicationContext.xml");
     
     HelloWorld hi = (HelloWorld)context.getBean("kor");
     ```

     

2. ApplicationContext에 의하여 IoC컨테이너에 등록

   - ```xml
     <bean id="kor" class = "com.ws.prac.HelloMsgKor"> </bean>
     ```



**DB**

```xml
<bean id="ds" class="SDDS">
	<property name="driverClass" value="com.mysql.cj.jdbc.Driver" />
    <property name="url" value="jdbc:mysql://127.0.0.1:3306/ssafyweb?serverTimezone=UTC&amp;useUniCode=yes&amp;characterEncoding=UTF-8" />
    <property name="username" value="ws" />
    <property name="password" value="1234" />
</bean>

<bean id="mydao" class="com.ws.model.dao.BoardDaoImpl">
	<property name="dataSource" ref="ds"></property>
</bean>
```

  

**Annotation**

- 어플리케이션의 규모가 커지고 빈의 개수가 많아질 경우 XML파일 관리하는 것이 번거로움

- 빈으로 사용될 클래스에 특별한 annotation을 부여해 주면 자동으로 빈 등록 가능

- Annotation으로 빈을 설정 할 경우 반드시 component-scan을 설정 해야 함

  - ```xml
    <context:component-scan base-package="com.ws.anno.*" />
    ```

    



`@Autowired`: 타입을 통해 의존성을 주입

- 변수, 생성자, Setter 메서드, 일반 메서드 등에 적용 가능

| Stereotype    | 적용 대상                                  |
| ------------- | ------------------------------------------ |
| `@Repository` | Data Access Layer의 DAO                    |
| `@Serviec`    | Service Layer의 클래스                     |
| `@Controller` | Presentation Layer의 MVC Controller        |
| `@Component`  | Layer 구분을 적용하기 어려운 일반적인 경우 |





**POJO(Plain Old Java Object)**:

- 특정 환경이나 기술에 **종속적이지 않은 객체지향 원리에 충실한 자바 객체**
- 특정 기술에 종속적이지 않기 때문에 생산성, 이식성 향상



**AOP(Aspect Oriented Programming)**: 

- 관심사의분리를 통해서 SW 모듈성을 향상
- 공통 모듈은 여러 코드에 쉽게 적용 가능



PSA(Portable Service): 

- 환경과 세부기술의 변경과 관계없이 일관된 방식으로 기술에 접근할 수 있게 해주는 설계 원칙





 

