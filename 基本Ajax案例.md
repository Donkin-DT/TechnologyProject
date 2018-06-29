##### 基本Ajax案例

```javascript
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
<title>Ajax案例</title>
<script type="text/javascript">
	window.onload = function(){//注意格式
		//1、获取a节点并对其添加onclick响应函数
		document.getElementsByTagName("a")[0].onclick = function(){//注意格式
			//3、创建一个XMLHttpRequese对象：
			var request = new XMLHttpRequest();
            
			//4、准备发送请求的数据：url
			var url = this.href + "?time=" + new Date();//"?time=" + new Date() :js中添加的时间戳
			var method = "GET";
			
			//5、调用XMlHttpRequest的open方法：
			request.open(method,url);
			
			//6、调用XMLHttpRequest的send方法：
			request.send(null);
            
			//7、为XMLHttpRequest对象添加onreadstatechange 响应函数
			request.onreadystatechange = function(){
				//alert(request.readyState);
			//8、判断响应是否完成：XMLHttpRequest的对象的readyState属性值是4的时候
				if(request.readyState == 4){
			//9、再判断响应是否可用；XMLHttpResquest对象的status属性值为200
					if(request.status == 200 || request.status == 304){
			//10打印相应结果，responseText
						alert(request.responseText);
					}
				}
			}
			
		//2、取消a节点的默认行为
		return false;
		}
	}
</script>
</head>
<body>
	<a href="helloAjax.txt">helloAjax</a>
</body>
</html>
```



