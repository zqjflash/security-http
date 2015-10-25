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
	
	* 数字密码
	
	使用不同密钥的旋转N字符密码
	![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-number-cipher.png)

## 3、对称密钥加密技术

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
  
## 4、公开密钥加密技术

  > 公开密钥加密技术没有为每对主机使用单独的加密/解密密钥，而是使用了两个非对称密钥：一个用来对主机报文编码，另一个用来对主机报文解码。
  
  * 公开密钥加密技术是非对称的，为编码和解码使用了不同的密钥，如下图：
  
  ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-public-key.png)

  * 对称密钥加密技术与公开密钥加密技术对比，如下图：

  ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-symmetry-public.png)

  * RSA（非对称加密算法）：公开密钥，只有私钥才得以解密

  * 混合加密系统和会话密钥

    * 公开加密算法计算可能会很慢。混合使用了对称和非对称策略。

    * 常见方式，在两节点间通过便捷的公钥加密技术建立安全通信，然后再用那条安全的通道产生并发送临时的随机对称密钥，通过更快的对称加密技术对其余的数据进行加密。

## 5、数字签名

  加密系统对报文进行签名（sign），以说明谁编写的报文并且未被篡改过。这种技术被称为数字签名。

  * 签名是加了密的校验和

  数字签名是附加在报文上的特殊加密校验码。

    * 签名可以证明是被信任的这条报文
    * 签名可以防止报文被篡改
    
  数字签名通常是用非对称公开密钥技术产生的。因为只有所有者才知道其私有密钥，所以可以将作者私有密钥当作一种“指纹”使用

  解密的数字签名流程，如下图：

  ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-sign.png)

## 6、数字证书

  > 数字证书（通过被称作"certs"）包含了由某个受信任组织担保的用户或公司的相关信息。

  证书的主要内容：

  1、对象的名称；

  2、过期时间；

  3、证书发布者（由谁为证书担保）；

  4、来自证书发布者的数字签名。

  典型的数字签名格式，如下图：

  ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-sign-format.png)

  **X.509 v3证书**

  ```html
  
    字段            |     描述
    版本              这个证书的X.509证书版本号。现在使用的通常都是版本3 
    序列号            证书颁发机构（CA）生成的唯一整数。CA生成的每个证书都要有一个唯一的序列号
    签名算法ID        签名所使用的加密算法。使用，“用RSA加密的MD2摘要”
    证书颁发者        发布并签署这个证书的组织名称，以X.500格式表示
    有效期            此证书何时有效，由一个起始日期和一个结束日期来表示
    对象名称          证书中描述的实体，比如一个人或一个组织。对象名称是以X.500格式表示的
    对象的公开密钥信息  证书对象的公开密钥，公开密钥使用的算法，以及所有附加参数
    发布者唯一的ID     可选的证书发布者唯一标识符，这样就可以重用相同的发布者名称
    对象唯一的ID       可选的证书对象唯一标识符，这样就可以重用相同的对象名称
    扩展              可选的扩展字段集
    证书的颁发机构签名  证书颁发机构用指定的签名算法对上述所有字段进行的数字签名
  ```

  用证书对服务器进行认证

  服务器证书
  
  * web站点的名称和主机名；

  * web站点的公开密钥；

  * 签名颁发机构的名称；

  * 来自签名颁发机构的签名。

  签证签名流程，如下图：

  ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-sign-validate.png)
