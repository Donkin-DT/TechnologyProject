###### Spring 与 SpringMVC整合

###### 步骤 

```java
/* 1.1 整合Spring到项目中 */
	//1.1.1 拷贝相关jar包
			IOC
				commons-logging-1.1.3.jar
				spring-beans-4.0.0.RELEASE.jar
				spring-context-4.0.0.RELEASE.jar
				spring-core-4.0.0.RELEASE.jar
				spring-expression-4.0.0.RELEASE.jar
					
			AOP
				com.springsource.net.sf.cglib-2.2.0.jar
				com.springsource.org.aopalliance-1.0.0.jar
				com.springsource.org.aspectj.weaver-1.6.8.RELEASE.jar
				spring-aop-4.0.0.RELEASE.jar
				spring-aspects-4.0.0.RELEASE.jar
					
			TX
				spring-jdbc-4.0.0.RELEASE.jar
				spring-orm-4.0.0.RELEASE.jar
				spring-tx-4.0.0.RELEASE.jar	
				c3p0-0.9.1.2.jar
				mysql-connector-java-5.1.7-bin.jar	
                    
			WEB
				spring-web-4.0.0.RELEASE.jar
					
			其他包：
				upload：	
					commons-fileupload-1.2.1.jar
					commons-io-2.0.jar				
				Jackson:
					jackson-annotations-2.1.5.jar
					jackson-core-2.1.5.jar
					jackson-databind-2.1.5.jar
				JSTL:
					jstl.jar
					standard.jar						
				
	//1.1.2 创建Spring配置文件
				扫描包
				加载properties属性文件
				数据源
				声明式事务			
		
	//1.1.3 在web.xml中声明监听器，用于创建IOC容器
					
/*1.2 整合SpringMVC到项目中*/
	
	//1.2.1 拷贝相关jar包
		spring-webmvc-4.0.0.RELEASE.jar
		
	//1.2.2 创建SpringMVC配置文件
			扫描包
			视图解析器
			文件上传解析器
			异常解析器
			拦截器
			处理静态资源和映射配置
		
	//1.2.3 在web.xml中声明核心控制器，以及相关过滤器（REST,Encoding）
		
/* 1.3 整合原理 */
	Spring框架主要管理数据源，事务，Service和Dao
	SpringMVC主要管理相关解析器，拦截器，Controller
	根据整合观察发现：Spring和SpringMVC两个框架都存在 IOC容器，都来管理Controller和Service ,这是存在一定问题的。
			
	需要将Controller和Service分别由两个容器进行管理：
		Spring管理Service,Dao 
		SpringMVC管理Controller
			
	解决办法：设置扫描包过滤。
		Spring配置：	
				<!-- 设置扫描包:Spring框架管理Service和dao,不再扫描@Controller注解所声明的类 -->
				<context:component-scan base-package="com.atguigu.ss">
					<context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
				</context:component-scan>
		
		SpringMVC配置：
				<!-- 扫描包:SpringMVC框架只管理@Controller注解声明类，Service和DAO不再管理了。
					use-default-filters="false" 表示取消默认扫描规则。默认扫描规则是对指定包以及子包全部进行扫描。-->
				<context:component-scan base-package="com.atguigu.ss" use-default-filters="false">
				<context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
				</context:component-scan>
```

###### 1.jar包 

```java
c3p0-0.9.1.2.jar
com.springsource.net.sf.cglib-2.2.0.jar
com.springsource.org.aopalliance-1.0.0.jar
com.springsource.org.aspectj.weaver-1.6.8.RELEASE.jar
commons-fileupload-1.2.1.jar
commons-io-2.0.jar
commons-logging-1.1.3.jar
jackson-annotations-2.1.5.jar
jackson-core-2.1.5.jar
jackson-databind-2.1.5.jar
jstl.jar
mysql-connector-java-5.1.7-bin.jar
spring-aop-4.0.0.RELEASE.jar
spring-aspects-4.0.0.RELEASE.jar
spring-beans-4.0.0.RELEASE.jar
spring-context-4.0.0.RELEASE.jar
spring-core-4.0.0.RELEASE.jar
spring-expression-4.0.0.RELEASE.jar
spring-jdbc-4.0.0.RELEASE.jar
spring-orm-4.0.0.RELEASE.jar
spring-tx-4.0.0.RELEASE.jar
spring-web-4.0.0.RELEASE.jar
spring-webmvc-4.0.0.RELEASE.jar
standard.jar
```

