# security-http

## 1、保护HTTP的安全

  * 需要提供下列功能的HTTP安全技术：

  1、服务器认证（`客户端感知是与可信任的服务端通信`）
  
  2、客户端认证（`服务端感知是与可新人的客户端通信`）
  
  3、完整性（`客户端和服务器的数据不可被篡改`）
  
  4、加密（`客户端和服务端通信不被窃取`）
  
  5、效率（`运行效率快的算法，支持低端客户端和服务端使用`）
  
  6、普适性（`支持所有客户端和服务器通信协议`）
  
  7、适应性（`能够支持目前最知名的安全方法`）
  
  * HTTPS（`所有主流的浏览器和服务器都支持此协议`）
  
  > HTTPS以`https://`，有些浏览器还会显示一些标志性的安全提示，如下图
  ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https.png)

  * HTTPS与HTTP对比
  
  > HTTPS在HTTP下面提供了一个传输级的密码安全层（SSL[`Secure Sockets Layer`] or TLS[`Transport Layer Security`]），如下图
  ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-protocol.png)

## 2、数字加密

  * 密码（`明文和密文`），如下图

  ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-cipher.png)
  
  * 密文规则（`循环移位3字符密码实例`）

  ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-rot.png)








  
