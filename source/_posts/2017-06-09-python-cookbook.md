---
title: python cookbook
date: 2017-06-09 15:40:07
tags: [Python, 读书]
---

Python 进阶必备

<!--more-->

# Chapter 1：数据结构与算法

本章介绍了 Python 内置数据类型的使用技巧与方法。
由于 Python 是脚本语言，所以在 Python 编码的过程中，我们应当使用其内置的方法（built-in）。因为这些方法大多数是由 **C** 实现的，有极高的效率。
本章围绕着 Python 的内置内省，主要介绍了三个主要的内置模块：**collections**、**itertools**、**operator**。

+ collections：该模块基于内置类型（dict、list、set和tuple）实现了一些更高级的数据结构类型。
+ itertools：该模块实现了一组快速的、内存高效的“迭代器代数”工具。
+ operator：该模块提供一组高效的与内置运算符对应的函数。这些函数包括执行对象比较、逻辑操作、数学运算和序列操作的类别。

此外，本章好介绍了一些有效的内置函数。有效的使用这些函数可以很好的提高编码和程序执行的效率。这些函数包括但不限于：slice、sorted、filter、compress、any/all等等。

所以，一般对于 Python 程序设计，若使用相同的算法，则程序越短效率越高。

# Chapter 2：字符串和文本

本章主要涉及字符串和文本的处理。由于 Python 内置的函数和方法，使得对文本的处理极大地便利化。Python 的文本处理方法主要分为两大块：基于 **字符串** 的处理和基于 **正则表达式** 的处理。由于生产任务的需要，通常将文本的处理分为以下几类，同时也罗列了相关的只要函数和方法：

1. 切分：`re.split`、`str.split`
2. 匹配：
    1. 查找：`str.find`、`str.startwith`、`str.endwith`、正则匹配
    2. 替换：`str.replace`、`str.transform`、`re.sub` 
3. 删除：`str.lstrip/rstrip/strip`
4. 格式化：`str.ljust/rjust/center`、`str.format`、string 模板、C风格格式化
5. 合并字符串：`str.join`、运算符 **加号**
6. 正则匹配：
    1. 组模式
    2. 贪婪匹配
    3. 多行匹配

本章介绍了基本正则表达式使用方法，可以适用于许多场景，但是为了更加高效的使用，我们还需要深入的学习，参见《Python 核心编程（第三版）》第一章的内容。

# Chapter 3：数字、日期和时间

本章介绍了 Python 处理数值数据和时间数据的方法。进行精确计数（金融）的应用场景应当使用 `decimal` 模块。2、8、16进制字符串生成函数：`bin`、`oct`、`hex`。检测 **INF**、**NaN** 函数：`math.isinf`和`math.isnan`。时间处理主要涉及内置模块 `datetime` 和第三方模块 `dateutil`。

Python 本身的数据处理能力较弱，不建议使用内置 Python 方法进行数据处理。我们应当是用 Numpy、Scipy 等第三方数学库进行科学计算。

# Chapter 4：迭代器和生成器

## 迭代协议

Python 支持在容器（container）上进行迭代。需要为容器对象定义一种方法来提供迭代支持：

`container.__iter__()` 返回一个迭代器对象。该对象需要支持 **迭代器协议**。

迭代器对象本身需要支持以下两种方法，它们一起形成迭代器协议：

+ `iterator.__iter__()`
返回迭代器对象本身。这是允许容器和迭代器与for和in语句一起使用的。该方法对应于Python / C API中Python对象的类型结构的 `tp_iter` slot。

+ `iterator.__next__()`
从容器返回下一个元素。如果没有下一元素，则会引发 `StopIteration` 异常。该方法对应于Python / C API中Python对象的类型结构的 `tp_iternext` slot。

Python 的生成器（generator）提供了实现迭代器协议的便捷方式。 如果容器对象的 `__iter__()` 方法被实现为生成器，它将自动返回一个提供 `__iter __()` 和 `__next __()` 方法的迭代器对象（技术上是一个生成器对象）。 