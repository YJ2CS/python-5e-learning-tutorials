---
title: 2-3-while-和-for-循环
url: 2-3-while-和-for-循环
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
no-photos: 'https://random.52ecy.cn/randbg.php?size=1&rid-2-3-while-和-for-循环'
date: 2020-12-20 00:29:50
---



# 1. while 循环  
while 语句是 Python 语言中最通用的迭代结构。只要顶端测试一直计算到真值，就会重复执行一个语句块。  

## 1.1 一般格式  
while 语句最完整的书写格式是：首行以及测试表达式、有一列或多列缩进语句的主体以及一个可选的 else 部分（控制权离开循环而又没有碰到 break 语句时会执行）。Python 会一直计算开头的 test，然后执行循环主体内的语句，直到测试返回假值为止。

```python
while <test>:
    <statements1>
else:
    <statements2>
```

```python
x = 'spam'
while x:                       # 当 x 非空
    print(x, end=' ')
    x = x[1:]                   # 切掉字符串第一个字符
```

    spam pam am m 

```python
a = 0; b = 10
while a < b:
    print(a, end=' ')
    a += 1
```

    0 1 2 3 4 5 6 7 8 9 

Python 没有其他语言中所谓的“do until”循环语句，不过可以在循环主体底部以一个测试和 break 来实现类似的功能。

```python
while True:
    ...loop body...
    if exitTest(): break
```

# 2. break、continue、pass 和循环 else  
- **break：**跳出最近所在的循环（跳过整个循环语句）。
- **continue：**跳到最近所在循环的开头处（来到循环的首行）。
- **pass：**什么事也不做，只是空站位语句。
- **循环 else 块：**只有当循环正常离开时才会执行（也就是没有碰到 break 语句）。  

## 2.1 一般循环格式  
加入 break 和 continue 语句后，while 循环的一般格式如下所示。

```python
while <test1>:
    <statements1>
    if <test2>: break
    if <test3>: continue
else:
    <statements2>
```

break 和 continue 可以出现在 while（或 for）循环主体的任何地方，但通常会进一步嵌套在 if 语句中，根据某些条件来采取对应的操作。

## 2.2 pass  
pass 语句是无运算的占位语句，当语法需要语句并且还没有任何实用的语句可写时，就可以使用它。它通常用于为复合语句编写一个空的主体。  

pass 有时指的是“以后会填上”，只是暂时用于填充函数主体而已：

```python
def func1():
    pass
```

Python 3.X 允许在可以使用表达式的任何地方使用 ...（三个连续的点号）来省略代码。由于省略号自身什么也不做，这可以当做是 pass 语句的一种替代方案，尤其是对于随后填充的代码——这是 Python 的“TBD”（未确定内容）的一种：

```python
def func1():
    ...
```

省略号可以和语句头出现在同一行，并且，如果不需要具体类型的话，可以用来初始化变量名：

```python
def func1(): ...
```

```python
X = ...
X
```

    Ellipsis

## 2.3 continue  
continue 语句会立即跳到循环的顶端。偶尔也避免语句的嵌套。

```python
x = 10
while x:
    x = x-1
    if x % 2 != 0: continue
    print(x, end=' ')
```

    8 6 4 2 0 

## 2.4 break  
break 语句会立刻离开循环。有时可以引入 break 来避免嵌套化。

```python
while True:
    name = input('Enter name: ')
    if name == 'stop': break
    age = input('Enter age: ')
    print('Hello', name, '=>', int(age) ** 2)
```

    Enter name: mel
    Enter age: 40
    Hello mel => 1600
    Enter name: stop

## 2.5 循环 else  
和循环 else 子句结合时，break 语句通常可以忽略其他语言中所需的搜索状态标志位。  

例如，下列程序搜索大于 1 的因子，来决定正整数 y 是否为质数。

```python
x = y // 2                             # 对于 y > 1
while x > 1:
    if y % x == 0:                     # 余数
        print(y, 'has factor', x)
        break                           
    x -= 1
else:                                  # 正常退出
    print(y, 'is prime')
```

除了设置标志位在循环结束时进行测试外，也可以在找到因子时插入 break。这样一来，循环 else 分句可以视为只有当没有找到因子时才会执行。如果没碰到 break，该数就是质数。  

如果循环主体从没有执行过，循环 else 分句可会执行，因为你没在其中执行 break 语句。  

