###### InputStream与OutputStream拷贝

```java
package com.atguigu.inputstream;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;

public class TestCopyImage {
	public static void main(String[] args) {
		//创建输入输出流：
		InputStream is = null;
		OutputStream os = null;
		try {
			is = new FileInputStream("D:\\DonkinFiles\\Images\\Java.png");
			os = new FileOutputStream("src\\atguigu.png");
			
			//创建流容器
			byte[] bt = new byte[1024];
			int len;
			while((len = is.read(bt))!= -1) {
				os.write(bt, 0, len);
			}
		} catch (IOException e) {
			e.printStackTrace();
		}finally {
			//关闭输入输出流
			if(os != null) {
				try {
					os.close();
				} catch (IOException e) {
					e.printStackTrace();
				}finally {
					if(is != null) {
						try {
							is.close();
						} catch (IOException e) {
							e.printStackTrace();
						}
					}
				}
			}
		}
	}
}

```

