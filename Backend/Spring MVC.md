# Spring MVC

![image](https://user-images.githubusercontent.com/55429912/124630308-46074980-debd-11eb-9306-3f00ecedc37a.png) 



**DispatcherServlet(Front Controller)**

- 모든 클라이언트의 요청을 전달 받음

- Controller에게 클라이언트의 요청을 전달하고, Controller가 리턴한 결과값을 View에게 전달하여 알맞은 응답을 생성

  



**HandlerMapping**

- 클라이언트의 요청 URL을 어떤 Controller가 처리할지를 결정
- URL과 요청 정보를 기준으로 어떤 핸들러 객체를 사용할지 결정하는 객체이며, DispatcherServlet은 하나 이상의 핸들러 매핑을 가질 수 있음



**Controller**

- 클라이언트의 요청을 처리한 뒤, Model을 호출하고 그 결과를 DispatcherServlet에 알려줌



**Model And View**

- Controller가 처리한 데이터 및 화면에 대한 정보를 보유한 객체

- Model: JSP에게 넘겨주는 Data
- View: Model을 받을 화면



**ViewResolver**

- Controller가 리턴한 뷰 이름을 기반으로 Controller의 처리 결과를 보여줄 View를 결정



**View**

- Controller의 처리결과를 보여줄 응답화면을 생성





## 구현

1. web.xml에 DispatcherServlet 등록 및 Spring 설정파일 등록(Spring 자동 생성)

   ```xml
   <servlet>
   	<servlet-name>appServlet</servlet-name>
       <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
       <init-param>
       	<param-name>contextConfigLocation</param-name>
           <param-value>/WEB-INF/spring/appServlet/servlet-context.xml</param-value>
       </init-param>
       <load-on-startup>1</load-on-startup>
   </servlet>
   
   <servlet-mapping>
   	<servlet-name>appServlet</servlet-name>
       <url-pattern>/</url-pattern>
   </servlet-mapping>
   ```

   (읽히는 순서: root-context.xml ⇒ servlet-context.xml)

2. 설정 파일에 HandlerMapping 설정

   - `servlet-context.xml` 파일 내에 <context:component-scan base-package="com.test.board" />

3. Controller 구현 및 Context 설정 파일(Servlet-context.xml)에 등록

4. Controller와 JSP의 연결을 위해 View Resolver 설정

   ```xml
   <beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
       <beans:property name="prefix" value="/WEB-INF/views/" />
       <beans:property name="suffix" value=".jsp" />
   </beans:bean>
   ```

   

5. JSP 코드 작성





**`web.xml` - DispatcherServlet 설정**

- <init-param\>을 설정하지 않으면 "<servlet-name\>-servlet.xml" file에서 applicationContext의 정보를 load
- Spring Container는 설정파일의 내용을 읽고 ApplicationContext 객체를 생성
- <url-pattern\>은 DispatcherServlet이 처리하는 URL Mapping pattern을 정의
- Servlet이므로 1개 이상의 DispatcherServlet 설정 가능
- <load-on-startup\>1</load-on-startup\>설정 시 WAS startup시 초기화 작업진행



여러개의 class가 하나의 Interface를 구현할 경우 @Qualifier를 통해 분류

