**关于循环 else 分句的更多内容**  
循环 else 分句提供了常见的编写代码的明确语法：这是编写代码的结构，让你捕捉循环的“另一条”出路，而不通过设定和检查标志位或条件。  

假设要写个循环搜索列表的值，而且需要知道在离开循环后该值是否已经找到，使用标志位的方法为：

```python
found = False
while x and not found:
    if match(x[0]):
        print('Ni')
        found = True
    else:
        x = x[1:]
if not found:
    print('not found')
```

else 的等效版本：

```python
while x:
    if match(x[0]):
        print('Ni')
        break
    x = x[1:]
else:
    print('Not found')
```

while 主体内的 break 会离开循环并跳过 else，因此可作为捕捉搜索失败的情况更为结构化的方式。

# 3. for 循环  
for 循环是一个通用的序列迭代器：可以遍历任何有序的序列对象内的元素。  

for 语句可用于字符串、列表、元组、其他内置可迭代对象以及通过类所创建的新对象。  

## 3.1 一般格式  

```python
for <target> in <object>:      # 将 object 中的项赋值给 target
    <statements1>              # 重复主体：使用 target
else:
    <statements2>              # 如果没遇到 'break'
```

当 Pytorch 运行 for 循环时，会逐个将序列对象中的元素赋值给目标，然后为每个元素执行循环主体。  

for 语句也支持一个选用的 else 块，就像在 while 循环中一样。  

**基本应用**

```python
for x in ['spam', 'eggs', 'ham']:
    print(x, end=' ')
```

    spam eggs ham 

```python
sum = 0
for x in [1, 2, 3, 4]:
    sum = sum + x
sum
```

    10

**其他数据类型**

```python
S = 'lumberjack'
T = ('and', "I'm", 'okay')
for x in S: print(x, end=' ')         # 迭代字符串
```

    l u m b e r j a c k 

```python
for x in T: print(x, end=' ')         # 迭代元组
```

    and I'm okay 

**在 for 循环中的元组赋值**  
如果迭代元组序列，循环目标本身实际上可以是目标元组。

```python
T = [(1, 2), (3, 4), (5, 6)]
for (a, b) in T:
    print(a, b)
```

    1 2
    3 4
    5 6

在 Python 中，它通常还和 SQL 数据库一起使用——外围的列表就是数据库表，嵌套的元组是表中的行，元组赋值和列对应。  

for 循环中的元组使得用 items 方法来遍历字典中的键和值变得很方便，而不必再遍历键并手动地索引以获取值：

```python
D = {'a': 1, 'b': 2, 'c': 3}
for key in D: 
    print(key, '=>', D[key])           # 使用字典键迭代和索引
```

    a => 1
    b => 2
    c => 3

```python
list(D.items())
```

    [('a', 1), ('b', 2), ('c', 3)]

```python
for (key, value) in D.items():
    print(key, '=>', value)            # 迭代键和值
```

    a => 1
    b => 2
    c => 3

for 循环中的元组赋值并非一种特殊情况；单词 for 之后的任何赋值目标在语法上都是有效地，尽管我们总是在 for 循环中手动地赋值以解包：

```python
T = [(1, 2), (3, 4), (5, 6)]
for both in T:
    a, b = both             # 手动赋值
    print(a, b)
```

    1 2
    3 4
    5 6

嵌套结构也能够自动解包：

```python
for ((a, b), c) in [([1, 2], 3), ['XY', 6]]:
    print(a, b, c)
```

    1 2 3
    X Y 6

**Python 3.X 在 for 循环中扩展的序列赋值**  
由于一个序列可以赋值给一组更为通用的名称（其中有一个带有星号的名称收集多个元素），我们可以在 for 循环中使用同样的语法来提取嵌套的序列的部分：  

```python
a, *b, c = (1, 2, 3, 4)       # 扩展序列赋值
a, b, c
```

    (1, [2, 3], 4)

```python
for (a, *b, c) in [(1, 2, 3, 4), (5, 6, 7, 8)]:
    print(a, b, c)
```

    1 [2, 3] 4
    5 [6, 7] 8

**嵌套 for 循环**  

```python
items = ['aaa', 111, (4, 5), 2.01]            # 对象集合
tests = [(4, 5), 3.14]                        # 需要搜索的键

for key in tests:
    for item in items:
        if item == key:
            print(key, 'was found')
            break
    else:
        print(key, 'not found!')
```

    (4, 5) was found
    3.14 not found!

