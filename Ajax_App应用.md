#####Ajax_App应用程序#####
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>第一个Ajax_App应用</title>
<script type="text/javascript" src="scripts/jquery-1.5.2.js"></script>

<!-- src="{pageContext.request.contextPath }/scripts/jquery-1.5.2.js" 中
这个 pageContext.request.contextPath 的理解和设置-->

<script type="text/javascript">
	$(function(){
		$(":input[name='userName']").change(function(){
			var val = $(this).val();
			val = $.trim(val);
			
			if(val != ""){
				var	url = "valiateUserName";//pageContext.request.contextPath/valiateUserName 这个绝对路径的理解
				/*访问后台的步骤：
					在项目中找到“Java Resource” 文件夹 打开点击“src”文件夹
					新建一个servlet小程序：
						设置类的存储在哪个包中;
						设置servlet小程序的类为：ValiateUserNameServlet；
						点击next，设置小程序（servlet类）的url（URL Mappings）映射名字为前端的url中的文件名
						点击next勾选Ajax方法doPost等等
						再继续编写ValiateUserNameServlet.java类中的方法等等
				*/
				var args = {"userName":val,"time":new Date()};
				$.post(url,args,function(data){
					$("#message").html(data);
				});
			}
		});
	});
</script>
</head>
<body>
	<form action="" method="post">
		UserName:<input type="text" name="userName">
		<br>
		<div id="message"></div>
		<br>
		<input type="submit" value="提交">
	</form>
</body>
</html>
```

##### 配置servlet类



![](C:\Users\Administrator\Desktop\servlet.png)



##### ValiateUserNameServlet.java 后台代码：

```java
package com.atguigu.ajax.app.servlets;

import java.io.IOException;
import java.util.Arrays;
import java.util.List;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class ValiateUserNameServlet
 */
public class ValiateUserNameServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public ValiateUserNameServlet() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		//列举三个数据中已经有的名字，现在是指定的三个，在后面这里可以用JDBC去访问数据库得到这个List：
		List<String> userNames = Arrays.asList("AAA","BBB","CCC");
		
		//用一个变量去接收前台传过来的参数userName：
		String userName = request.getParameter("userName");
		
		//定义一个变量result用于后面返回去给前台的数据：
		String result = null;
		
		//将前台传过来的变量值和后台去数据库获取的值做比较，得到结果，并赋值给用于返回的变量result：
		if(userNames.contains(userName)){
			result = "<font color = 'red'>该用户名已经存在</font>";
		}else{
			result = "<font color = 'green'>该用户名可以使用</font>";
		}
		
		//设置返回的结果的编码格式和内容格式：
		response.setContentType("UTF-8");
		response.setCharacterEncoding("UTF-8");
		//将结果result返回到前台：
		response.getWriter().print(result);
	}
}
```

