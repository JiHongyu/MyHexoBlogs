---
title: Springboot 模块驱动设计模式（Springboot 编程思想第8章）
date: 2020-05-03 22:41:29
tags: springboot
---

从 Spring Framework 3.1 以后，Spring 逐渐向模块化框架演进。

<!--more-->

模块驱动核心的注解是 `@Import`，通过用法可以分为两类实现：

+ 注解驱动：导入普通 `@Configuration` 类
+ 接口编程：导入 `ImportSelector` 或者 `ImportBeanDefinitionRegistrar` 实现类

（如果是 Xml 配置文件，则需使用注解 `@ImportResource`）

Spring Bean 两中后置处理接口：`BeanPostProcessor`和`BeanFactoryPostProcessor`

+ `BeanPostProcessor`：bean级别的处理，针对某个具体的bean进行处理
+ `BeanFactoryPostProcessor`：BeanFactory级别的处理，是针对整个Bean的工厂进行处理

## WEB 自动装配

在 Servlet 3.0 以后，支持通过 `WebApplcaitionInitializer`（替换 web.xml） 构建 WEB 应用。其基本扩展类结构如下：

{% plantuml %}
WebApplcaitionInitializer <|-- AbstractContextLoaderInitializer
AbstractContextLoaderInitializer <|-- AbstractDispatcherServletInitializer
AbstractDispatcherServletInitializer <|-- AbstractAnnotationConfigDispatcherServletInitializer

WebApplcaitionInitializer <|-- SpringServletContainerInitializer
{% endplantuml %}
 