外层循环扫描键列表，内层循环为每个键扫描元素列表。

```python
for key in tests:
    if key in items:
        print(key, 'was found')
    else:
        print(key, 'not found!')
```

    (4, 5) was found
    3.14 not found!

for 执行典型的数据结构任务：收集两个序列（字符串）中相同的元素。在循环执行后，res 引用的列表中包含 seq1 和 seq2 中找到的所有元素。

```python
seq1 = 'spam'
seq2 = 'scam'

res = []                     # 从空列表开始
for x in seq1:               # 扫描第一个序列
    if x in seq2:            # 是否是共同项
        res.append(x)        # 添加结果到列表
res
```

    ['s', 'a', 'm']

# 4. 编写循环的技巧  
一般而言，for 比 while 容易写，执行时也比较快。  

有时需要以更为特定的方式来进行迭代。  

Python 提供了两个内置函数，在 for 循环内定制迭代：
- 内置 range 函数返回一系列连续增加的整数，可作为 for 中的索引。
- 内置 zip 函数返回并行元素的元组的列表，可用于在 for 中遍历数个序列。
- 内置 enumerate 函数在迭代器中生成元素的值和索引，因此不必手动计数。

## 4.1 循环计数器：range  
range 常用在 for 循环中来产生索引，但也可以用在任何需要整数列表的地方。  

在 Python 3.X 中，range 是一个迭代器，会根据需要产生元素，因此，我们需要将其包含到一个 list 调用中以一次性显示其结果：

```python
list(range(5))
```

    [0, 1, 2, 3, 4]

```python
list(range(2, 5))
```

    [2, 3, 4]

```python
list(range(0, 6, 2))
```

    [0, 2, 4]

传入一个参数时，Python 会产生从零算起的整数列表，但其中不包括该参数的值。  

传入两个参数时，第一个将视为下界。  

第三个选用参数可以提供步进值，默认是1。  

range 也可以是非整数或非递增的：

```python
list(range(-5, 5))
```

    [-5, -4, -3, -2, -1, 0, 1, 2, 3, 4]

```python
list(range(5, -5, -1))
```

    [5, 4, 3, 2, 1, 0, -1, -2, -3, -4]

Python 3.X 中，for 循环迫使 range 结果自动化，因此不需要使用 list。

```python
for i in range(3):
    print(i, 'Pythons')
```

    0 Pythons
    1 Pythons
    2 Pythons

在可能的情况下，最好使用 Python 中的简单的 for 循环，不要用 while， 并且不要在 for 循环中使用 range 调用，只将其视为最后的手段。  

## 4.2 序列排列：range 和 len  
一些算法可以使用序列重排序——在搜索中生成替代选择，来测试不同的值排序的效果。这种情况可能需要偏移量，以便将序列分开并将它们重新放在一起。range 在第一个例子中提供重复计数，在第二个例子提供切片的位置：

```python
S = 'spam'
for i in range(len(S)):       # 重复 0-3
    S = S[1:] + S[:1]         # 将头部项移到尾部
    print(S, end=' ')
```

    pams amsp mspa spam 

```python
for i in range(len(S)):
    X = S[i:] + S[:i]          # 后面部分 + 前面部分
    print(X, end=' ')
```

    spam pams amsp mspa 

第二种方法产生的结果与第一种方法相同，尽管顺序不同，但是不会改变原始变量。因为两个分片都可以得到要连接的部分，所以它们也可以处理任何类型的序列，并返回与正在排序的序列相同的类型的序列——如果你排序一个列表，你就创建了重新排序的列表:

```python
L = [1, 2, 3]
for i in range(len(L)):
    X = L[i:] + L[:i]
    print(X, end=' ')
```

    [1, 2, 3] [2, 3, 1] [3, 1, 2] 

## 4.3 非完备遍历：range和分片  
前面部分中 range/len 组合的情况是很有用的应用。我们也可以使用这个技术来跳过一些元素：

```python
S = 'abcdefghijk'
list(range(0, len(S), 2))
```

    [0, 2, 4, 6, 8, 10]

```python
for i in range(0, len(S), 2):
    print(S[i], end=' ')
```

    a c e g i k 

通过这种方式使用 range 来跳过循环内的元素，依然保持了 for 循环的简单性。  

但这可能不是如今 Python 中理想情况下最现实的技术。分片表达式提供了实现相同目标的更简单的办法：

```python
S = 'abcdefghijk'
for c in S[::2]:
    print(c, end=' ')
```

    a c e g i k 

