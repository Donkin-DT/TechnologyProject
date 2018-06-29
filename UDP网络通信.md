###### UDP网络通信😀

```java
package demo.net;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;
import java.net.SocketException;
import java.net.UnknownHostException;

import org.junit.Test;
/**
 * 此类用于演示基于UDP协议的网络通信
 * 案例：发送端——>接收端  发送数据，接收端接受并打印
 */
public class TestUDP {
	//测试发送端
	@Test
	public void send() throws SocketException, IOException {
		//1.创建发送端套接字对象
		DatagramSocket socket = new DatagramSocket();
		
		//2.发送数据
		//①创建DatagramPacket对象，指定发送的数据、收件人的地址等
		byte[] bytes = "哈喽，我是土豆".getBytes();
		DatagramPacket packet = new DatagramPacket(bytes, bytes.length, InetAddress.getLocalHost(),9999);
		
		//②发送
		socket.send(packet);

		//3.关闭
		socket.close();
	}
	
	//测试接收端
	@Test
	public void receive() throws IOException {
		//1.创建接收端套接字对象
		DatagramSocket socket = new DatagramSocket(9999);
		
		//2.接收
		//①创建DatagramPacket对象，用于接受
		byte[] b = new byte[1000];
		DatagramPacket packet = new DatagramPacket(b, b.length);
		
		//②接受
		socket.receive(packet);
		
		//③处理接收的数据
		byte[] data = packet.getData();
		int length = packet.getLength();
		
		System.out.println(new String(data,0,length));
		
		//3.关闭
		socket.close();
	}
}
```

