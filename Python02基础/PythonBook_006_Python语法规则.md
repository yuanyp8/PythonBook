# Python基础语法规范
—————
![](https://github.com/Yuanyp8/pict/blob/master/python%E7%BC%96%E7%A8%8B%E8%A7%84%E8%8C%83.jpg?raw=true)
## 注释

### 单行注释
单行住释用`#`表示，例如：

```
# 这是单行注释
```

### 多行注释
多行注释用`"""`包围起来，例如：

```
"""
这是
多行
注释
"""
```


## 数字

### 整数
- python3开始不区分`long`和`int`，`long`被重命名为`int`，所以整数只有`int`.因此也没有了整数型的限制，可以很大很大，大到内存放不下...
>比如，Mysql的int类型有很多种，能插入多大的值都是有限定的

```
In [2]: type(100)
Out[2]: int

In [3]: type(10000000000000000)
Out[3]: int

In [4]: type(2**10000)
Out[4]: int
# 可以看到，无论数字多大(2的10000次方)，都是int类型
```

- bool值，包括`True`和`False`，比较常用

```
In [10]: type(True)
Out[10]: bool

In [11]: type(False)
Out[11]: bool
```

### 浮点数
- `1.2`、`-0.287`、`3.5555554`都是浮点数
- 本质上采用了C语言的double类型，因此描述的数据非常大，超乎你想象；所以对于基本的开发绰绰有余

```
In [16]: type(0.423432)
Out[16]: float
```


### 复数
- `1+2j`

```
In [19]: type (1 + 2j)
Out[19]: complex
```


## 字符串
使用`"`或者`’`包起来的字符序列

```
In [12]: c = "2"

In [13]: type(c)
Out[13]: str

In [14]: a = 'string'

In [15]: type(a)
Out[15]: str
```


### 三引号
- 三引号是python引进的一种用法，分为`"""`和`‘’‘`
- 在三引号中可以随意的使用和添加单/双引号和换行符等

```
InIn [20]: type(''' 我是字符串‘“'" ''')

Out[20]: str
```


### r前缀
在字符串前面加上`r`或者`R`前缀，表示该字符串不做特殊处理

```
In [23]: print('d\ngrgr')
d
grgr

In [24]: print(r'd\ngrgr')
d\ngrgr

In [24]: print('d\\ngrgr')
d\ngrgr

In [34]: print("aaa     bbbb\naaa\tbbbb")
aaa     bbbb
aaa     bbbb
```



### f前缀
在字符串前面加上`f`前缀，格式化字符串，仅支持3.6版本以上

## 缩进
- 未使用C等语言的花括号,而是采用缩进的方式表示层次关系
- 约定使用4个空格缩进

### 缺点
利用C语言等花括号进行编写的语言，可以将换行符缩进等完全压缩到一行代码，也就是前端技术`CSS`或`JS`压缩。
压缩之后可以成为一行代码，节省前端的字节数。

## 续行
- 在行尾使用`\`

```
In [40]: 'sssssssssssssssss\
    ...: sssssss'
Out[40]: 'ssssssssssssssssssssssss'
```

## 标识符
一个名字，用来指定一个值

### 大小写敏感

```
In [41]: abc = "dddd"

In [42]: ABC = "eeee"

In [43]: print(abc,ABC)
dddd eeee
```

### 变量可以字母开头，也可以下划线开头，不能用数字开头！

```
In [44]: a_1 = 2

In [45]: 1a =2
  File "<ipython-input-45-aad01bb6808c>", line 1
    1a =2
     ^
SyntaxError: invalid syntax
```

>- 一般以小写字母定义标识符就可以，大写字母一般表示类，_也有特殊含义
- 也不要使用有歧义的单词，如def、class等
- 一般禁止使用中文变量-_-（容易出锅）


## 常量
- 一旦赋值就不能改变值的变量
例如linux系统的hostname，但是在python，没有任何常量

>所以如此自由的语言，应该心存敬畏，有自己的编程规范


## 字面常量
- 一个单独的量，如`12`,`100`,'abc'
- 看见12，你就知道是12，12不可能是13
