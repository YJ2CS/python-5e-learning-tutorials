---
title: 1-1-介绍python对象类型
url: 1-1-介绍python对象类型
author: YJ2CS
avatar: '/custom/avatar.webp'
authorLink: YJ2CS.github.io
authorAbout: 愿青年摆脱了冷气，只是向前走！
authorDesc: 愿青年摆脱了冷气，只是向前走！
comments: true
categories:
  - 文章
tags:
  - 悦读
no-photos: 'https://random.52ecy.cn/randbg.php?size=1&rid-1-1-介绍python对象类型'
date: 2020-12-20 00:27:49
---



## 1. Python 核心数据类型

第5版第四章

引言：这些核心数据类型是在Python语言中高效创建的。所有人都该了解他们。

## **内置对象**  

对象类型|例子 常量/创建
---|---
数字|1234, 3.1415, 3+4j, 0b111, Decimal(), Fraction()
字符串|'spam', "guido's", b'a\xolc', u'sp\xc4m'
列表|[1, [2, 'three'], 4], list(range(10))
字典|{'food': 'spam', 'taste': 'yum'}, dict(hours=10)
元组|(1, 'spam', 4, 'U'), tuple('spam'), namedtuple
文件|open('eggs.txt'), open(r'C:\ham.bin', 'wb')
集合|set('abc'), {'a', 'b', 'c'}
其他类型|类型、None、布尔型
编程单元类型|函数、模块、类
与实现相关的类型|编译的代码，堆栈跟踪

## 2. 变量

```python
message = "Hello World"
print(message)
```

```python
    Hello World
```

这里message为一个变量，与字符串“Hello World”关联在一起。

- 变量名只能包含字母、数字和下划线，变量名可以字母或下划线开头，但不能以数字开头。
- 变量名不能包含空格，但可以使用下划线分隔其中单词。
- 不能将Python关键字和函数名用作函数名。
- 变量名应既简短又具有描述性。
- 慎用小写字母l和大写字母O。  

Python中有三个主要类型（以及操作）的分类：  

- 数字（整数、浮点数、二进制、分数等）  
    支持加法和乘法等。  
- 序列（字符串、列表、元组）  
    支持索引、分片和合并等。  
- 映射（字典）  
    支持通过键的索引等。  

Python中主要核心类型划分为如下两类：  

- **不可变类型**：数字、字符串、元组、不可变集合  
- **可变类型**：列表、字典、可变集合

```python

```

