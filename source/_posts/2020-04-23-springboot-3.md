---
title: Springboot 注解驱动编程（Springboot 编程思想第7章）
date: 2020-04-23 23:05:19
tags: springboot
---

## 注解驱动发展史（不同 Spring 阶段的注解）

### Spring Framework 1.X

@ManagedResource、@Transactional

### Spring Framework 2.0

@Required、@Repository

<!--more-->


### Spring Framework 2.5

@Autowired、@Qualifier、@Component、@Service

MVC: @Controller、@RequestMapping、@ModelAttribute

@JSR-250: Resource、@PostConstruct、@PreDestory

### Spring Framework 3.X

@Configuration、@Import、@ComponentScan、@Bean、@DependsOn、@Role、@Profile

@RequestHeader、@CookieValue、@RequestPart、@ResponseBody、@ResponseStatus

@PropertyResource、@Validated、@Asyn、@Scheduled

接口：

+ Environment：属性存储接口
+ PropertySources：属性源抽象

Spring 3.1 引入 @Enable 模块

### Spring Framework 4.X

@Conditional、@Repeatable、@AliasFor

@CrossOrigin、@ControllerAdvice


### Java 的元注解

@Retention：生命周期
@Target：作用位置
@Documented：生成 JavaDoc 文档
@Inherited：传递性
@Repeatable：重复注解

### Spring 的元注解

@Component：Spring 组件

Spring 注解编程模型

+ 元注解 @Component
+ Spring 模式注解：元注解的继承（以及多重继承）
+ Spring 组合注解：注解的搭配
+ Spring 注解属性别名和覆盖规则

注：这里的注解继承需要打“引号”，它并不是通过继承或者实现某个类或接口来实现的。

Spring Metadata: 是 Spring 围绕 **注解编程** 增强 JDK 反射特性定义的新接口

+ ClassMetadata: 对 Class 的抽象
+ AnnotatedTypeMetadata: 对注解的抽象
+ AnnotationMetadata: 对 Class 的注解抽象
+ MethodMetadata: 对 Method 的注解抽象

（ps 以上类名取得不是很好，看名字稍微有点绕）

Spring Metadata 实现了两簇数据实现：Simple 簇（ASM）、Standard 簇（JDK）

AnnotationAttributes：Spring 对注解属性的抽象，是基于 LinkedHashMap 实现

注解属性覆盖有两种方式：

+ 隐式覆盖：子类同名注解覆盖父类同名注解
+ 显示覆盖：`@AliasFor` 指定覆盖

Spring 元注解之前最好不要互相标注，这个问题后面可以研究一下。
