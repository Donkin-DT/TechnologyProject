##### 基本Ajax_JSON_getJSON/get/post_XML案例

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>基本Ajax_JSON_getJSON/get/post_XML案例</title>
<script type="text/javascript" src="script/jquery-1.5.2.js"></script>
<script type="text/javascript">
	$(function(){
		$("a").click(function(){
			var url = this.href;
			var args = {"time":new Date()};
			/*$.getJSON(url,args,function(data){
				var name = data.person.name;
				var website = data.person.website;
				var age = data.person.age;
				$("#detail").empty()//先将节点中的子节点清空
				.append("<h2><a href='mailto:"+ age +"'>"+ name +"</a></h2>")//当前节点添加此节点之后获取到的还是当前节点就再执行下一行代码，继续添加子节点
				.append("<a href='"+ website +"'>"+ website +"</a>");
			});*/
			
			//同样可以用$.post(url,args,function(data){。。。},"JSON")方式来进行AJAX请求但是需要注意的是：需要添加"JSON"参数
			/*$.post(url,args,function(data){
				var name = data.person.name;
				var website = data.person.website;
				var age = data.person.age;
				$("#detail").empty()//先将节点中的子节点清空
				.append("<h2><a href='mailto:"+ age +"'>"+ name +"</a></h2>")//当前节点添加此节点之后获取到的还是当前节点就再执行下一行代码，继续添加子节点
				.append("<a href='"+ website +"'>"+ website +"</a>");
			},"JSON");*/
			
			$.get(url,args,function(data){
				var name = data.person.name;
				var website = data.person.website;
				var age = data.person.age;
				$("#detail").empty()//先将节点中的子节点清空
				.append("<h2><a href='mailto:"+ age +"'>"+ name +"</a></h2>")//当前节点添加此节点之后获取到的还是当前节点就再执行下一行代码，继续添加子节点
				.append("<a href='"+ website +"'>"+ website +"</a>");
			},"JSON");
			
			return false;
		});
	});
</script>
</head>
<body>
	<h3><a href="files/donkin.json">Donkin</a></h3>
	<h3><a href="files/xiaoming.json">xiaoming</a></h3>
	<h3><a href="files/xiaohong.json">xiaohong</a></h3>
	<div id="detail"></div>
</body>
</html>
```

