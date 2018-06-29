###### File类与递归综合😃

```java
package com.atguigu.file;

import java.io.File;

public class TestFile {
	public static void main(String[] args) {
        //创建路径的 File 对象,需要判断是否存在此目录或文件，如果返回false则需要创建目录或文件；
        //创建目录调用：file1.mkdirs();
        //创建文件：file1.createNewFile()
		File file1 = new File("D:\\DonkinFiles\\文档文件");
		printFiles(file1);
	}
	
//	递归方法：
	public static void printFiles(File filePath) {
		File[] files = filePath.listFiles();
		
		for (File file : files) {
			System.out.println(file.getName());
//			//方式 1：
//			if(file.isFile()) {
//				continue;
//			}else {
//				printFiles(file);
//			}
			
//			//方式2：
			if(file.isDirectory()) {
				printFiles(file);
			}
		}
	}
}
```

console

```java
	第六章 面向对象（下）.md
	第六章 面向对象（中）.md
	综合案例（面向对象中、下）.md
	！word
	bin
	JavaSE_01概述.bin
	JavaSE_02基本语法.bin
	JavaSE_06异常处理.bin
	JavaSE_07集合.bin
	JavaSE_13网络编程.bin
	javaweb.bin
	JavaSE_01概述.doc
	JavaSE_05面向对象3.doc
	JavaSE_06异常处理.doc
	JavaSE_06异常处理.files
	header.htm
	JavaSE_09IO.doc
	JavaSE_12反射机制.doc
	JavaSE_13网络编程.doc
	filelist.xml
	themedata.thmx
	javaweb.doc
```