这里使用 range 的唯一优点是——它没有复制字符串，并且不会在 Python 3.X 中创建一个列表，对于很大的字符串来说，这会节省内存。

## 4.4 修改列表：range 和表达式  
可以使用 range/len 和 for 组合的常见场合就是在循环中遍历列表时对齐进行修改。例如，假设你因某种理由要为列表中每个元素都加1。可以通过简单的 for 循环来做，但可能给并不是你想要的。

```python
L = [1, 2, 3, 4, 5]
for x in L:
    x += 1             # 改变 x，而不是 L
L
```

    [1, 2, 3, 4, 5]

```python
x
```

    6

这样修改的是循环变量 x，而不是列表 L。要真的在遍历列表时对其进行修改，我们需要使用索引。

```python
L = [1, 2, 3, 4, 5]
for i in range(len(L)):      # 对 L 中的每一项加 1
    L[i] += 1
L
```

    [2, 3, 4, 5, 6]

range 的解决方案依然不理想。

```python
[x + 1 for x in L]
```

    [3, 4, 5, 6, 7]

列表解析表达式也能做类似的工作，并且运行更快，没有对最初的列表进行在原处的修改（我们可以把表达式的新列表对象赋值给L，但是这样不会更新原始列表的其他任何引用值）。

## 4.5 并行遍历：zip 和 map  
在基本运算中，zip 会取得一个或多个序列为参数，然后返回元组的列表，将这些序列中的并排的元素配成对。  

和 range 一样，zip 在 Python 3.X 中也是一个可迭代对象，因此，我们必须将其包含在一个 list 调用中以便一次性显示所有结果。

```python
L1 = [1, 2, 3, 4]
L2 = [5, 6, 7, 8]
zip(L1, L2)
```

    <zip at 0x24556a44f48>

```python
list(zip(L1, L2))
```

    [(1, 5), (2, 6), (3, 7), (4, 8)]

这样的结果在其他环境下也有用，然而搭配 for 循环时，它就会支持并行迭代。

```python
for (x, y) in zip(L1, L2):
    print(x, y, '--', x + y)
```

    1 5 -- 6
    2 6 -- 8
    3 7 -- 10
    4 8 -- 12

zip 可以接受任何类型的序列（包括文件），并且可以由两个以上的参数。  

对于三个参数，它构建了 3 元素元组的一个列表，其中带有来自每个序列的元素，基本上按照列对应。

```python
T1, T2, T3 = (1, 2, 3), (4, 5, 6), (7, 8, 9)
list(zip(T1, T2, T3)) 
```

    [(1, 4, 7), (2, 5, 8), (3, 6, 9)]

当参数长度不同时，zip 会以最短序列的长度为准来截断所得到的元组。

```python
S1 = 'abc'
S2 = 'xyz123'
list(zip(S1, S2))
```

    [('a', 'x'), ('b', 'y'), ('c', 'z')]

**使用 zip 构造字典**  
将列表变成字典的一种做法就是将这些字符串 zip 起来，直接把 zip 过的键/值列表传给内置的 dict 构造函数。

```python
keys = ['spam', 'eggs', 'toast']
vals = [1, 3, 5]
D3 = dict(zip(keys, vals))
D3
```

    {'eggs': 3, 'spam': 1, 'toast': 5}

```python
keys = ['spam', 'eggs', 'toast']
vals = [1, 3, 5]
{k: v for (k, v) in zip(keys, vals)}
```

    {'spam': 1, 'eggs': 3, 'toast': 5}

## 4.5 产生偏移和元素：enumerate  
在有些程序中，我们需要用到元素以及这个元素的偏移值。enumerate 函数可以为我们做这件事。

```python
S = 'spam'
for (offset, item) in enumerate(S):
    print(item, 'appears at offset', offset)
```

    s appears at offset 0
    p appears at offset 1
    a appears at offset 2
    m appears at offset 3

enumerate 函数返回一个生成器对象：这种对象支持迭代协议。我们可以在 for 循环中通过元组赋值运算将元组解包：

```python
E = enumerate(S)
E
```

    <enumerate at 0x24556a46168>

```python
next(E)
```

    (0, 's')

```python
next(E)
```

    (1, 'p')

```python
next(E)
```

    (2, 'a')

```python
[c * i for (i, c) in enumerate(S)]
```

    ['', 'p', 'aa', 'mmm']

