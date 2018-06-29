##### ServletRequest获取请求参数值

index.html

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Http協議練習</title>
</head>
<body>
	<form action = "loginServlet" method = "post">
		登錄名：<input type = "text" name="userName"/>
		<br>
		密碼:<input type = "password" name = "password"/>
		<br>
		<input type = "submit" value="登錄"/>
		<br>
		興趣愛好:
		<input type="checkbox" name="interesting" value ="football"/>football
		<input type="checkbox" name="interesting" value ="tennies"/>tennies
		<input type="checkbox" name="interesting" value ="films"/>films
		<input type="checkbox" name="interesting" value ="musics"/>musics
		<input type="checkbox" name="interesting" value ="mountain"/>mountain
		<input type="checkbox" name="interesting" value ="visit"/>visit
	</form>
</body>
</html>
```

web.xml

```java
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="http://java.sun.com/xml/ns/javaee"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
	id="WebApp_ID" version="2.5">
	<servlet>
		<servlet-name>LoginServlet</servlet-name>
		<servlet-class>com.atguigu.javaweb.servlets.LoginServlet</servlet-class>
	</servlet>
	
	<servlet-mapping>
		<servlet-name>LoginServlet</servlet-name>
		<url-pattern>/loginServlet</url-pattern>
	</servlet-mapping>
</web-app>
```

LoginServlet.java

```java
package com.atguigu.javaweb.servlets;

import java.io.IOException;
import java.util.Arrays;
import java.util.Enumeration;
import java.util.Map;

import javax.servlet.Servlet;
import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;

public class LoginServlet implements Servlet {

	@Override
	public void destroy() {
		// TODO Auto-generated method stub
		
	}

	@Override
	public ServletConfig getServletConfig() {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public String getServletInfo() {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public void init(ServletConfig arg0) throws ServletException {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void service(ServletRequest request, ServletResponse response)
			throws ServletException, IOException {
        //1、获取指定参数名的参数值：
		String name = request.getParameter("userName");
		String password = request.getParameter("password");
		System.out.println("姓名：" + name);
		System.out.println("密碼：" + password);
		String interesting = request.getParameter("interesting");
		System.out.println("興趣愛好：" + interesting );
		
		//2、获取指定参数名的多个值，并以数组的形式存储
		String[] interestings = request.getParameterValues("interesting");
		for(String interest:interestings){
			System.out.println("---" + interest);
		}
		
		//3、枚举的方式：一次性将所有的 参数名 获取到
		Enumeration<String> names = request.getParameterNames();
		while(names.hasMoreElements()){
			String name = names.nextElement();
			String val = request.getParameter(name);
			System.out.println(name + ":" + val);
		}
		
		//4、Map键值对方式：一次性获取所有的 参数名 和 参数值，有多个值的参数将用数组存储：
		Map<String,String[]> map = request.getParameterMap();
		for(Map.Entry<String,String[]> entry:map.entrySet()){
			System.out.println(entry.getKey() + Arrays.asList(entry.getValue()));
		}
		
		//5、获取与URL有关的参数：
		HttpServletRequest httpServletRequest = (HttpServletRequest) request;
		//5.1获取URI
		String uri = httpServletRequest.getRequestURI();
		System.out.println("URI ：" + uri);  //URI ：/Test426/loginServlet
		
		//5.2获取请求方式；
		String method = httpServletRequest.getMethod();
		System.out.println("请求方式为：" + method);// 请求方式为：POST
		
		//5.3修改 请求方式为get之后可以进行获取 URL地址中的 ？号之后的参数：前提条件是必须要将请求方式改为get
		String getMethod = httpServletRequest.getMethod();
		System.out.println("请求方式为：" + getMethod);// 请求方式为：GET
		String queryString = httpServletRequest.getQueryString();// URL：http://localhost:8080/Test426/loginServlet?userName=atguigu&password=123456
		System.out.println("queryString:" + queryString);//queryString: userName=atguigu&password=123456
		//5.4获取servlet的名字：
		String servletPath = httpServletRequest.getServletPath();
		System.out.println("serlet的名字是；" + servletPath);//serlet的名字是；/loginServlet
	}
}
```
LoginServlet2.java

实际开发写的Servlet继承HttpServlet。

```java
package com.atguigu.javaweb;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class LoginServlet2 extends HttpServlet{
	
	/**
	 * 
	 */
	private static final long serialVersionUID = 1L;

	@Override
	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		
		String userName = request.getParameter("userName");
		String password = request.getParameter("password");
		
		//继承 HttpServlet的servlet类之后，用以下方法访问web.xml文档中 的初始化参数：
		//getServletContext().getInitParameter("user");
		String user = getServletContext().getInitParameter("user");
		String password2= getServletContext().getInitParameter("password");
		
		PrintWriter out = response.getWriter();
		
		if(userName.equals(user) && password.equals(password2)){
			out.print("Hello  " + userName + " Succeed!");
		}else{
			out.print("Failure!");
		}
	}
}

```

