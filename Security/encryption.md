# <center>Encryption</center>

<br></br>



## Asymmetric Encryption 非对称加密
With asymmetric algorithms, only private key member of the pair must be kept private and secure; as its name suggests, the public key can be made available to anyone without compromising the encrypted data. The downside of public-key algorithms is that they're much slower than symmetric algorithms and can't be used to encrypt large amounts of data.

非对称加密使用一对密钥，即公钥（public key）和私钥（private key）。公钥加密数据，私钥解密数据。公钥和私钥是相关的密钥，使用其中一个密钥加密的数据只能通过另一个密钥解密。你使用朋友的公钥加密消息，然后发送给朋友。朋友使用自己私钥解密消息，读取内容。即使有人截获加密消息，没有私钥情况下也无法解密。

特点：
- 安全的密钥管理：由于加密和解密使用不同密钥，公钥可公开发布，而私钥须保密。减轻了密钥管理难度。
- 速度慢：比对称加密计算复杂度高，处理速度慢，因此常用于较小的数据或加密对称加密的密钥。
- 算法：RSA、DSA（数字签名算法）、ECC（椭圆曲线加密）等。

<br></br>



## Symmetric encryption 对称加密
Algorithms that use symmetric keys, such as Advanced Encryption Standard (AES), are typically faster than public-key algorithms, and are often used for protecting large data stores. Because there's only one key, procedures must be in place to prevent the key from becoming publicly known.

对称加密是在加密和解密时使用相同密钥。意味发送和接收方使用同一个密钥加密和解密消息。假设你和朋友有相同密钥，你用密钥加密一条消息，然后发送给朋友。朋友使用相同密钥解密消息。

特点：
- 速度快：由于加密和解密使用相同密钥，对称加密计算效率高，适合处理大量数据。
- 密钥管理难度大：由于同一密钥用于加密解密，密钥须在传输或存储过程中保持安全。
- 算法：AES（高级加密标准）、DES（数据加密标准）、3DES（三重DES）、RC4等。
