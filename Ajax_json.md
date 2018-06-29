##### 基本Ajax_json案例

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
							//把json文档转换为对象：eval( "(" + request.responseText + ")")
							var result = eval( "(" + request.responseText + ")");
							
							var name = result.person.name;
							var website = result.person.website;
							var age = result.person.age;
							
							//创建a节点：
							var aNode = document.createElement("a");
							//创建文本节点，并添加到a节点下面
							aNode.appendChild(document.createTextNode(name));
							
							var h2Node = document.createElement("h2");
							h2Node.appendChild(aNode);
							
							var aNode2 = document.createElement("a");
							//创建文本节点，并添加到a节点下面
							aNode2.appendChild(document.createTextNode(website));
							aNode2.appendChild(document.createTextNode("  年龄"));
							aNode2.appendChild(document.createTextNode(age));
					
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
	<h3><a href="files/donkin.json">Donkin</a></h3>
	<h3><a href="files/xiaoming.json">xiaoming</a></h3>
	<h3><a href="files/xiaohong.json">xiaohong</a></h3>
	<div id="detail"></div>
</body>
</html>

//json文件：donkin.json如下

{"person":{
"name":"donkin",
"website":"www.donkin.com",
"age":27
}
}

```

