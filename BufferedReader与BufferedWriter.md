###### BufferedReaderOrBufferedWriter

```java
package com.atguigu.buffered;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class TestBufferedReaderOrBufferedWriter {
	public static void main(String[] args){
		BufferedReader br = null;
		BufferedWriter bw = null;
		
		try {
			br = new BufferedReader(
					new FileReader("C:\\Users\\Administrator\\Desktop\\InputStream与OutputStream.md"));
			bw = new BufferedWriter(
					new FileWriter("C:\\Users\\Administrator\\Desktop\\1.md"));
			String line;
			int count = 0;
			while((line = br.readLine()) != null) {
				if(line.trim().length() == 0) 
					continue;
				bw.write(++count + "\t" + line);
				bw.newLine();
			}
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			if(bw != null) {
				try {
					bw.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
			if(br != null) {
				try {
					br.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
	}
}
```

