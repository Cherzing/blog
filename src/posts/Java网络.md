---
title: Java网络
date: 2023-08-18
cover: https://cdn.jsdelivr.net/gh/czlifetime/img/Java.jpg
tag:
  - Java
---

# 网络

## InetAddress类

+ 获取本机InetAddress对象：`getLocalHost()`
+ 根据指定主机名/域名获取ip地址对象：`getByName()`
+ 获取InetAddress对象的主机名：`getHostName()`
+ 获取InetAddress对象的地址：`getHostAddress()`

```Java

public class API_ {
    public static void main(String[] args) throws UnknownHostException {
        InetAddress localHost = InetAddress.getLocalHost();
        System.out.println(localHost);

        InetAddress byName = InetAddress.getByName("MaxLifetime-LAPTOP");
        System.out.println(byName);

        String lh1 = localHost.getHostName();
        System.out.println(lh1);

        String hm = byName.getHostName();
        System.out.println(hm);
    }
}

```

## Socket

1. 套接字(Socket)开发网络应用程序被广泛采用，以至于成为事实上的标准

2. 通信的两端都要有插座，是两台机器间通信的端点
3. 网络通信其实就是Socket间的通信.
4. Socket允许程序把网络连接当成一个流，数据在两个套接字间通过IO传输
5. 一般主动发起通信的应用程序属客户端，等待通信请求的为服务端

###  TCP网络通信编程

1. 基本介绍
   + 基于客户端——服务端的网络通信
   + 底层使用的是TCP/IP协议
   + 应用场景举例：客户端发送数据、服务端接受并显示
   + 基于Socket的TCP编程
   + （可靠）

### UDP编程

（不可靠）

