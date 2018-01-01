http://www.cnblogs.com/spiritman/p/5158331.html

Python迭代器(Iterator)
概述

　　迭代器是访问集合元素的一种方式。迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退。

延迟计算或惰性求值 (Lazy evaluation)

　　迭代器不要求你事先准备好整个迭代过程中所有的元素。仅仅是在迭代至某个元素时才计算该元素，而在这之前或之后，元素可以不存在或者被销毁。这个特点使得它特别适合用于遍历一些巨大的或是无限的集合。

可迭代对象

　　迭代器提供了一个统一的访问集合的接口。只要是实现了__iter__()或__getitem__()方法的对象，就可以使用迭代器进行访问。

　　序列：字符串、列表、元组

　　非序列：字典、文件

　　自定义类：用户自定义的类实现了__iter__()或__getitem__()方法的对象

创建迭代器对象

　　使用内建的工厂函数iter(iterable)可以获取迭代器对象：

　　语法：

　　　　iter(collection) -> iterator

　　　　iter(callable,sentinel) -> iterator

　　说明：

　　　　Get an iterator from an object. 

　　　　In the first form, the argument must supply its own iterator, or be a sequence.

　　　　In the second form, the callable is called until it returns the sentinel.

　　实例展示：

说明：

　　for循环可用于任何可迭代对象

　　for循环开始时，会通过迭代协议传输给iter()内置函数，从而能够从迭代对象中获得一个迭代器，返回的对象含有需要的next()方法。

http://blog.csdn.net/passionkk/article/details/49929887
  
Python 中 Iterator和Iterable的区别

Python中 list，truple，str，dict这些都可以被迭代，但他们并不是迭代器。为什么？
因为和迭代器相比有一个很大的不同，list/truple/map/dict这些数据的大小是确定的，也就是说有多少事可知的。
但迭代器不是，迭代器不知道要执行多少次，所以可以理解为不知道有多少个元素，每调用一次next()，就会往下走一步，是惰性的。

判断是不是可以迭代，用Iterable：
```
from collections import Iterable  
isinstance({}, Iterable) --> True  
isinstance((), Iterable) --> True  
isinstance(100, Iterable) --> False
```

判断是不是迭代器，用Iterator：
```
from collections import Iterator  
isinstance({}, Iterator)  --> False  
isinstance((), Iterator) --> False  
isinstance( (x for x in range(10)), Iterator)  --> True
```

所以，凡是可以for循环的，都是Iterable；凡是可以next()的，都是Iterator！
集合数据类型如list，truple，dict，str，都是Itrable不是Iterator，但可以通过iter()函数获得一个Iterator对象
Python中的for循环就是通过next实现的：

```
#先获取iterator对象  
it = iter([1,2,3,4,5])  
while True:  
    try:  
        #获取下一个值  
        x = next(it);  
    except StopIteration:  
        # 遇到StopIteration就退出循环  
        break
```

```
#!/usr/bin/env python

import time

ai = [1,2,3,4,5]

for x in ai:
    print x

iter = ai.__iter__()

while True:
    try:
        e = iter.next()
        print e
        time.sleep(1)
    except StopIteration:
        print "end of iter"
        break
```
