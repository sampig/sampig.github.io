---
layout: post
title: "Spring Practice: Spring+SpringMVC+MyBatis"
date: 2019-07-24 15:15:00 +0200
category: tutorial
tagline: ""
tags: [Java, Spring, MyBatis]
abstract : "Learning Note: how to build SSM web projects using Maven in Eclipse."
---
{% include JB/setup %}

* [Introduction](#introduction)
    - [Spring Framework and SpringMVC](#spring-framework-and-springmvc)
    - [MyBatis](#mybatis)
    - [Maven](#maven)
* [Creation Process](#creation-process)
    - [Preparation for Database](#preparation-for-database)
    - [Create a Project](#create-a-project)
    - [Modify Configuration Files](#modify-configuration-files)
    - [Create Classes](#create-classes)
    - [Run Functional Testing](#run-functional-testing)
    - [Create Web Pages](#create-web-pages)
    - [Start Server](#start-server)
* [Summary](#summary)
* [References](#references)


# Introduction

In this blog, I will build a SSM (Spring+SpringMVC+MyBatis) project based on Maven in Eclipse.

The tools and the libraries that I use:
1. JDK 1.8.0_91 ([Java SE Downloads](https://www.oracle.com/technetwork/java/javase/downloads/index.html){:target="_blank"})
2. Apache Tomcat 9.0.22 ([Apache Tomcat 9 Downloads](https://tomcat.apache.org/download-90.cgi){:target="_blank"})
3. MySQL 5.6.36 ([MySQL Community Server Downloads](https://dev.mysql.com/downloads/mysql/){:target="_blank"})
4. Apache Maven 3.3.9 ([Apache Maven Downloads](https://maven.apache.org/download.cgi){:target="_blank"}) ([Gradle](https://gradle.org/){:target="_blank"} is an alternative.)
5. Eclipse IDE for Enterprise Java Developers 2019-06 R Packages ([Eclipse IDE 2019-06 R Packages Downloads](https://www.eclipse.org/downloads/packages/){:target="_blank"})
6. Spring Framework 5.1.5
7. MyBatis 3.4.6 ([Hibernate](http://hibernate.org/){:target="_blank"} is an alternative.)
8. MyBatis-Spring 1.3.2

You can try other newer stable or released versions.
In addition, [IntelliJ IDEA](https://www.jetbrains.com/idea/){:target="_blank"}, developed by JetBrains, is another popular IDE for Java development now.

## Spring Framework and SpringMVC

The Spring Framework provides a comprehensive programming and configuration model for modern Java-based enterprise applications - on any kind of deployment platform.

A key element of Spring is infrastructural support at the application level: Spring focuses on the "plumbing" of enterprise applications so that teams can focus on application-level business logic, without unnecessary ties to specific deployment environments.

The Spring Framework provides features:
1. Core technologies: dependency injection, events, resources, i18n, validation, data binding, type conversion, SpEL, AOP.
2. Testing: mock objects, TestContext framework, Spring MVC Test, WebTestClient.
3. Data Access: transactions, DAO support, JDBC, ORM, Marshalling XML.
4. Spring MVC and Spring WebFlux web frameworks.
5. Integration: remoting, JMS, JCA, JMX, email, tasks, scheduling, cache.
6. Languages: Kotlin, Groovy, dynamic languages.

## MyBatis

MyBatis comes from and is a fork of iBATIS.
iBATIS is a persistence framework which automates the mapping between SQL databases and objects in Java, .NET, and Ruby on Rails. In Java, the objects are POJOs. The mappings are decoupled from the application logic by packaging the SQL statements in XML configuration files.
In 2010, iBATIS was retired at the apache software foundation and moved to google code. Besides, it was renamed to MyBatis.

MyBatis is a first class persistence framework with support for custom SQL, stored procedures and advanced mappings. MyBatis eliminates almost all of the JDBC code and manual setting of parameters and retrieval of results. MyBatis can use simple XML or Annotations for configuration and map primitives, Map interfaces and Java POJOs (Plain Old Java Objects) to database records. 

## Maven

Apache Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information. 


# Creation Process

The basic process:
1. prepare for database;
2. create project in Eclipse;
3. modify configuration files;
4. create classes;
5. run testing for the methods in classes;
6. create web pages;
7. start server.

## Preparation for Database

Find how to install MySQL on the Internet or my [GitHub - MySQL](https://github.com/sampig/DatabaseLearning/tree/master/mysql){:target="_blank"}.

Create a database and grant privileges on a given user.
Create a table and insert some testing data into the table.

```sql
CREATE TABLE `user` (
  `user_id` INT(11) NOT NULL AUTO_INCREMENT,
  `user_name` VARCHAR(32) NOT NULL,
  `user_password` VARCHAR(32) NOT NULL,
  `user_email` VARCHAR(32) NOT NULL,
  PRIMARY KEY (`user_id`),
  KEY `idx_name` (`user_name`)
) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8;

INSERT INTO user (user_name, user_password, user_email) VALUES ('user1', 'asdfasdf', 'user1@zhuzhu.org');
INSERT INTO user (user_name, user_password, user_email) VALUES ('user2', 'asdfasdf', 'user2@zhuzhu.org');
```

## Create a Project

In Eclipse,
1. Create a Dynamic Web Project.
2. Convert the project to a Maven Project.
Right click the project: Configure --> Convert to Maven Project.
Input the GAV (groupId, artifactId, Version).
3. Create source folders for java classes, testing and web pages as shown below:
![Folder Structure]({{ site.url }}/assets/images/java_ssm/folder_structure.png)
4. Configure `pom.xml`, adding some dependencies, modifying building parameters:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.zhuzhu</groupId>
    <artifactId>name_of_project</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>war</packaging>

    <!-- Version information -->
    <properties>
        <spring.version>5.1.5.RELEASE</spring.version>
        <mybatis.version>3.4.6</mybatis.version>
        <mybatis.spring.version>1.3.2</mybatis.spring.version>
        <mysql.jdbc.version>5.1.47</mysql.jdbc.version>
        <log4j.version>2.11.1</log4j.version>
        <slf4j.version>1.7.25</slf4j.version>
        <druid.version>1.1.17</druid.version>
        <jstl.version>1.2</jstl.version>
        <jackson.version>2.9.9</jackson.version>
        <junit.version>4.12</junit.version>
        <javax.servlet.version>3.1.0</javax.servlet.version>
    </properties>

    <dependencies>
        <!-- Spring start -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aop</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aspects</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aop</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <!-- Spring end -->
        <!-- MyBatis start -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>${mybatis.version}</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>${mybatis.spring.version}</version>
        </dependency>
        <!-- MyBatis end -->
        <!-- DB start -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>${mysql.jdbc.version}</version>
        </dependency>
        <!-- DB end -->
        <!-- Log start -->
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-core</artifactId>
            <version>${log4j.version}</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>${slf4j.version}</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>${slf4j.version}</version>
        </dependency>
        <!-- Log end -->
        <!-- Druid start -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>${druid.version}</version>
        </dependency>
        <!-- Druid end -->
        <!-- JSTL start -->
        <dependency>
            <groupId>jstl</groupId>
            <artifactId>jstl</artifactId>
            <version>${jstl.version}</version>
            <scope>compile</scope>
        </dependency>
        <!-- JSTL end -->
        <!-- Jackson start -->
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-core</artifactId>
            <version>${jackson.version}</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>${jackson.version}</version>
        </dependency>
        <!-- Jackson end -->
        <!-- Test start -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>${junit.version}</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>${spring.version}</version>
            <scope>test</scope>
        </dependency>
        <!-- Test end -->
        <!-- -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>${javax.servlet.version}</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.0</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <plugin>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.2.1</version>
                <configuration>
                    <warSourceDirectory>WebContent</warSourceDirectory>
                    <webResources>
                        <resource>
                            <directory>web</directory>
                            <targetPath>web</targetPath>
                        </resource>
                    </webResources>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## Modify Configuration Files

Besides the `web.xml` in `WEB-INF`, there are some other configuration files:
![Configuration Files]({{ site.url }}/assets/images/java_ssm/configuration_files.png)

`db.properties` is used to store information about database connection. The values can be used directly by XML files after loading.
An example:

```
# Common
mysql.jdbc.driverClassName=com.mysql.jdbc.Driver
mysql.jdbc.url=jdbc:mysql://localhost:3306/[schema_name]
mysql.jdbc.username=[username]
mysql.jdbc.password=[password]
# Used in Druid
mysql.jdbc.initialSize=0
mysql.jdbc.maxActive=20
mysql.jdbc.maxIdle=20
mysql.jdbc.minIdle=1
mysql.jdbc.maxWait=60000
```

`spring-mybatis.xml` is normally used for data source bean and sql session factory bean.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="http://www.springframework.org/schema/beans 
     http://www.springframework.org/schema/beans/spring-beans.xsd
     http://www.springframework.org/schema/context
     http://www.springframework.org/schema/context/spring-context.xsd
     http://www.springframework.org/schema/aop
     http://www.springframework.org/schema/aop/spring-aop.xsd
     http://www.springframework.org/schema/tx 
     http://www.springframework.org/schema/tx/spring-tx.xsd">

    <!-- Data Source Bean -->
    <bean id="dataSource"
        class="com.alibaba.druid.pool.DruidDataSource"
        init-method="init" destroy-method="close">
        <property name="driverClassName"
            value="${mysql.jdbc.driverClassName}" />
        <property name="url" value="${mysql.jdbc.url}" />
        <property name="username"
            value="${mysql.jdbc.username}" />
        <property name="password"
            value="${mysql.jdbc.password}" />

        <!-- You could use other data source manager driver such as: class="org.springframework.jdbc.datasource.DriverManagerDataSource". If so, the properties below should be removed based on the schema of xml. -->
        <property name="initialSize"
            value="${mysql.jdbc.initialSize}" />
        <property name="maxActive"
            value="${mysql.jdbc.maxActive}" />
        <property name="maxIdle" value="${mysql.jdbc.maxIdle}" />
        <property name="minIdle" value="${mysql.jdbc.minIdle}" />
        <property name="maxWait" value="${mysql.jdbc.maxWait}" />
    </bean>

    <!-- SQL Session Factory Bean -->
    <bean id="sqlSessionFactory"
        class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource" />
        <!-- auto scan mapping xml files -->
        <property name="mapperLocations"
            value="classpath:org/zhuzhu/ssm/mapper/*.xml" />
        <!-- If there are special configurations such as alias, could add: <property name="configLocation" value="classpath:mybatis-config.xml"></property> -->
    </bean>
    <!-- DAO interfaces -->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="org.zhuzhu.ssm.dao" />
        <property name="sqlSessionFactoryBeanName"
            value="sqlSessionFactory" />
    </bean>

</beans>
```

`spring-tx.xml` is used for AOP(Aspect-oriented programming) and transaction beans.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
        http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">

    <!-- Auto scan AOP annotation -->
    <aop:aspectj-autoproxy
        proxy-target-class="true" />

    <!-- Transaction Manager -->
    <bean id="transactionManager"
        class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource" />
    </bean>

    <!-- Configure the transaction in detail. -->
    <tx:advice id="transactionAdvice"
        transaction-manager="transactionManager">
        <tx:attributes>
            <tx:method name="add*" propagation="REQUIRED"
                isolation="DEFAULT" read-only="false"
                rollback-for="Exception" />
            <tx:method name="delete*" propagation="REQUIRED"
                isolation="DEFAULT" read-only="false"
                rollback-for="Exception" />
            <tx:method name="update*" propagation="REQUIRED"
                isolation="DEFAULT" read-only="false"
                rollback-for="Exception" />
        </tx:attributes>
    </tx:advice>

    <!-- Configure AOP: auto generate proxy for targets -->
    <aop:config proxy-target-class="true">
        <aop:pointcut id="transactionPointcut"
            expression="execution(* org.zhuzhu.ssm.service..*Impl.*(..))" />
        <aop:advisor advice-ref="transactionAdvice"
            pointcut="within(org.zhuzhu.ssm.controller.*)" />
    </aop:config>

</beans>
```

`spring-mvc.xml` is used for MVC annotation and view resolver bean.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context-4.0.xsd
        http://www.springframework.org/schema/mvc
        https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!-- Auto scan components -->
    <context:component-scan
        base-package="org.zhuzhu.ssm.dao" />
    <context:component-scan
        base-package="org.zhuzhu.ssm.service" />
    <context:component-scan
        base-package="org.zhuzhu.ssm.controller" />
    <context:component-scan
        base-package="org.zhuzhu.ssm.mapper" />

    <!-- Register MVC annotation driver -->
    <mvc:annotation-driven>
        <mvc:message-converters>
            <bean
                class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
            </bean>
        </mvc:message-converters>
    </mvc:annotation-driven>
    <mvc:resources mapping="/**" location="/" />

    <!-- Configure View Resolver. -->
    <bean id="viewResolver"
        class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/"></property>
        <property name="suffix" value=".jsp"></property>
    </bean>

</beans>
```

`spring.xml` is used for

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
                        http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
                        http://www.springframework.org/schema/context
                        http://www.springframework.org/schema/context/spring-context-3.0.xsd">

    <!-- Load properties configuration file. -->
    <context:property-placeholder
        location="classpath:db.properties" />
    <!-- Autowired Annotaion Bean -->
    <bean
        class="org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor" />

    <!-- if you want to only load a single spring configuration file, you could import all other files here. -->
    <import resource="spring-mvc.xml" />
    <import resource="spring-mybatis.xml" />
    <import resource="spring-tx.xml" />
</beans>
```

`log4j2.xml` is the configuration file for Log4j2. In the previous version of Log4j, the configuration file is `log4j.properties`.
You could set the output way of log, its level, its output format and so on.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE log4j:configuration PUBLIC "-//APACHE//DTD LOG4J 1.2//EN" "http://logging.apache.org/log4j/1.2/apidocs/org/apache/log4j/xml/doc-files/log4j.dtd">
<Configuration status="WARN">
    <Appenders>
        <Console name="Console" target="SYSTEM_OUT">
            <PatternLayout
                pattern="%d{YYYY-MM-dd HH:mm:ss} [%t] %-5p %c{1}:%L - %msg%n" />
        </Console>
        <RollingFile name="RollingFile"
            filename="log/test.log"
            filepattern="${logPath}/%d{YYYYMMddHHmmss}-rolling.log">
            <PatternLayout
                pattern="%d{YYYY-MM-dd HH:mm:ss} [%t] %-5p %c{1}:%L - %msg%n" />
            <Policies>
                <SizeBasedTriggeringPolicy
                    size="100 MB" />
            </Policies>
            <DefaultRolloverStrategy max="20" />
        </RollingFile>
    </Appenders>
    <Loggers>
        <Root level="info">
            <AppenderRef ref="Console" />
            <AppenderRef ref="RollingFile" />
        </Root>
    </Loggers>
</Configuration>
```

Finally, `web.xml` also needs to be modified.

```xml
...
    <!-- Load spring configuration files. -->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:spring.xml</param-value>
    </context-param>

    <!-- Servlet Context Listener -->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    <listener>
        <listener-class>org.springframework.web.util.IntrospectorCleanupListener</listener-class>
    </listener>

    <!-- Encoding Filter -->
    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>
    <!-- Encoding filter for jsp page -->
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <!-- Front-end controller servlet -->
    <servlet>
        <servlet-name>springMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:spring-mvc.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springMVC</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

    <!-- Logging -->
    <context-param>
        <!-- Log Profile Path -->
        <param-name>log4jConfigLocation</param-name>
        <param-value>classpath:log4j2.xml</param-value>
    </context-param>
    <context-param>
        <!-- Refresh intervals for log pages -->
        <param-name>log4jRefreshInterval</param-name>
        <param-value>6000</param-value>
    </context-param>
    <context-param>
        <param-name>controller</param-name>
        <param-value>controller-log</param-value>
    </context-param>
    <context-param>
        <param-name>loggingLevel</param-name>
        <param-value>info</param-value>
    </context-param>
    <listener>
        <listener-class>org.apache.logging.log4j.web.Log4jServletContextListener</listener-class>
    </listener>
...
```

`UserMapper.xml` is the mapper file to map a table in the database to a model class.
We could also configure SQL statements for the methods in the DAO class.
An example is shown below:

```xml
<?xml version="1.0" encoding="UTF-8" ?>    
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<mapper namespace="org.zhuzhu.ssm.dao.UserDao">
    <resultMap id="userResultMap"
        type="org.zhuzhu.ssm.model.User">
        <id property="userId" column="user_id" />
        <result property="userName" column="user_name" />
        <result property="userPassword" column="user_password" />
        <result property="userEmail" column="user_email" />
    </resultMap>
    <select id="listAllUsers" resultMap="userResultMap">
        SELECT user_id,
        user_name, user_password, user_email
        FROM user;
    </select>
    <select id="getUser" parameterType="java.lang.Integer"
        resultMap="userResultMap">
        SELECT user_id, user_name, user_password, user_email
        FROM user
        WHERE user_id=#{id,jdbcType=INTEGER};
    </select>
    <insert id="saveUser"
        parameterType="org.zhuzhu.ssm.model.User"
        useGeneratedKeys="true" keyColumn="user_id" keyProperty="userId">
        INSERT
        INTO user(user_name, user_password,
        user_email)
        VALUES(#{userName,jdbcType=VARCHAR},
        #{userPassword,jdbcType=VARCHAR},
        #{userEmail,jdbcType=VARCHAR});
    </insert>
    <update id="updateUser"
        parameterType="org.zhuzhu.ssm.model.User">
        UPDATE user SET
        user_name=#{userName,jdbcType=VARCHAR},
        user_password=#{userPassword,jdbcType=VARCHAR},
        user_email=#{userEmail,jdbcType=VARCHAR}
        WHERE
        user_id=#{userId,jdbcType=INTEGER};
    </update>
    <delete id="deleteUser" parameterType="java.lang.Integer">
        DELETE FROM user WHERE
        user_id=#{id,jdbcType=INTEGER}
    </delete>
</mapper>
```

## Create Classes

After creating and modifying the configuration files, the next step is to start coding and to write classes.

We would like to put different types of classes in different packages like:
![Classes Structure]({{ site.url }}/assets/images/java_ssm/classes_structure.png)

`User.java` is the Entity class mapping from the `user` table.

```java
package org.zhuzhu.ssm.model;

public class User {

  private Integer userId;
  private String userName;
  private String userPassword;
  private String userEmail;

  public User(Integer userId, String userName, String userPassword, String userEmail) {
    super();
    this.userId = userId;
    this.userName = userName;
    this.userPassword = userPassword;
    this.userEmail = userEmail;
  }

  public Integer getUserId() {
    return userId;
  }

  public void setUserId(Integer userId) {
    this.userId = userId;
  }

  public String getUserName() {
    return userName;
  }

  public void setUserName(String userName) {
    this.userName = userName;
  }

  public String getUserPassword() {
    return userPassword;
  }

  public void setUserPassword(String userPassword) {
    this.userPassword = userPassword;
  }

  public String getUserEmail() {
    return userEmail;
  }

  public void setUserEmail(String userEmail) {
    this.userEmail = userEmail;
  }

  @Override
  public String toString() {
    return String.format("User [userId=%s, userName=%s, userEmail=%s]", userId, userName,
        userEmail);
  }

}
```

`UserDao.java` is the DAO of user. It is an interface for data access.

```java
package org.zhuzhu.ssm.dao;

import java.util.List;

import org.zhuzhu.ssm.model.User;

public interface UserDao {

  List<User> listAllUsers();

  User getUser(Integer id);

  void saveUser(User user);

  void updateUser(User user);

  void deleteUser(Integer id);

}
```

`UserService.java` is the service interface.

```java
package org.zhuzhu.ssm.service;

import java.util.List;

import org.zhuzhu.ssm.model.User;

public interface UserService {

  List<User> listAllUsers();

  User getUser(Integer id);

  void saveUser(User user);

  User updateUser(User user);

  void deleteUser(Integer id);

}
```

`UserServiceImpl.java` is the implementation of `UserService`.

```java
package org.zhuzhu.ssm.service.impl;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.zhuzhu.ssm.dao.UserDao;
import org.zhuzhu.ssm.model.User;
import org.zhuzhu.ssm.service.UserService;

@Service("userService")
public class UserServiceImpl implements UserService {

  @Autowired
  private UserDao userDao;

  @Override
  public List<User> listAllUsers() {
    return userDao.listAllUsers();
  }

  @Override
  public User getUser(Integer id) {
    return userDao.getUser(id);
  }

  @Override
  public void saveUser(User user) {
    userDao.saveUser(user);
  }

  @Override
  public User updateUser(User user) {
    userDao.updateUser(user);
    return userDao.getUser(user.getUserId());
  }

  @Override
  public void deleteUser(Integer id) {
    userDao.deleteUser(id);
  }

}
```

`UserController.java` is the controller for url request handler.

```java
package org.zhuzhu.ssm.controller;

import java.util.HashMap;
import java.util.List;
import java.util.Map;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.ResponseBody;
import org.zhuzhu.ssm.model.User;
import org.zhuzhu.ssm.service.UserService;

@Controller
@RequestMapping(value = "/user")
public class UserController {

  @Autowired
  private UserService userService;

  @RequestMapping("list")
  public String listAllUsers(HttpServletRequest request) {
    List<User> userList = userService.listAllUsers();
    request.setAttribute("userList", userList);
    return "web/user_list";
  }

  @ResponseBody
  @RequestMapping(value = "/listUsers", method = {RequestMethod.POST, RequestMethod.GET})
  public Object listAllUsers(HttpServletRequest request, HttpServletResponse response) {
    List<User> userList = userService.listAllUsers();
    Map<String, Object> map = new HashMap<>(0);
    map.put("users", userList);
    return map;
  }

  @ResponseBody
  @RequestMapping(value = "/getUser", method = {RequestMethod.POST, RequestMethod.GET})
  public Object getUser(Integer id) {
    User user = userService.getUser(id);
    Map<String, Object> map = new HashMap<>(0);
    map.put("user", user);
    return map;
  }

  @ResponseBody
  @RequestMapping(value = "/addUser", method = {RequestMethod.POST, RequestMethod.GET})
  public Object insertUser(User user) {
    Map<String, Object> result = new HashMap<String, Object>();
    try {
      userService.saveUser(user);
      result.put("success", true);
      result.put("user", user);
      return result;
    } catch (Exception e) {
      e.printStackTrace();
      result.put("success", false);
      return result;
    }
  }

  @ResponseBody
  @RequestMapping(value = "/editUser", method = {RequestMethod.POST, RequestMethod.GET})
  public Object editUser(User user) {
    Map<String, Object> result = new HashMap<String, Object>();
    try {
      userService.updateUser(user);
      result.put("success", true);
      result.put("user", user);
      return result;
    } catch (Exception e) {
      e.printStackTrace();
      result.put("success", false);
      return result;
    }
  }


  @ResponseBody
  @RequestMapping(value = "/deleteUser", method = {RequestMethod.POST, RequestMethod.GET})
  public Object deleteUser(Integer id) {
    Map<String, Object> result = new HashMap<String, Object>();
    try {
      userService.deleteUser(id);
      result.put("success", true);
      result.put("userid", id);
      return result;
    } catch (Exception e) {
      e.printStackTrace();
      result.put("success", false);
      return result;
    }
  }

}
```

## Run Functional Testing

Write some test cases for the methods in the classes of service layer using jUnit.

![Java Test Structure]({{ site.url }}/assets/images/java_ssm/java_test_structure.png)

`BaseTestCase.java` is an abstract class of all the test cases for loading configuration and other usages.

```java
package org.zhuzhu.ssm;

import org.junit.runner.RunWith;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.AbstractJUnit4SpringContextTests;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
import org.springframework.test.context.web.WebAppConfiguration;

@ContextConfiguration(locations = {"classpath:spring.xml"})
@RunWith(SpringJUnit4ClassRunner.class)
@WebAppConfiguration("src/main/resources")
public abstract class BaseTestCase extends AbstractJUnit4SpringContextTests {

  protected Logger logger = LoggerFactory.getLogger(getClass());

}
```

`UserServiceTest.java` is the test for `UserService` and its implementation.

```java
package org.zhuzhu.ssm.service;

import static org.junit.Assert.assertTrue;

import java.util.List;
import java.util.logging.Level;
import java.util.logging.Logger;

import org.junit.FixMethodOrder;
import org.junit.Test;
import org.junit.runners.MethodSorters;
import org.springframework.beans.factory.annotation.Autowired;
import org.zhuzhu.ssm.BaseTestCase;
import org.zhuzhu.ssm.model.User;

@FixMethodOrder(MethodSorters.NAME_ASCENDING)
public class UserServiceTest extends BaseTestCase {

  @Autowired
  private UserService userService;

  Logger logger = Logger.getLogger(UserServiceTest.class.getName());

  @Test
  public void tc1_listAllUsers() {
    List<User> list = userService.listAllUsers();
    logger.log(Level.INFO, "Users: " + list.size());
    for (User user : list) {
      logger.log(Level.INFO, "User: " + user);
    }
    assertTrue(list.size() > 0);
  }

  @Test
  public void tc2_getUser() {
    Integer id = 11;
    User user = userService.getUser(id);
    logger.log(Level.INFO, "Get user: " + user);
    assertTrue("user1".contentEquals(user.getUserName()));
  }

  @Test
  public void tc3_insertUser() {
    User user = new User("test_user", "testcase", "test@test.com");
    userService.saveUser(user);
    logger.log(Level.INFO, "Insert new user: " + user);
    List<User> list = userService.listAllUsers();
    logger.log(Level.INFO, "Users after insertion: " + list.size());
  }

  @Test
  public void tc4_updateUser() {
    List<User> list = userService.listAllUsers();
    User user = list.get(list.size() - 1);
    logger.log(Level.INFO, "User updated before: " + user);
    user.setUserName("updated");
    User newUser = userService.updateUser(user);
    logger.log(Level.INFO, "User updated after: " + newUser);
  }

  @Test
  public void tc5_deleteUser() {
    List<User> list = userService.listAllUsers();
    int size = list.size();
    logger.log(Level.INFO, "Users before deletion: " + size);
    User user = list.get(size - 1);
    userService.deleteUser(user.getUserId());
    list = userService.listAllUsers();
    int newSize = list.size();
    logger.log(Level.INFO, "Users after deletion: " + newSize);
    assertTrue(newSize == size - 1);
  }

}
```

So that you don't need to start the server to test the methods in classes.

## Create Web Pages

Create JSPs, JS, CSS and other files in the folder for the front-end.

![Web Pages Structure]({{ site.url }}/assets/images/java_ssm/web_pages_structure.png)

`user_list.jsp` is an example page for user listing, adding, editing and deleting.
Only main parts in the page are shown below:

```html
...
<script>
...
    function addUser() {
        jQuery.ajax({
            url : "${path}/user/addUser",
            type : "POST",
            data : $("#addForm").serialize(),
            dataType : 'json',
            success : function(msg) {
                if (msg.success) {
                    console.log(msg.user);
                    $("#userinfo").empty();
                    $("#userinfo").append(msg.user);
                    getList();
                } else {
                    console.log("error!");
                }
            }
        });
    }
...
    function showUser(id) {
        jQuery.ajax({
            url: "${path}/user/getUser",
            type: "POST",
            data: {id:id},
            dataType: "json",
            success: function (msg) {
                    var user = msg.user;
                    cleanForm();
                    $("#userid").val(user.userId);
                    $("#username").val(user.userName);
                    $("#password").val(user.userPassword);
                    $("#email").val(user.userEmail);
            }
        });
    }
    function editUser() {
        jQuery.ajax({
            url: "${path}/user/editUser",
            type: "POST",
            data: $("#addForm").serialize(),
            dataType: "json",
            success: function (msg) {
                if (msg.success) {
                    console.log(msg.user);
                    $("#userinfo").empty();
                    $("#userinfo").append(msg.user);
                    getList();
                } else {
                    console.log("error!");
                }
            }
        });
    }
    function deleteUser(id) {
...
                jQuery.ajax({
                    url: "${path}/user/deleteUser",
                    type: "POST",
                    data:{id:id},
                    dataType: "json",
                    success: function (msg) {
                        if(msg.success){
                            console.log("Succeed to delete.");
                            swal("Success");
                            getList();
                        }else{
                            console.log("Failed to delete.");
                            swal("Failed");
                        }
                    }
                });
...
    }
...
</script>
...
    <!-- List users -->
    <div>
        <table>
            <tbody>
                <tr>
                    <th>Username</th>
                    <th>Email</th>
                </tr>
                <c:if test="${!empty userList }">
                    <c:forEach items="${userList}" var="user">
                        <tr>
                            <td><a target="_self"
                                onclick="showUser(${user.userId })">${user.userName }</a></td>
                            <td>${user.userEmail }</td>
                        </tr>
                    </c:forEach>
                </c:if>
            </tbody>
        </table>
    </div>
...
```

## Start Server

Start the tomcat and visit the website with "http://<URL_PATH>/user/list" in browser.


# Summary

In this blog, I only introduce the main processes and files about how to create an SSM project with Maven in Eclipse.
If you want to know more detail or have any questions, send email to me.
I would like to give some helps.


# References

1. [Spring Framework Documentation](https://docs.spring.io/spring/docs/current/spring-framework-reference/index.html){:target="_blank"}
2. [Spring Web MVC](https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc){:target="_blank"}
3. [MyBatis Documentation](http://www.mybatis.org/mybatis-3/){:target="_blank"}
4. [MyBatis-Spring Documentation](http://www.mybatis.org/spring/index.html){:target="_blank"}
5. [MvnRepository](https://mvnrepository.com/){:target="_blank"}