![](https://cdn.jsdelivr.net/gh/czlifetime/img/TCP%E9%80%9A%E4%BF%A1%E7%BC%96%E7%A8%8B.png)

> 练习1.：
>
> 1.编写一个服务器端,和一个客户端
> 2.服务器端在 9999端口监听
> 3.客户端连接到服务器端，发送“hello,server”，然后退出
> 4.服务器端接收到 客户端发送的 信息，输出，并退出
>
> 思路：
>
> ![](https://cdn.jsdelivr.net/gh/czlifetime/img/TCPMind.jpg)
>
> > <Strong>Server:</Strong>
> >
> > ```java 
> > package Internet.API;
> > 
> > 
> > 
> > 
> > import java.io.IOException;
> > import java.io.InputStream;
> > import java.net.ServerSocket;
> > import java.net.Socket;
> > 
> > public class SocketTCPServer {
> >     public static void main(String[] args) throws IOException {
> >         ServerSocket serverSocket = new ServerSocket(9999);
> >         System.out.println("等待连接");
> >         Socket socket = serverSocket.accept();
> > 
> >         InputStream inputStream = socket.getInputStream();
> > 
> >         byte[] bytes = new byte[8];
> >         int readLen  = 0;
> >         while((readLen = inputStream.read(bytes)) != -1){
> >             System.out.print(new String(bytes ,0,readLen));
> >         }
> >         System.out.println();
> >         System.out.println("关闭");
> >         serverSocket.close();
> >         inputStream.close();
> >     }
> > }
> > 
> > ```
> >
> > <Strong>Client：</Strong>
> >
> > ```Java
> > package Internet.API;
> > 
> > import java.io.FileOutputStream;
> > import java.io.IOException;
> > import java.io.OutputStream;
> > import java.net.InetAddress;
> > import java.net.Socket;
> > import java.net.UnknownHostException;
> > 
> > public class SocketTCPClient {
> >     public static void main(String[] args) throws IOException {
> >         Socket socket = new Socket(InetAddress.getLocalHost(), 9999);
> >         String string = "Hello world";
> > 
> >         OutputStream outputStream = socket.getOutputStream();
> >         byte[] bytes = new byte[8];
> > 
> >         outputStream.write(string.getBytes());
> > 
> >         outputStream.close();
> >         socket.close();
> >         }
> >     }
> > 
> > 
> > ```
> >
> > 

> 练习2：(使用字节流)
>
> 1. 编写一个服务端，和一个客户端
> 2. 服务器端在9999端口监听
> 3. 客户端连接到服务器端，发送“你好，服务器”，并接收服务器端回发的“你好，客户”再退出
> 4. 服务器端接收到客户端发送的信息，输出，并发送“你好，客户”，再退出 
>
> 思路：
>
>  /+ 以上思路
>
> ![](https://cdn.jsdelivr.net/gh/czlifetime/img/TCPMindTest2.jpg)
>
> > <strong>Server:</strong>
> >
> > ```java
> > package Internet.API.TCP_2;
> > 
> > import java.io.IOException;
> > import java.io.InputStream;
> > import java.io.OutputStream;
> > import java.net.ServerSocket;
> > import java.net.Socket;
> > 
> > public class SocketTCP2Server {
> >     public static void main(String[] args) throws IOException {
> >         //2.服务器端在9999端口监听
> >         ServerSocket serverSocket = new ServerSocket(9999);
> >         Socket socket = serverSocket.accept();
> >         InputStream inputStream = socket.getInputStream();
> >         byte[] bytes = new byte[1024];
> >         int readLen = 0;
> >         while((readLen = inputStream.read(bytes)) != -1){
> >             System.out.print(new String(bytes,0,readLen));
> >         }
> > 
> >         System.out.println("\nServer收到“你好，服务器”");
> > 
> > 
> >         //3.客户端连接到服务器端，发送“你好，服务器”，并接收服务器端回发的“你好，客户”再退出
> >         //4.服务器端接收到客户端发送的信息，输出，并发送“你好，客户”，再退出
> >         OutputStream outputStream = socket.getOutputStream();
> >         outputStream.write("你好，客户".getBytes());
> >         socket.shutdownOutput();
> > 
> >         serverSocket.close();
> >         socket.close();
> >         inputStream.close();
> >         outputStream.close();
> > 
> >     }
> > }
> > 
> > ```
> >
> > <Strong>Client:</strong>
> >
> > ```java
> > package Internet.API.TCP_2;
> > 
> > import java.io.InputStream;
> > import java.io.OutputStream;
> > import java.net.InetAddress;
> > import java.io.IOException;
> > import java.net.Socket;
> > 
> > public class SocketTCP2Client {
> >     public static void main(String[] args) throws IOException {
> >         //3.客户端连接到服务器端，发送“你好，服务器”，并接收服务器端回发的“你好，客户”再退出
> >         Socket socket = new Socket(InetAddress.getLocalHost(), 9999);
> >         OutputStream outputStream = socket.getOutputStream();
> >         outputStream.write("你好，服务器".getBytes());
> >         socket.shutdownOutput();
> > 
> > 
> >         InputStream inputStream = socket.getInputStream();
> >         byte[] bytes = new byte[1024];
> >         int readLen = 0;
> >         while((readLen = inputStream.read(bytes)) != -1){
> >             System.out.print(new String(bytes,0,readLen));
> >         }
> > 
> >         //4.服务器端接收到客户端发送的信息，输出，并发送“你好，客户”，再退出
> >         socket.close();
> >         outputStream.close();
> >         inputStream.close();
> >     }
> > }
> > 
> > ```
>
> 

> 练习3：(使用字节流)
>
> 1. 编写一个服务端，和一个客户端
> 2. 服务器端在9999端口监听
> 3. 客户端连接到服务器端，发送“你好，服务器”，并接收服务器端回发的“你好，客户”再退出
> 4. 服务器端接收到客户端发送的信息，输出，并发送“你好，客户”，再退出 
>
> ![](https://cdn.jsdelivr.net/gh/czlifetime/img/TCPMindTest3.jpg)
>
> > <strong>Client:</strong>
> >
> > ```java
> > package Internet.API.TCP_3;
> > 
> > import java.io.*;
> > import java.net.InetAddress;
> > import java.net.Socket;
> > 
> > public class SocketTCP3Client {
> >     public static void main(String[] args) throws IOException {
> >         //3.客户端连接到服务器端，发送“你好，服务器”，并接收服务器端回发的“你好，客户”再退出
> >         Socket socket = new Socket(InetAddress.getLocalHost(), 9999);
> >         OutputStream outputStream = socket.getOutputStream();
> >         //使用字符流
> >         BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(outputStream));
> >         bufferedWriter.write("hello Server");
> >         bufferedWriter.newLine();
> >         bufferedWriter.flush();
> >         socket.shutdownOutput();
> > 
> > 
> >         InputStream inputStream = socket.getInputStream();
> >         BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream));
> >         String s = bufferedReader.readLine();
> >         System.out.println(s);
> > 
> >         //4.服务器端接收到客户端发送的信息，输出，并发送“你好，客户”，再退出
> >         socket.close();
> >         outputStream.close();
> >         bufferedReader.close();
> >         bufferedWriter.close();
> >     }
> > }
> > 
> > ```
> >
> > <strong>Server:</strong>
> >
> > ```java
> > package Internet.API.TCP_3;
> > 
> > import java.io.*;
> > import java.net.ServerSocket;
> > import java.net.Socket;
> > 
> > public class SocketTCP3Server {
> >     public static void main(String[] args) throws IOException {
> >         //2.服务器端在9999端口监听
> >         ServerSocket serverSocket = new ServerSocket(9999);
> >         Socket socket = serverSocket.accept();
> >         InputStream inputStream = socket.getInputStream();
> > 
> >         BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream));
> >         String s = bufferedReader.readLine();
> >         System.out.println(s);
> > 
> >         System.out.println("\nServer收到“你好，服务器”");
> > 
> > 
> >         //3.客户端连接到服务器端，发送“你好，服务器”，并接收服务器端回发的“你好，客户”再退出
> >         //4.服务器端接收到客户端发送的信息，输出，并发送“你好，客户”，再退出
> >         OutputStream outputStream = socket.getOutputStream();
> >         BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(outputStream));
> >         bufferedWriter.write("Hello Client");
> >         bufferedWriter.newLine();
> >         bufferedWriter.flush();
> > 
> >         serverSocket.close();
> >         socket.close();
> >         bufferedWriter.close();
> >         bufferedReader.close();
> >     }
> > }
> > 
> > ```



