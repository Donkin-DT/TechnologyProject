###### ReaderOrWriter

```java
package com.atguigu.readerorwriter;

import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.io.Reader;
import java.io.Writer;

public class TestReaderWriter {
	public static void main(String[] args) {
		Reader rd = null;
		Writer wd = null;
		try {
			rd = new FileReader("C:\\Users\\Administrator\\Desktop\\InputStream与OutputStream.md");
			wd = new FileWriter("C:\\Users\\Administrator\\Desktop\\1.md");
			
			char[] ch = new char[1024];
			int len;
			while((len = rd.read(ch)) != -1) {
				wd.write(ch, 0, len);
			}
		}catch (IOException e) {
			e.printStackTrace();
		}finally {
			if(wd != null) {
				try {
					wd.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
			if(rd != null) {
				try {
					rd.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
	}
}
```

