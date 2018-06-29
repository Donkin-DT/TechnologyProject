##### 基本Ajax_jQuery_get/post_XML案例

```htm
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Ajax_jQuery_get/post_XML案例</title>
<script type="text/javascript" src="script/jquery-1.5.2.js"></script>
<script type="text/javascript">
	$(function(){
		$("a").click(function(){
			var url= this.href;
			var args = {"time":new Date()};
			$.post(url,args,function(data){//$.get(url,args,function(data){:也可以用get方法，没有多大的差别
				var name = $(data).find("name").text();//$(data):将返回的数据封装成jQuery对象
				var email = $(data).find("email").text();
				var website = $(data).find("website").text();
				$("#detail").empty()//先将节点中的子节点清空
				.append("<h2><a href='mailto:"+ email +"'>"+ name +"</a></h2>")//当前节点添加此节点之后获取到的还是当前节点就再执行下一行代码，继续添加子节点
				.append("<a href='"+ website +"'>"+ website +"</a>");
			});
			return false;
		});
	});
</script>
</head>
<body>
	<h3><a href="files/donkin.xml">Donkin</a></h3>
	<h3><a href="files/xiaoming.xml">xiaoming</a></h3>
	<h3><a href="files/xiaohong.xml">xiaohong</a></h3>
	<div id="detail"></div>
</body>
</html>
```

