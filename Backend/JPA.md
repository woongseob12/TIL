# JPA

**JPA(Java Persistence API)**: 자바 진영의 ORM 기술 표준

![image](https://user-images.githubusercontent.com/55429912/125406975-6327a500-e3f4-11eb-8bd0-9651bcb25373.png)



**ORM(Object Relational Mapping)**: 객체와 관계형 DB의 데이터를 **자동으로 매핑(연결)** 해주는 것

- 객체 지향 프로그래밍은 **클래스**, 관계형 DB는 **테이블**을 사용하여 불일치가 존재
- ORM을 통해 객체 간의 관계를 바탕으로 SQL을 자동으로 생성하여 불일치를 해결

1. implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
2. EntityManager



**Hibernate(하이버네이트)**: JPA Provider의 한 종류, JPA의 표준을 실제로 구현

![image](https://user-images.githubusercontent.com/55429912/125425189-5bbd8654-516b-4d61-98d7-20f6ff387e7a.png)



## 설정

1. Dependency 설정

   ```groovy
   dependencies{
       implementation("org.springframework.boot:spring-boot-starter-data-jpa")
       runtimeOnly("mysql:mysql-connector-java")
   }
   ```

   

2. DB 연결(application.properties)

   ```properties
   #database
   spring.datasource.url=[url주소]
   spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
   spring.datasource.hikari.username=[사용자명]
   spring.datasource.hikari.password=[비밀번호]
   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL57Dialect
   ```



3. Entity 매핑

   - 객체와 테이블 매핑: `@Entity`, `@Table`

     - `@Entity`: JPA가 Entity로서 관리
     - `@Table`: Entity와 매핑할 DB Table을 지정

   - 기본 키 매핑: `@Id`

     - `@Id`: Primary Key 지정

   - 필드와 컬럼 매핑: `@Column`

     - `@Column`: 객체 필드를 테이블 컬럼과 매핑해주는 가장 대표적인 Annotation

   - 연관관계 매핑: `@ManyToOne`, `@JoinColumn`

     - `@ManyToOne`: N:1 관계
     - `@JoinColunm`: 외래키 매핑

     

