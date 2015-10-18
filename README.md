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

  * 数字加密

    * 密码（`明文和密文`），如下图

    ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-cipher.png)
  
    * 密文规则（`循环移位3字符密码实例`）

    ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-rot.png)

    * 数字密码

    使用不同密钥的旋转N字符密码
    ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-number-cipher.png)

## 2、对称密钥加密技术

  > 发送端和接收端要共享相同的密钥k才能进行通信。发送端用共享的密钥来加密报文，并将得到的密文发送给接收端。接收端收到密文，并对其应用解密函数和相同的共享密钥，恢复出原始的明文

  > 对称密钥加密算法为编/解码使用相同的密钥

  ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-symmetry.png)

  > 流行的对称密钥加密算法包括：DES、Triple-DES、RC2和RC4。

  * 密钥长度与枚举攻击

  密钥长度取决密钥值的位数，枚举攻击方式是通过暴力破解所有密钥值
  
  * 建立共享密钥

  对称密钥加密技术的缺点之一：发送者与接收者在互相对话之前，一定要有一个共享的保密密钥。
  
## 3、公开密钥加密技术

  > 公开密钥加密技术没有为每对主机使用单独的加密/解密密钥，而是使用了两个非对称密钥：一个用来对主机报文编码，另一个用来对主机报文解码。
  
  * 公开密钥加密技术是非对称的，为编码和解码使用了不同的密钥，如下图：
  
  ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-public-key.png)

  * 对称密钥加密技术与公开密钥加密技术对比，如下图：

  ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-symmetry-public.png)























  
