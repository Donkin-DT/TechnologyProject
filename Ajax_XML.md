##### 基本Ajax_XML案例

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Ajax_XML案例</title>
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
					alert(request.readyState);
					if(request.readyState == 4){
						if(request.status == 200 || request.status == 304){
							var result = request.responseXML;
							//分别解析XML文档
							var name = result.getElementsByTagName("name")[0].firstChild.nodeValue;
							var website = result.getElementsByTagName("website")[0].firstChild.nodeValue;
							var email = result.getElementsByTagName("email")[0].firstChild.nodeValue;
							
							//创建a节点：
							var aNode = document.createElement("a");
							//创建文本节点，并添加到a节点下面
							aNode.appendChild(document.createTextNode(name));
							aNode.href = "mailto:" + email;
							
							var h2Node = document.createElement("h2");
							h2Node.appendChild(aNode);
							
							var aNode2 = document.createElement("a");
							//创建文本节点，并添加到a节点下面
							aNode2.appendChild(document.createTextNode(website));
							aNode2.href = website;
							
							var detailsNode = document.getElementById("detail");
						
							detailsNode.innerHTML = "";//detailsNode节点每次添加新的节点的时候先清空。
							detailsNode.appendChild(h2Node);
							detailsNode.appendChild(aNode2);
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
	<h3><a href="files/donkin.xml">Donkin</a></h3>
	<h3><a href="files/xiaoming.xml">xiaoming</a></h3>
	<h3><a href="files/xiaohong.xml">xiaohong</a></h3>
	<div id="detail"></div>
</body>
</html>
```

