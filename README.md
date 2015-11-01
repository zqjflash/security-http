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
	
  * 密码（`明文和密文`），如下图:
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

  **对称密钥加密技术**

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

## 7、HTTPS-细节介绍

  * HTTPS的两个首要目标

    1. 加密传输：第三方无法获知通信内容
    2. 身份认证：第三方无法冒充网站

  * HTTPS的名词解释

    > SSL：安全套接层（Secure Sockets Layer，SSL）是一种二进制协议，其流量是承载在另一个端口上的，通常是443端口；

    > TLS：传输层安全协议（Transport Layer Security），该协议由两层组成：TLS记录协议和TLS握手协议；

    > RTT：同一个封包来回时间

    > tps：系统吞吐量，每秒钟request/事务的数量

    > 事务：访问并可能更新数据库中各种数据项的一个程序执行单元。具有4个属性（ACID特性）：原子性、一致性、隔离性、持久性
    
    > AES-GCM：是一种对称块密码，可以加密和解密的 128 位，使用密码密钥长度为 128、 192 位和 256 位数据块中的信息。

    > CA：证书中心（certificate authority），为公钥做认证。类似：`公安局`

    > 数字证书：包含服务端公钥和数字签名。类似：`身份证`

    > 数字签名：包含加密的摘要，类似：`身份证防伪`

    > 摘要：使用HASH函数计算得到

    > DH：迪菲-赫尔曼密钥交换

    > RSA：加密算法，可以从密文中解出原文，所以不需要携带原文

    > DSA：签名算法，必须把原文和签名一起传输

    > ECC：Elliptic Curve Cryptography - 椭圆曲线密码学（椭圆函数域）

  * HTTPS服务器配置方案

    1. 基础方案-简版：nginx修改配置

	    ```js
	    server {
	      listen              443 ssl;
	      server_name         www.example.com;
	      ssl_certificate     www.example.com.crt;
	      ssl_certificate_key www.example.com.key;
	      ssl_protocols       TLSv1 TLSv1.1 TLSv1.2;
	      ssl_ciphers         HIGH:!aNULL:!MD5;
	    }
	    ```

	    缺点：性能很差
	
	      * 比HTTP多2~7个RTT，1.5秒
	
	      * 服务器耗时增加 9ms CPU， 1k tps
	
	      * 移动客户端耗时增加 50ms CPU

    2. 基础方案-完整版：nginx修改配置

        ```js
        server {
          listen              443 ssl;
          server_name         www.example.com;
          ssl_certificate     www.example.com.crt;
          ssl_certificate_key www.example.com.key;
          ssl_protocols       TLSv1 TLSv1.1 TLSv1.2;
          ssl_ciphers         HIGH:!aNULL:!MD5;

          ssl_perfer_server_ciphers on;
          # session cache
          ssl_session_cache   shared:SSL:1m;
          ssl_session_timeout 5m;
          # HSTS 6 months
          add_header Strict-Transport-Security max-age=15768000;
          # OCSP Stapling ---
          ssl_stapling on;
          ssl_stapling_verify on;
        }
        ```

    3. HTTPS如何加密

        * 对称加密：加密和解密的密钥相同，如下图：

        ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/symmetry.png)

            * 特点：加解密快，消耗小于1ms，256位安全

            * 分为两种：
            
                * 分组加密：DES、AES-CBC（不安全）、AES-GCM（推荐）等
                * 流式加密：RC4（不安全）、ChaCha20（推荐）等

        * 非对称加密：加密和解密的密钥不相同，分为公钥和私钥，公钥可以公开，私钥必须保密，如下图：

        ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/asymmetric.png)

            * 特点：加解密非常慢，需要消耗9ms，2048位安全
            
            * 加密算法：RSA

    4. HTTPS安全层-SSL && TLS

        * SSL/TLS协议的基本思路是采用公钥加密法，也就是说，客户端先向服务器端索要公钥，然后用公钥加密信息，服务器收到密文后，用自己的私钥解密。

        * 加密流程图如下：

        ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/SSL&TLS.png)

        * SSL&TLS协议发展史

        ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/SSL&TLSProtocol.png)

        * 特点：用`对称密钥`加密HTTP协议，用非对称密钥加密对称密钥（`耗时！`），对称密钥又称会话密钥（Session Key）

    5. 如何确定公钥的身份？

        ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/public_private_key.png)

        * 数字证书在https协议主要用于网页加密
        
            step1：客户端使用公钥加密数据，发出请求；

            step2：服务端用自己私钥加密网页以后，连同本身的数字证书，一起发送给客户端;

            step3：客户端“证书管理器”，有“受信任的根证书颁发机构”列表，并且查看解开数字证书的公钥是否在列表之内;

            step4：如果数字证书是受信任的机构颁发，浏览器会发出另一种警告;

            step5：数字证书如果可靠，就可以使用证书中的服务器公钥，对信息进行加密，与服务器交换加密信息。

    6. 公钥基础设施：Public Key Infrastructure，如下图：

        ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/PKI.png)

    7. HTTPS握手过程

        ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/shake_hands.png)
	
        * HTTPS两种握手方案
    
		    ```html
	                  | 密钥协商       |  认证     |   组合
	
	          RSA握手    RSA             RSA          RSA
	
	          DH握手     DH(比RSA安全)    RSA/DSA      DH+RSA（比RSA慢）DH+DSA
		    ```
    
    8. HTTPS加速

        * HTTPS加速 - RSA握手方案，如下图：
        
            ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-rsa.png)

        * HTTPS加速 - DH握手方案，如下图：

            ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-dh.png)

        * HTTPS加速 - DH握手方案 - ECC加速
        
          ECC加速，密钥协商（ECDHE），认证（ECDSA），组合（ECDHE + ECDSA（比RSA快））

          2015年4月，全世界6.2%站点有ECDSA证书；终端TLS1.2

          破解RSA公钥、私钥 = 大数分解

          破解DSA公钥、私钥 = 解Elliptic Curve Discrete Logarithm Problem（ECDLP）问题--比大数分解更难

          ```html
          256位ECDSA    密钥强度3248位RSA           签名速度9516.8tps
          2048位RSA     密钥强度2048位RSA           签名速度10001.8tps
          ```

        * HTTPS加速 - 主流方案，如下图：

            ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-main-speeded-up.png)

    9. HTTPS加密套件，如下图：

		![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-encryption-kits.png)

    10. keyless方案 - 计算集群

        ![Alt text](https://raw.githubusercontent.com/zqjflash/security-http/master/https-cloudflare-keyless.png)

    11. keyless方案 - 密钥复用

		* 好处
		    1. 减少了CPU消耗，因为不需要进行非对称密钥交换的计算。
		    2. 提升访问速度，不需要进行完全握手阶段二，节省了一个RTT和计算耗时。
		
        * 密钥复用
        
            1. Session ID - Key cache
                1. nginx只支持单机cache
                2. 地域局部性好，多地部署memcached
            2. Session ticket
                1. 通过配置系统定时统一更新

    12. 其他优化

        * false Start
            * 在完全握手的第二个阶段将应用数据一起发出来
            * 依赖DH握手（不支持RSA握手）
        * TCP Fast Open
            * 在syn包发出的同时捎上应用层的数据
            * 从linux 3.7 开始支持
        * HSTS
        	* 浏览器缓存HTTP到HTTPS的302跳转
        * 防止HTTPS计算型攻击

    13. 其他优化 - 硬件加速

        * 服务器
            * RSA：无加速 9ms
                * Intel Coleto Creek 芯片
                * RSA握手
                * DH握手
                * ECC：ECDHE & ECDSA
                * Hash
                * gzip压缩
                * 华为对应产品
            * AES：有加速 小于1ms（1KB - 13MB）
                * 2010 Intel CPU Westmere
                * gcc 4.4
        * 终端：未来也会有