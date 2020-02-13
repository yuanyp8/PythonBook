# python函数

## 数学的定义
 `y = f(x)`,y是x的函数，x是自变量，`y=f(x0,x1...xn)`

## python中的函数
- 由若干语句组成的语句块，函数名称、参数列表构成、它是组织代码的最小单元
- 完成一定的功能

## 函数的作用
- 结构化编程对代码的最基本的封装，一般按照功能组织一段代码
- 封装的目的是为了复用，减少冗余代码
- 代码更加简洁，可读性更高

## 函数的分类
- 内建函数，如print()、max()等
- 库函数，如math.ceil()
- 自定义函数，使用def关键字


## 函数的定义

```python
def 函数名(参数列表)：
    函数体或代码块
    [return 返回值]
```
- 函数名就是标识符，命名要求一样
- 语句块必须缩进，约定四个空格
- python的函数没有return语句，会返回一个None值
- 定义中的参数列表称为**形式参数**，只是一种符号表达（标识符），简称形参

## 函数调用
- 函定义时，只是声明了一个函数，它不能被执行，需要调用执行
- 调用的方式，就是函数名后面加括号，如有必要则传日参数
- 调用时写入的是实际参数，是实实在在的值，简称实参
先定义一个函数

```python
>>> def add(x,y):  # 函数定义
	s= x+y    # 函数体
	return s  # 返回值
```

然后再调用

```python
>>> add(1,2)
3
```


>上面代码的解释：
- 定义一个函数add，函数名为add，接受两个参数
- 该函数的计算结果，通过返回值返回，需要return语句
- 调用时，通过函数名add()，里面有两个参数，返回值可使用变量接受
- 函数名也是标识符，返回值也是值
- 定义要在调用前，调用时如果没有定义函数，会NameError
- 函数是可调用对象，callable()





### 查看函数是不是可调用
```python
>>> add(1,2)
3
>>> callable(add)
True
>>> callable(1)
False
>>> callable(add(2,3))
False
```


## 传参

### 按位传参


```python
>>> def add(x,y):
	s = x+y
	return s

>>> add(1,2)
3

>>> add(1)
Traceback (most recent call last):
  File "<pyshell#53>", line 1, in <module>
    add(1)
TypeError: add() missing 1 required positional argument: 'y'
>>> add()
Traceback (most recent call last):
  File "<pyshell#54>", line 1, in <module>
    add()
TypeError: add() missing 2 required positional arguments: 'x' and 'y'

```


### 关键字传参

```python
>>> def add(x,y):
	s = x+y
	return s
>>> add(1,2)
3
>>> add(y = 1,x=2)
3
>>> add(x=1,y=2)
3
>>> add(2,y=3)
5
```
>如果位置参数和关键字参数同时存在，位置传参必须在关键字参数之前


## 缺省值


```python
>>> def sum(x=1,y=1):
	result = x/y
	return result

>>> sum()
1.0
>>> sum(2)
2.0
>>> sum(y = 10)
0.1
>>> sum(5,y=2)
2.5
```

### 形参的定义
```python
>>> def add(x,y=4):
	s = x+y
	return s

>>> add(1)
5
>>> add(1,2)
3
>>> add(x=1,y=3)
4
>>> def ad(x=4,y):
	s = x+y

SyntaxError: non-default argument follows default argument
```

>对于形参来说，也是同样的定义，位置参数在前面，关键字参数在后面，位置取反不可取（带等号的往后靠！！！）


## 练习

### login函数

```python
>>> def login(user='root',ip='127.0.0.1',password='abc123',port='22'):
	print("ssh {}@{}:{} {}".format(user,ip,port,password))

>>> login(user = "apache")
ssh apache@127.0.0.1:22 abc123
>>> login(password="aabbcc",ip="10.67.203.100")
ssh root@10.67.203.100:22 aabbcc
```

### 多参数求和
弄一个可迭代对象
```python
>>> def sums(iterable):
	result = 0
	for i in iterable:
	    result += i
	return result

>>> sums([1,2,3,4])
10
>>> sums((1,2,3,4))
10
>>> sums({1,2,3,4})
10
>>>
```
这样麻烦，可不可以考虑生成一个可迭代对象


```python
>>> def sums(*iterable):
	result = 0
	for i in iterable:
            result += i
	print("type(iterable)",result,iterable)

>>> sums(1,2,3)
type(iterable) 6 (1, 2, 3)
```



## 可变参数

1. 可变位置参数
    - 在形参前面使用*表示该形参是可变位置参数，可以接受多个实参
    - 它将收集到的实参组织到一个tuple中
2.  可变关键字参数
    - 在形参前面使用**表示该形参是可变关键字参数，可以接受多个关键字参数
    - 它将收集到的实参的名称和值，组织到一个dict当中







```python
def abc(**kwargs):
    for x,y in kwargs.items():
        print(x,">>",y)

abc(a=1,b=2)

结果如下
a >> 1
b >> 2
```



位置参数和关键字参数一起
```python
>>> def  aac(*iterable,**kwargs):
	print(type(iterable),type(kwargs))

>>> aac()
<class 'tuple'> <class 'dict'>
>>> aac(1,2,3,a=3,v=4)
<class 'tuple'> <class 'dict'>
```



看看以下成功或失败的原因
```python
>>> def test(username,passsword,*iterable,**kwargs):
	pass

>>> def test1(username,*args,**kwargs):
	pass

>>> def test2(username.**kwargs,*iterable):

SyntaxError: invalid syntax
>>>
```

## 总结
- 有可变位置参数和可变关键字参数的
- 可变位置参数在可变关键字参数
- 可变关键字参数在形参前面加**
- 可变位置参数和可变关键字参数都可以收集若干个实参，可变位置参数收集形成一个tuple，可变关键字参数收集形成一个dict
- 混合使用参数的时候，普通参数需要放到参数列表的后面，可变位置参数需要在可变关键字参数前面
