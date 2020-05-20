---
title: Springboot 自动装配（Springboot 编程思想第9章）
date: 2020-05-04 21:53:12
tags: springboot
---

## Spring 配置工厂 `spring.factories` 文件

Spring 仿照 Java SPI 实现的一套工厂配置模块，用于一些可插拔的逻辑配置，比如 **自动装配**

`spring.factories` 文件的读取是在 `SpringFactoriesLoader` 实现

