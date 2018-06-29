##### 基本Ajax_jQuery_load()_HTML案例

```html

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
<title>Ajax_jQuery_load()_HTML案例</title>
<script type="text/javascript" src="script/jquery-1.5.2.js"></script>
<script type="text/javascript">
	$(function(){
		$("a").click(function(){
			var url = this.href;
			var args = {"time" : new Date()};
			$("#detail").load(url,args);
			return false;
		});
	});
</script>
</head>
<body>
	<h3><a href="files/donkin.html">Donkin</a></h3>
	<h3><a href="files/xiaoming.html">xiaoming</a></h3>
	<h3><a href="files/xiaohong.html">xiaohong</a></h3>
	<div id="detail"></div>
</body>
</html>
```

