##### 基本Ajax_HTML案例

```html

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
<title>Ajax_HTML案例</title>
<script type="text/javascript">
	window.onload = function(){//注意格式

		var aNodes = document.getElementsByTagName("a");
		for(var i = 0;i < aNodes.length;i++){
			
			aNodes[i].onclick = function(){
				var request = new XMLHttpRequest();
				
				var method = "GET";
				var url = this.href + "?time=" + new Date();
				
				request.open(method,url);
				
				request.send(null);
				
				request.onreadystatechange = function(){
					if(request.readyState == 4){
						if(request.status == 200 || request.status == 304){
							document.getElementById("detail").innerHTML = request.responseText;
						}
					}
				}
				
			return false;
			} 
		}
	}
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

