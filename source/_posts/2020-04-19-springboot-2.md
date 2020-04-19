---
title: Springboot 自动装配初探（Springboot 编程思想5～6章小结）
date: 2020-04-19 17:57:52
tags: springboot
---

Springboot 门面注解：`@SpringBootApplication`

`@SpringBootApplication` 继承了以下三个注解，并通过 `@AliasFor` 代理了被继承注解的一些值设置：

```java
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = {
  @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
  @Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
```

`@ComponentScan` 用于扫描 `@Component` 组件

`@SpringBootConfiguration` 继承于 `@Configuration`，表示其为一个配置类

`@EnableAutoConfiguration` 是 springboot 实现自动化配置的核心注解，激活 **自动装配机制**。内部通过@Import注入了一个ImportSelector的现类 `AutoConfigurationImportSelector`，这个 `ImportSelector` 最终实现根据我们的配置，动态加载所需的bean.

`@SpringBootApplication` 类既可以标记在 Main 类上，也可以标记在其他类上面，最后由 `SpringApplication#run` 引导。

由 `@Bean` 生成的 Bean 根据实现的地方会有差异：

+ 在 `@Configuration` 下声明的 `@Bean` 属于 Full 模式，会有 CGLIB 增强（代理）
+ 其他的 Bean （比如 `@Component` 下声明）属于 Lite 模式，不会有 CGLIB 增强

创建一个自动装配类：

```java
// 1. 定义一个没有 @Configuration 注解的类
public class HelloConfig {
  @Bean("hello")
  public String hello(){
      return "Jihongyu";
  }
}

// 2. 定义自动配置类
@Configuration
@Import(HelloConfig.class)
public class HelloAutoConfig {
}

// 3. resources 目录下面新建 META-INF/spring.factories 文件，配置开启自动配置类
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.cmb.config.HelloAutoConfig
```

自动装配一般都会和 `@Conditional` 一起使用，对配置进行约束。`spring-boot-autoconfigure` 对其又进行了扩展，构建了 13 个 Conditional 扩展注解:

```java
@ConditionalOnProperty
@ConditionalOnBean
@ConditionalOnMissingBean
@ConditionalOnClass
@ConditionalOnMissingClass
@ConditionalOnExpression
@ConditionalOnSingleCandidate
@ConditionalOnResource
@ConditionalOnJndi
@ConditionalOnJava
@ConditionalOnWebApplication
@ConditionalOnNotWebApplication
@ConditionalOnCloudPlatform
```

这些 Conditional 也是可以按照 And、Or、Not 组合使用的，需要实现下面的抽象类:

```java
AllNestedConditions
AnyNestedCondition
NoneNestedConditions
```

（未完待续）