###### 2.web.xml 😀

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" id="WebApp_ID" version="2.5">
  <display-name>SpringAndSpringMVC</display-name>
  	
	  <!-- ★ 应用上下文参数，给ContextLoaderListener监听器提供参数，用于创建IOC容器。 -->
	  <context-param>
	  	<param-name>contextConfigLocation</param-name>
	  	<param-value>classpath:/spring.xml</param-value>
	  </context-param>
	  
	  <!-- ★ 创建ContextLoaderListener监听器：
	  	在服务器启动时，用于创建IOC容器 XmlWebApplicationContext
	  	框架将IOC容器存放到application域中。
	  	如果希望使用IOC容器对象，可以通过工具类获取：
	  	ApplicataionContext ioc = WebApplicationContextUtils.getWebApplicationContext(application);
	  -->
	  <listener>
	  	<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	  </listener>
  
  
	  <!-- ★ 配置处理中文乱码问题 filter 过滤器 -->
	  <filter>
	  	<filter-name>CharacterEncodingFilter</filter-name>
	  	<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
	  	<!-- 配置字符集编码格式： -->
	  	<init-param>
			<param-name>encoding</param-name>
			<param-value>UTF-8</param-value>
	  	</init-param>
	  	<!-- 配置请求和返回为同一字符集编码格式： -->
	  	<init-param>
	  		<param-name>forceEncoding</param-name>
	  		<param-value>true</param-value>
	  	</init-param>
	  </filter>
	  <!-- 配置处理中文乱码问题 filter 过滤器映射 -->
	  <filter-mapping>
	  	<filter-name>CharacterEncodingFilter</filter-name>
	  	<!-- 配置对所有的请求进行字符集编码： -->
	  	<url-pattern>/*</url-pattern>
	  </filter-mapping>

	  
	  <!-- ★配置RESTFul模式请求过滤器filter
	  	          支持REST风格：将POST请求转换为PUT 或 DELETE -->
	  <filter>
	  	<filter-name>HiddenHttpMethodFilter</filter-name>
	  	<filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
	  </filter>
	  <!-- 配置请求过滤器filter映射 -->
	  <filter-mapping>
	  	<filter-name>HiddenHttpMethodFilter</filter-name>
	  	<!-- 配置对所有的请求都过滤 -->
	  	<url-pattern>/*</url-pattern>
	  </filter-mapping>
	  
	  <!-- ★ 配置核心控制器 -->
		<servlet>
			<servlet-name>springDispatcherServlet</servlet-name>
			<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
			<init-param>
				<param-name>contextConfigLocation</param-name>
				<!-- 配置核心控制器配置文件 -->
				<param-value>classpath:/spring-mvc.xml</param-value>
			</init-param>
			<load-on-startup>1</load-on-startup>
		</servlet>
		<!-- 配置核心控制器映射 -->
		<servlet-mapping>
			<servlet-name>springDispatcherServlet</servlet-name>
			<!-- 配置对所有的请求都控制 -->
			<url-pattern>/</url-pattern>
		</servlet-mapping>
  		
  	  <!-- ★ 配置WEB动态项目在启动时寻找的直接访问的首页 -->
	  <welcome-file-list>
	    <welcome-file>index.html</welcome-file>
	    <welcome-file>index.jsp</welcome-file>
	  </welcome-file-list>
	  
</web-app>
```

###### 3.spring.xml 😀

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:tx="http://www.springframework.org/schema/tx"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.0.xsd
		http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-4.0.xsd">

	<!-- 导入外部数据库配置资源文件 -->
	<context:property-placeholder location="classpath:/db.properties"/>
	
	<!-- 配置 C3PO 数据源 -->
	<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
		<property name="user" value="${jdbc.user}"></property>
		<property name="password" value="${jdbc.password}"></property>
		<property name="jdbcUrl" value="${jdbc.jdbcUrl}"></property>
		<property name="driverClass" value="${jdbc.driverClass}"></property>
		
		<!-- 配置数据源初始化值： -->
		<property name="initialPoolSize" value="${jdbc.initialPoolSize}"></property>
		<property name="minPoolSize" value="${jdbc.minPoolSize}"></property>
		<property name="maxPoolSize" value="${jdbc.maxPoolSize}"></property>
	</bean>
	
	
	<!-- 配置JdbcTemplate -->
	<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
		<!-- 配置管理的数据源 -->
		<property name="dataSource" ref="dataSource"></property>
	</bean>
	
	
	<!-- 设置扫描包:Spring框架管理Service和dao,不再扫描@Controller注解所声明的类 -->
	<context:component-scan base-package="com.atguigu.sasmvc">
		<!-- 配置需要排除的扫描包，
			注意：
			表达式填写的是注解的包即：org.springframework.stereotype.Controller -->
		<context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
	</context:component-scan>

	
	<!-- 配置数据源事务管理器 -->
	<!-- <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
		配置事务管理的数据源
		<property name="dataSource" ref="dataSource"></property>
	</bean> -->
	<!-- 启用事务注解 -->
	<!-- <tx:annotation-driven transaction-manager="transactionManager"/> -->
	
	
	<!-- 事务管理器：切面类 -->
	<bean  id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
		<property name="dataSource" ref="dataSource"></property>
	</bean>
	
	<aop:config>
		<!-- 全局切入点表达式，注意：事务一定是加在业务层 -->
		<aop:pointcut id="pointcutId" expression="execution(* com.atguigu..service.*Service.*(..))"/>
		<!-- 将切入点表达式和通知关联在一起 -->
		<aop:advisor advice-ref="txAdviceId" pointcut-ref="pointcutId"/>
	</aop:config>
	
	<!-- 事务通知 -->
	<tx:advice id="txAdviceId" transaction-manager="transactionManager">
		<tx:attributes>
			<tx:method name="*" propagation="REQUIRED" isolation="REPEATABLE_READ" rollback-for="java.lang.Exception"/>
			<tx:method name="query*" read-only="true"/>
			<tx:method name="get*" read-only="true"/>
		</tx:attributes>
	</tx:advice>
</beans>
```

###### 4.spring-mvc.xml 😀

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xsi:schemaLocation="http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd
		http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd">
    
	
	<!-- ★扫描包:SpringMVC框架只管理@Controller注解声明类，Service和DAO不再管理了。
	     use-default-filters="false" 表示取消默认扫描规则。默认扫描规则是对指定包以及子包全部进行扫描。-->
	<context:component-scan base-package="com.atguigu.sasmvc" use-default-filters="false">
		<!-- 设置需要包含的扫描包 -->
		<context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
	</context:component-scan>

	
	<!-- ★配置视图解析器 -->
	<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<!-- 配置视图解析器的目标页面路径： -->
		<property name="prefix" value="/WEB-INF/jsp/"></property>
		<!-- 配置视图解析器解析为何类型的页面： -->
		<property name="suffix" value=".jsp"></property>
	</bean>
	
	
	<!-- ★ 配置动态WEB项目使用静态资源 -->
	<mvc:default-servlet-handler/>
    
	
	<!-- ★ 配置使用静态资源后的映射找不到问题 -->
	<mvc:annotation-driven/>
	
	
	<!-- ★ 配置文件上传解析器（文件下载直接用静态或动态下载即可） -->
	<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
		<!-- 配置文件上传解析器的编码格式 -->
		<property name="defaultEncoding" value="UTF-8"></property>
		<!-- 配置资源上传的最大字节:100M -->
		<property name="maxUploadSize" value="102400"></property>
	</bean>
	
	
	<!-- ★ 配置拦截器：
		需要继承HandlerInterceptorAdapter 拦截适配器
		或实现HandlerInterceptor接口
		①只会拦截请求，不会拦截jsp而filter什么都会拦截，包括jsp页面 
	    ②与配置其他bean不一样，一个项目中可以有多个拦截器：执行的顺序和配置的顺序一致 -->
	<mvc:interceptors>
		<!-- 配置的第一个拦截器： -->
		<bean id="firstInterceptor" class="com.atguigu.sasmvc.springmvc.interceptor.FirstInterceptor"></bean>
	</mvc:interceptors>
	
	<!-- ★ 配置框架的异常解析器(SimpleMappingExceptionResolver)
		作用：就不用在Controller控制器中写try{}cathch(){}finally{}语句；
		但是不能处理页面上的异常，需要在jsp页面中指定errorPage="/WEN-INF/jsp/error.jsp" -->
	<bean id="handlerExceptionResolver" class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
		<!-- 配置解析器解析哪些异常并转发到指定的错误页面
			可以指定多个异常类，也可以直接指定最大的运行异常Exception  -->
		<property name="exceptionMappings">
			<props>
				<!-- 指定解析的异常和转发的错误页面，会根据视图解析器指定的路径和文件类型去找指定的错误页面 -->
				<prop key="java.lang.Exception">error</prop>
			</props>
		</property>
	</bean>
	
</beans>
```

###### 5.db.properties 😀

```properties
jdbc.user=root
jdbc.password=1234
jdbc.jdbcUrl=jdbc:mysql://127.0.0.1:3306/sasmvc
jdbc.driverClass=com.mysql.jdbc.Driver

jdbc.initialPoolSize=5
jdbc.minPoolSize=10
jdbc.maxPoolSize=20
```

###### 6.src

```java
com.atguigu.sasmvc
	com.atguigu.sasmvc.spring
		com.atguigu.sasmvc.spring.bean
			Address.java
			Department.java
			Employee.java
			
		com.atguigu.sasmvc.spring.dao
			EmployeeDao.java
			com.atguigu.sasmvc.spring.dao.impl
				EmployeeDaoImpl.java
			
		com.atguigu.sasmvc.spring.service
			EmployeeService.java
			com.atguigu.sasmvc.spring.service.impl
				EmployeeServiceImpl.java
		
	com.atguigu.sasmvc.springmvc
		com.atguigu.sasmvc.springmvc.controller
			EmployeeController.java
			com.atguigu.sasmvc.springmvc.controller.Impl
				EmployeeControllerImpl.java
				
		com.atguigu.sasmvc.springmvc.interceptor
			FirstInterceptor.java
			
	com.atguigu.sasmvc.test
		SpringMVCTest.java
```

###### db.sql 😀

```mysql
/* 删除 employee 库*/
DROP DATABASE IF EXISTS sasmvc;

