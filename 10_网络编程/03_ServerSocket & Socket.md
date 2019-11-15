## ServerSocket & Socket 类

##### ServerSocket:

`java.net.ServerSocket`: 实现了服务端套接字, 等待客户端套接字请求

构造方法: 

`public ServerSocket(int port)`: 创建绑定到指定端口号的服务器套接字



成员方法:

1. `public Socket accept()`: 侦听并返回客户端的套接字, 然后使用客户端的套接字与客户端进行交互
2. `public void close()`: 关闭套接字, 释放资源



##### Socket:

`java.net.Socket`: 实现了客户端的套接字, 套接字是两台机器之间通信的端点

套接字是包含了 IP 地址和端口号的网络单位



构造方法: 

`Socket(String host, int port)`: 创建一个流套接字, 并将其连接到指定主机, 指定端口



成员方法: 

1. `OutputStream getOutputStream()`: 返回套接字的输出流
2. `InputStream getInputStream()`: 返回套接字的输入流
3. `void close()`: 关闭此套接字  



##### demo:

server

```java
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class TCPServer {
    public static void main(String[] args) throws IOException {
        // 创建 server socket
        ServerSocket server  = new ServerSocket(9000);
        // 获取客户端连接
        Socket socket = server.accept();
        // 获取输入 IO流对象
        InputStream is = socket.getInputStream();
        // 读取 数据
        byte[] bytes = new byte[1024];
        int dataLen = is.read(bytes);
        System.out.println("来自客户端的消息: " + new String(bytes, 0, dataLen));
        // 发送数据
        OutputStream os = socket.getOutputStream();
        os.write("收到了".getBytes("UTF-8"));
        os.flush();

        //释放资源
        socket.close();
        server.close();
    }
}

```



client

```java
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.Socket;


public class TCPClient {
    public static void main(String[] args) throws IOException {
        // 创建 socket, 这里就连接服务器的地址和端口了
        Socket socket  = new Socket("localhost", 9000);
        // 获取输出 IO流 对象
        OutputStream os = socket.getOutputStream();
        // 写入 IO 流,  发送到服务端
        os.write("hello world".getBytes("UTF-8"));
        os.flush();
        System.out.println("信息发送成功");

        //接收服务端的信息
        InputStream is = socket.getInputStream();
        byte[] bytes = new byte[1024];
        int dataLen = is.read(bytes);
        System.out.println("来自服务端的响应: " + new String(bytes, 0, dataLen));

        //释放资源
        socket.close();
    }
}
```



