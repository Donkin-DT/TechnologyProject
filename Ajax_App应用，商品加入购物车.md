##### Ajax_App应用，商品加入购物车

1. index.jsp

```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>购物车应用案例：</title>
<script type="text/javascript" src="${pageContext.request.contextPath }/scripts/jquery-1.5.2.js"></script>

<script type="text/javascript">
	$(function(){
		$("a").click(function(){
			var url = this.href;
			var args = {"time":new Date()};
			
			$.getJSON(url,args,function(data){
				$("#bookName").text(data.bookName);
				$("#totalBookNumber").text(data.totalBookNumber);
				$("#totalMoney").text(data.totalMoney);
			});
			
			return false;
		});
	});
</script>
</head>
<body>
		你已经将&nbsp;&nbsp;<span id="bookName"></span> &nbsp;&nbsp; 加入购物车中,
		<br><br>
		购物车中的书有 &nbsp;&nbsp;<span id="totalBookNumber"></span>&nbsp;&nbsp; 本，
		<br><br>
		总价格为：&nbsp;&nbsp;<span id="totalMoney"></span>&nbsp;&nbsp; 钱。
		<br><br>
		Java &nbsp;&nbsp;<a href="${pageContext.request.contextPath }/addToCart?id=Java&price=200">加入购物车</a>
		<br><br>
		Oracle &nbsp;&nbsp;<a href="${pageContext.request.contextPath }/addToCart?id=Oracle&price=150">加入购物车</a>
		<br><br>
		Struts2 &nbsp;&nbsp;<a href="${pageContext.request.contextPath }/addToCart?id=Struts2&price=300">加入购物车</a>

</body>
</html>
```

2.com.atguigu.ajax.app.beans

​	shoppingCart.java

```java
package com.atguigu.ajax.app.beans;

import java.util.HashMap;
import java.util.Map;

public class ShoppingCart {
	
	//存放ShoppingCartItem的Map：键，：书名，值：ShoppingCartItem的对象。
	private Map<String,ShoppingCartItem> items = new HashMap<String,ShoppingCartItem>();
	
	public void addToCart(String bookName,int price){
		if(items.containsKey(bookName)){
			ShoppingCartItem item = items.get(bookName);
			item.setNumber(item.getNumber() + 1);
		}else{
			ShoppingCartItem item = new ShoppingCartItem();
			item.setBookName(bookName);
			item.setPrice(price);
			item.setNumber(1);
			
			items.put(bookName, item);
		}
	}
    
	public int getTotalBookNumber(){
		int total = 0;
		
		for(ShoppingCartItem item:items.values()){
			total += item.getNumber();
		}
		
		return total;
	}
	
	public int getTotalMoney(){
		int money = 0;
		
		for(ShoppingCartItem item:items.values()){
			money += item.getNumber() * item.getPrice();
		}
		
		return money;
	}
}
```

​	ShoppingCartItem.java

```java
package com.atguigu.ajax.app.beans;

public class ShoppingCartItem {
	private int number;
	
	private String bookName;
	
	private int price;

	public int getNumber() {
		return number;
	}

	public void setNumber(int number) {
		this.number = number;
	}

	public String getBookName() {
		return bookName;
	}

	public void setBookName(String bookName) {
		this.bookName = bookName;
	}

	public int getPrice() {
		return price;
	}

	public void setPrice(int price) {
		this.price = price;
	}
    
}
```

3.com.atguigu.ajax.app.servlets

​	AddtoCartServlet.java

```java
package com.atguigu.ajax.app.servlets;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

import com.atguigu.ajax.app.beans.ShoppingCart;
import com.atguigu.ajax.app.beans.ShoppingCartItem;

/**
 * Servlet implementation class AddToCartServlet
 */
public class AddToCartServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public AddToCartServlet() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		//让doGet调用时也是去调用doPost方法：
		doPost(request,response);
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		//获取请求参数：id，price
		String bookName = request.getParameter("id");
		int price = Integer.parseInt(request.getParameter("price"));
		
		//很重要的：获取购物车对象：
		HttpSession session = request.getSession();
		ShoppingCart sc = (ShoppingCart)session.getAttribute("sc");
		
		if(sc == null){
			sc = new ShoppingCart();
			session.setAttribute("sc", sc);
		}
		 
		//把点击的对象添加到购物车中：
		sc.addToCart(bookName, price);
		
		//准备响应结果拼接成JSON对象：必须用转义字符：\" 来设置 JSON 对象中的双引号 ""，得到JSON对象的格式为：{"bookName":"","tatalBookNumber",1,"totalMoney",1}
		StringBuilder result = new StringBuilder();
		result.append("{")
			  .append("\"bookName\":\"" + bookName + "\"")
			  .append(",")
			  .append("\"totalBookNumber\":" + sc.getTotalBookNumber())
			  .append(",")
			  .append("\"totalMoney\":" + sc.getTotalMoney())
			  .append("}");
		
		//响应JSON对象；
		//设置返回结果的内容字符编码和内容类型：
		response.setContentType("text/javascript");
		response.setCharacterEncoding("UTF-8");
		
		//将结果写入到返回的结果中：
		response.getWriter().print(result.toString());
	}

}

```