/* 创建 sasmvc 库*/
CREATE DATABASE IF NOT EXISTS sasmvc;
	
/* 创建 employee 表*/
CREATE TABLE IF NOT EXISTS employee(id INT PRIMARY KEY AUTO_INCREMENT,lastName VARCHAR(20) NOT NULL ,
					age INT CHECK(age BETWEEN 1 AND 130),
					gender CHAR DEFAULT '男',email VARCHAR(20) UNIQUE,salary DOUBLE(8,2));					

/* 创建 department 表*/	
CREATE TABLE IF NOT EXISTS department(departmentId INT UNIQUE NOT NULL DEFAULT '1',departmentName VARCHAR(20) NOT NULL UNIQUE )	;

/* 创建 address 表*/
CREATE TABLE IF NOT EXISTS address(addressId INT UNIQUE NOT NULL,
				nation VARCHAR(20) DEFAULT '中国',
				province VARCHAR(20) DEFAULT '四川',
				city VARCHAR(20) DEFAULT '成都');
	
-- 查看 employee 表
SELECT * FROM employee;

-- 查看 department 表
SELECT * FROM department;

-- 查看 address 表
SELECT * FROM address;

# 插入 employee 第一条数据
INSERT INTO employee(id,lastname,age,gender,email,salary) VALUES
							(1,'donkin',27,'男','donkin@163.com',20000.00),
							(2,'潘星宇',24,'女','pxy@163.com',18000.00);

# 插入 department 第一条数据
INSERT INTO department VALUE(1,'董事会');

# 插入 address 第一条数据
INSERT INTO address VALUE(1,'中国','四川','成都');		
```