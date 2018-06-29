##### 基本Ajax_jQuery_load()_txt案例

```htm
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
<title>Ajax_jQuery_load()_txt案例</title>
<script type="text/javascript" src="script/jquery-1.5.2.js"></script>
<script type="text/javascript">
	$(function(){
		alert("1");
		$("a").click(function(){
			var url = this.href;
			var args = {"time":new Date()};
			$("#detail").load(url,args);
			return false;
		});
	});
</script>
</head>
<body>
	<a href="helloAjax.txt">helloAjax</a>
	<div id="detail"></div>
</body>
</html>

//helloAjax.txt
helloWorld!
```

