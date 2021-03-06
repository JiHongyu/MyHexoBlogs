---
title: https deployment
date: 2020-03-15 18:29:34
tags:
categories: HTTPS
---


## TLS/SSL 介绍

TLS/SSL 协议的核心：认证、密钥协商、数据加密

前向安全性：拿到私钥对历史数据进行解密。RSA 密钥协商算法和静态DH算法都不能保证前向安全性。

中间人攻击：RSA 和 DH 保证不了，需要使用 PKI 技术。

PKI 不是 TLS/SSL 技术的一部分，但是必须引入 PKI 才能保证 TLS/SSL 安全。

PKI 的核心是证 **证书**，通过 CA 签发的证书保证信息交换的可靠性。

<!--more-->

申请证书的流程：

1. 服务器准备发布 https://www.test.com 

2. 服务器实体生成公开密钥算法的一对密钥，比如一对 RSA 密钥

3. 服务器实体生成 CSR 文件交给 CA 机构

4. CA 机构核实 CSR 文件

5. 对于审核通过的 CSR 文件，CA 机构用自己的私钥对 CSR 签名附在 CSR 文件后面得到证书文件

6. 将证书文件返回给服务实体

浏览器访问流程：

1. 浏览器向 https://www.test.com 发出请求
2. 服务器收到请求后将证书和 RSA 公钥发送给浏览器
3. 浏览器根据证书中的机构信息，确定是否为 CA 签发证书，并进行验证
4. 若验证成功，说明服务器身份是受 CA 机构认可，然后对比 RSA 公钥和证书公钥对比，判断是否是同一个服务器实体
5. 如果验证再次成功，说明身份校验完成，接下来可以进行密钥协商


HTTPS 一般要求全站 HTTPS 策略，但是会存在 HTTPS 页面引用了非 HTTPS 元素，导致出现 **混合内容**

+ 被动混合
+ 主动混合

浏览器采取的策略一般是不一样的。
