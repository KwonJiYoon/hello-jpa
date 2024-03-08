# hello-jpa
[Book] 자바 orm 표준 JPA 프로그래밍

### ⚙️ Setting Info
* Language : JAVA 8 이상
* DB : H2 Database - [H2 DB Download](https://www.h2database.com/html/main.html)
* Build Tool : Maven <br>
  * 자바 라이브러리, 빌드 관리
  * 라이브러리 자동 다운로드 및 의존성 관리

### 🖥️ Create project in IntelliJ
![image](https://github.com/KwonJiYoon/hello-jpa/assets/60695604/73fd5b0f-4469-45dd-9e55-9bbd6365a633)

### 📄 Add dependencies at pom.xml
    <dependencies>
    <!-- h2DataBase -->
    <!-- version은 pc에 설치한 h2데이터베이스와 맞춰 주어야 한다. -->
    <dependency>
        <groupId>com.h2database</groupId>
        <artifactId>h2</artifactId>
        <version>2.1.210</version>
    </dependency>

    <!-- hibernate -->
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-entitymanager</artifactId>
        <version>5.3.10.Final</version>
    </dependency>
</dependencies>

### 📄 Create persistence.xml
    <?xml version="1.0" encoding="UTF-8"?>
<persistence version="2.2"
             xmlns="http://xmlns.jcp.org/xml/ns/persistence" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence http://xmlns.jcp.org/xml/ns/persistence/persistence_2_2.xsd">

    <persistence-unit name="hello">
        <properties>
            <!-- 필수 속성 -->
            <property name="javax.persistence.jdbc.driver" value="org.h2.Driver"/>
            <property name="javax.persistence.jdbc.user" value="sa"/>
            <property name="javax.persistence.jdbc.password" value=""/>
            <property name="javax.persistence.jdbc.url" value="jdbc:h2:tcp://localhost/~/test"/>
            
            <property name="hibernate.dialect" value="org.hibernate.dialect.H2Dialect"/>

            <property name="hibernate.show_sql" value="true"/>

            <property name="hibernate.format_sql" value="true"/>

            <property name="hibernate.use_sql_comments" value="true"/>
            <!--<property name="hibernate.hbm2ddl.auto" value="create" />-->

        </properties>
    </persistence-unit>
</persistence>

