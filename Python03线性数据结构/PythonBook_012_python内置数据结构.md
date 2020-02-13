# Python内置数据结构

## 数值型
int、float、complex、bool都是class类型，对象即实例
### 常见的数值型函数
#### int
python3中的`int`就是长整数类型，本身没有大小限制，受限于内存区域的大小

#### float
由整数类型和小数部分组成，支持十进制和科学记数法，是C语言的双精度类型实现的

#### complex
由实数和虚数部分组成，实数和虚数都是浮点数
#### bool
int的子类，近有两个实例`True`和`False`，分别对应`1`和`0`，可以直接和整数计算


## 类型转换(build—in)
### int()
int(x)返回一个整数,如遇到小数则只保留整数部分

```
>>> int(4.3)
4
>>> int(4.7)
4
>>> int(-4.4)
-4
```

### math()

#### math.ceil()
向上取整,取天花板值

```
>>> math.ceil(2.49)
3
>>> math.ceil(2.9)
3
>>> math.ceil(-2.1)
-2
```

#### math.floor()
向下取值，取地板值

```
>>> math.floor(2.9)
2
>>> math.floor(-2.9)
-3
```

### round
- 四舍六入，遇5取最近的偶数
- 遇到负号先运行四舍六入，再考虑负号

```
>>> round(2.1)
2
>>> round(2.9)
3
>>> round(-2.1)
-2
>>> round(-2.9)
-3

>>> round(2.5)  # 2.5距离2近，距离4远，取2
2
>>> round(3.5)  # 3.5距离4近，距离2远，取4
4
```


### abs()
返回一个数的绝对值。实参可以是整数或浮点数。如果实参是一个复数，返回它的模

```
>>> abs(-2)
2
>>> 1+4j
(1+4j)
>>> abs(-(1+4j))
4.123105625617661

```


### all(iterable)

如果 iterable 的所有元素为真（或迭代器为空），返回 True 。
> 元素除了是 0、空、None、False 外都算 True。

函数等价于：
```
def all(iterable):
    for element in iterable:
        if not element:
            return False
    return True
```


```
>>> all(['a', 'b', 'c', 'd'])  # 列表list，元素都不为空或0
True
>>> all(['a', 'b', '', 'd'])   # 列表list，存在一个为空的元素
False
>>> all([0, 1，2, 3])          # 列表list，存在一个为0的元素
False

>>> all(('a', 'b', 'c', 'd'))  # 元组tuple，元素都不为空或0
True
>>> all(('a', 'b', '', 'd'))   # 元组tuple，存在一个为空的元素
False
>>> all((0, 1, 2, 3))          # 元组tuple，存在一个为0的元素
False

>>> all([])             # 空列表
True
>>> all(())             # 空元组
True

```
### any(iterable)
any() 函数用于判断给定的可迭代参数 iterable 是否全部为 False，则返回 False，如果有一个为 True，则返回 True。
但是如果可迭代对象为空，返回False
> 元素除了是 0、空、FALSE 外都算 TRUE。

函数等价于：

```
def any(iterable):
    for element in iterable:
        if element:
            return True
    return False
```

```
>>>any(['a', 'b', 'c', 'd'])  # 列表list，元素都不为空或0
True

>>> any(['a', 'b', '', 'd'])   # 列表list，存在一个为空的元素
True

>>> any([0, '', False])        # 列表list,元素全为0,'',false
False

>>> any(('a', 'b', 'c', 'd'))  # 元组tuple，元素都不为空或0
True

>>> any(('a', 'b', '', 'd'))   # 元组tuple，存在一个为空的元素
True

>>> any((0, '', False))        # 元组tuple，元素全为0,'',false
False

>>> any([]) # 空列表
False

>>> any(()) # 空元组
False
```

### bin()
返回一个整数 int 或者长整数 long int 的二进制表示


```
>>>bin(10)
'0b1010'
>>> bin(20)
'0b10100'
```


### oct()
函数将一个整数转换成8进制字符串。

```
>>>oct(10)
'012'
>>> oct(20)
'024'
>>> oct(15)
'017'
>>>

```


### hex()
函数用于将10进制整数转换成16进制，以字符串形式表示。

```
>>>hex(255)
'0xff'
>>> hex(-42)
'-0x2a'
>>> hex(1L)
'0x1L'
>>> hex(12)
'0xc'
>>> type(hex(12))
<class 'str'>      # 字符串
```



### bool()
函数用于将给定参数转换为布尔类型，如果没有参数，返回 False。
>bool 是 int 的子类。

```
>>>bool()
False
>>> bool(0)
False
>>> bool(1)
True
>>> bool(2)
True
>>> issubclass(bool, int)  # bool 是 int 子类
True
```

### min()
min() 方法返回给定参数的最小值，参数可以为序列。

```
>>> min([33])
33
>>> min([3,5,6])
3
```

### max()
与min()对应，返回可迭代对象的最大值

```
>>> max([2,4])
4
```

### pow()
返回 x^y（x的y次方） 的值。


#### math.pow()
```
>>> math.pow(2,3)
8.0
>>> math.pow(2,0.5)
1.4142135623730951

```

#### 内置pow()

```
>>> pow(2,3)
8
```

### type
如果你只有第一个参数则返回对象的类型，三个参数返回新的类型对象。
>isinstance() 与 type() 区别：
- type() 不会认为子类是一种父类类型，不考虑继承关系。
- isinstance() 会认为子类是一种父类类型，考虑继承关系。
- 如果要判断两个类型是否相同推荐使用 isinstance()。

```
>>> type(6)
<class 'int'>
>>> type(6) == int
True
>>> type(6) == 'int'
False

##隐式类型转换(看来强类型转换，也有隐式类型转换)
>>> type(1+True+2.2)
<class 'float'>
```

### isinstance
isinstance() 函数来判断一个对象是否是一个已知的类型，类似 type()。

```
>>>a = 2
>>> isinstance (a,int)
True
>>> isinstance (a,str)
False
>>> isinstance (a,(str,int,list))    # 是元组中的一个返回 True
True

isinstance能判断子类
>>> isinstance(False,int)
True
>>> type(False) == int
False
```
