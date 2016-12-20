---
title: Thinking in Java (1). 面向过程
date: 2016-11-15 23:03:03
tags: [Java, 入门]
---

# 前言

Java 入门第一篇。虽说 Java 里的骨子里流淌着的是 OOP 的思想，但入门这部分主要涉及变量类型，数据存储，初始化和析构等方面的内容，这其实是每个程序语言的基础知识。为了与后面的高级主题区别，所以我将这一部分称作 【面向过程】（其实叫做【入门过程】也未尝不可(/≧▽≦)/）。
<!--more-->

# 正文

java 的数值基本类型全是有符号的。

java 中每一个基本类型都对应这一个包装器类型。

java的基本类型存储在栈上，其他类型存储在堆上面。


java禁止内层作用域屏蔽外层作用域。例如下列代码C/C++合法，而java不合法
```java
{
    int x = 0;
    {
        int x = 1;
    }
}
```

使用未初始化的基本类型变量会**编译报错**，基本类型变量作为累的成员时会默认初始化。Java 杜绝了对象的未初始化现象。

`static` 关键字：单一特性，类特性

`java.lang` 是默认导入到每个java文件的。

java 的注释分为两种：

+ 普通注释：`//` 和 `/*   */`
+ 文档注释: `/** */`，可以嵌入HTML或文档标签，自动生成复杂的文档页面

基本类型，字符串，数组，包装类型，自定义类型数据的比较，赋值，参数传递问题

java 的三种位移操作符：左移操作符`<<`，右移操作符`>>`，无符号右移操作符`>>>`。

窄化转换必须要显示转换，而扩展转换则不必。基本类型扩展转换表，见书p81。

java 中的执行流控制语句中引入了 foreach 语法和多重跳出规则。

构造函数虽然不是 static 成员函数，但是它的行为确实是 static 函数的行为。

使用不同类型的参数或者是不同个数的参数可以达到函数重载的目的。函数重载不依赖于函数返回值。

在处理构造函数方面，java 与 C++ 是基本一致的。基本一致体现在 Java 中的 class 里至少有一个构造函数（手写或者自动生成）；C++ 中如果一个没有手写构造函数的 class 没有被实例化，编译器是不会自动生成默认构造函数的。

Java 可以在构造函数中调用构造函数，目的是简化构造函数代码。这跟 C++11 的某个特性很想，记不起来了(⊙v⊙)。 

Java 的一大卖点就是自动垃圾回收机制，高深的算法理论和设计机制就留给后面的章节再看吧。`finalize()` 函数也没有看懂。

class 数据初始化顺序：

+ static 成员数据自动初始化（按顺序来）
+ non-static 成员数据自动初始化
+ 构造函数

最好不要在同一个函数用同样的可变参数重载多次。