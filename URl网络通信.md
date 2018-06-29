URl

```java
package com.atguigu.url;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.net.URL;
import java.net.URLConnection;

public class TestURL {
	public static void main(String[] args) throws Exception {
		URL url = new URL("http://192.168.15.77:8080/rb.jpg");
		URLConnection connection = url.openConnection();
		
		InputStream inputStream = connection.getInputStream();
		BufferedInputStream bi = new BufferedInputStream(inputStream);
		
		BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("src\\rb.jpg"));
		
		byte[] bt = new byte[1024];
		int len;
		while((len = bi.read(bt)) != -1) {
			bos.write(bt, 0, len);
		}
		
		bos.close();
		bi.close();
	}
}
```

