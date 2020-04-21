---
title: HTTPS（一）加密算法
date: 2020-03-14 17:55:33
tags:
categories: HTTPS
---

## 加密算法的四个意义

隐私性：对称和非对称加密算法

完整性：摘要算法

身份确认：数字签名

不可抵赖：数字签名

<!--more-->

Macos 中的 openssl 版本是 **LibreSSL 2.8.3**

---

## 随机数算法

+ 利用计算机噪声生成随机数：

```bash
sudo head -c 32 /dev/urandom | openssl enc -base64
```

+ 伪随机数算法

  + Blum Blum Shub
  + Mersenne Twister
  + Linear congruential generator

+ 密码学随机数生成算法

  + 块密码算法 CTR 模式
  + 摘要算法
  + 流密码算法

---

## 密码学 HASH 算法

HASH 算法特点：

+ 强抗碰撞性
+ 弱抗碰撞性
+ 单向性

HASH 算法只要要是**弱抗碰撞性**和**单向性**

算法分类：

+ MD5 算法：已经被证明是不安全的，理论上不具有弱抗碰撞性，不建议使用
+ SHA

  + SHA-1: 已经被证明是不安全的
  + SHA-2: SHA-256、SHA-512、SHA-224、SHA-384
  + SHA-3: SHA3-256、SHA3-512、SHA3-224、SHA3-384

---

## 对称加密算法

> 基本思想：
>
> 密文 = E(明文，算法，密钥)
>
> 明文 = D(密文，算法，密钥)

算法类型：

+ 块密码算法（例如：AES）：基于分组块的迭代运算
+ 流密码算法（例如：RC4）：基于 XOR 运算

AES 迭代类型：

+ ECB：最简单，不推荐
+ CBC：推荐
+ CTR：推荐

块密码算法的填充标准 **PKCS#7**。**PKCS#7** 可以处理 255 内的字节，**PKCS#5** 是他的子集，只能处理 8 个字节

对于 AES 算法，双方需要约定分组长度、迭代类型、填充方式

openssl 工具使用（加密解密均需要输入口令）：

利用 openssl 工具进行加密解密：

```bash
# 加密
openssl enc -aes-256-cbc -salt -in file.txt -out file.encrypt -p

# 解密
openssl enc -d -aes-256-cbc -in file.encrypt
```

AES 算法涉及到 salt、初始化向量、密钥、口令。其中 `密钥=salt+口令`

---

## 消息验证码算法

由于存在中间人攻击，密码学HASH算法不能校验消息是否被篡改。

MAC 算法的种类：

+ CBC-MAC 算法
+ HMAC 算法

```bash
# 普通HASH算法
openssl dgst -sha1 file.txt

# MAC 算法
openssl dgst -sha224 -hmac "123" file.txt
```

---

## 非对称加密算法

用途：加密解密、数字签名

### RSA 算法

密钥文件（包含公钥和私钥）

+ p: 一个大质数
+ q: 另一个大质数
+ n: p*q
+ e: 公开指数
+ d: 私钥=func(e,p,q)

加密 C = M^e (mod n)，解密 M = C^d (mod n)

签名 s = m^d (mod n)，验签 m = s^e (mod n)

```bash
# 生成一个 RSA 密钥（私钥）
openssl genrsa 2048

# 生成一个 RSA 私钥，并导出公钥
openssl genrsa -out rsa_pri.pem 2048
openssl rsa -in rsa_pri.pem -pubout -out rsa_pub.pem

# 校验密钥是否正确
openssl rsa -in rsa_pri.pem -check -noout
openssl rsa -pubin -in rsa_pub.pem -text

# 加解密文件（默认采用PKCS#1 v1.5填充 -pkcs，也可以手动指定PKCS#1OAEP填充 -oaep）
openssl rsautl -encrypt -pubin -inkey rsa_pub.pem -in file.txt -out file.encrypt
openssl rsautl -decrypt -inkey rsa_pri.pem -in file.encrypt

# 数字签名，对摘要签名
openssl dgst -sha256 -sign rsa_pri.pem -out file.sign file.txt
openssl dgst -sha256 -verify rsa_pub.pem -signature file.sign file.txt
```

### ECC 算法

加密：

```bash
# 罗列自带的命名曲线
openssl ecparam -list_curves

# 生成一组椭圆曲线密钥，并显示出参数
openssl ecparam -name secp256k1 -out secp256k1.pem
openssl ecparam -in secp256k1.pem -text -param_enc explicit


## output:
Field Type: prime-field
Prime:
    00:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:fe:ff:
    ff:fc:2f
A:    0
B:    7 (0x7)
Generator (uncompressed):
    04:79:be:66:7e:f9:dc:bb:ac:55:a0:62:95:ce:87:
    0b:07:02:9b:fc:db:2d:ce:28:d9:59:f2:81:5b:16:
    f8:17:98:48:3a:da:77:26:a3:c4:65:5d:a4:fb:fc:
    0e:11:08:a8:fd:17:b4:48:a6:85:54:19:9c:47:d0:
    8f:fb:10:d4:b8
Order:
    00:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:ff:
    ff:fe:ba:ae:dc:e6:af:48:a0:3b:bf:d2:5e:8c:d0:
    36:41:41
Cofactor:  1 (0x1)
```

A、B 椭圆曲线参数，P 大质数，Generator G点，n 椭圆曲线的阶，Cofactor 椭圆曲线所有点除以 n

数字签名算法 ECDSA：

```bash
openssl ecparam -name secp256k1 -genkey -out ecdsa_pri.pem
openssl ec -in ecdsa_pri.pem -pubout -out ecdsa_pub.pem
openssl dgst -sha256 -sign ecdsa_pri.pem -out file.sign file.txt
openssl dgst -sha256 -verify ecdsa_pub.pem -signature file.sign file.txt
```

---

## 密钥

口令：方便记忆的人造简单密钥

密钥：计算机生成的随机数

### DH 密钥协商算法

由通信双方 A 和 B 一起协商生成一个会话密钥（思想比算法更重要）
