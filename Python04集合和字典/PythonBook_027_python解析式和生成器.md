## datetime库简单使用
对日期、时间、时间戳的处理

### datetime类
#### 类方法
datetime.datetime是个类方法
类似于`int`、`str`等，都是一类方法的引用

```python
>>> type(datetime.datetime)
<class 'type'>
>>> type(int)
<class 'type'>

```

##### today()
利用类方法的时间对象  
返回本地时区当前时间的datetime对象

```python
>>> datetime.datetime.today()
datetime.datetime(2020, 1, 8, 13, 38, 46, 655917)

```

##### now(tz=None)
返回当前时区的datetime对象，时间到微秒，如果tz=None，返回和today()一样

```python
>>> import datetime     # 引入模块
>>> datetime.datetime.now()    
datetime.datetime(2020, 1, 8, 13, 34, 34, 879482)
```

##### utcnow()
没有时区的当前时间

```python
datetime.datetime(2020, 1, 8, 13, 39, 41, 756573)
>>> datetime.datetime.utcnow()
datetime.datetime(2020, 1, 8, 5, 39, 51, 640815)
```

##### fromtimestamp(timestamp,tz=None)
从一个时间戳返回一个datetime对象

先再浏览器用js得到一个时间戳


```python
new Date().getTime()
1578462570049
```
得到的结果是放大了1000倍的结果，去掉后三位，用timestamp转化

```python
>>> datetime.datetime.fromtimestamp(1578462570)
datetime.datetime(2020, 1, 8, 13, 49, 30)
```

> 类方法做的就是：没有对象，构造对象

#### datetime对象

##### timestamp()返回一个时间到微秒的时间戳

```python
>>> datetime.datetime.fromtimestamp(1578462570).timestamp()
1578462570.0
```

##### 时间差
```python
>>> d1 = datetime.datetime.now()
>>> d2 = datetime.datetime.now()
>>> d3 = d2.timestamp() -d1.timestamp()
>>> d1
datetime.datetime(2020, 1, 8, 15, 16, 4, 6129)
>>> d2
datetime.datetime(2020, 1, 8, 15, 16, 26, 835832)
>>> d3
22.829703092575073
```

##### 直接构造
直接给出年月日时分秒来得到一个时间对象
```python
>>> datetime.datetime(2017,12,1,1,2,3,4)
datetime.datetime(2017, 12, 1, 1, 2, 3, 4)
```


### 时间对象的使用方法


#### 解析年月日
year、month、day、weekday()

```python
>>> d = datetime.datetime.now()
>>> d
datetime.datetime(2020, 1, 9, 9, 57, 58, 64721)
>>> d.year,d.month,d.day
(2020, 1, 9)
>>> d.weekday() #这个是老外的时间
3
>>> d.isoweekday() # ISO标准化日期
4
```


#### date()

返回日期的date对象

```python
>>> d
datetime.datetime(2020, 1, 9, 9, 57, 58, 64721)
>>> d.date()
datetime.date(2020, 1, 9)
```


#### time()
返回时间time对象

```python
>>> d.time()
datetime.time(9, 57, 58, 64721)
```


#### replace()
修改并立即返回新的时间

```python
>>> d
datetime.datetime(2020, 1, 9, 9, 57, 58, 64721)
>>> d.replace(2222,2,2)
datetime.datetime(2222, 2, 2, 9, 57, 58, 64721)
>>> d
datetime.datetime(2020, 1, 9, 9, 57, 58, 64721)
```


#### iscalendar()
返回一个三元组（年，周数，周几）

```python
>>> d.isocalendar()
(2020, 2, 4)
```

### 日期格式化
#### 类方法strptime(date_string,format)，返回datetime对象  
`string-->>datetime`

```python
>>> datetime.datetime.strptime("2020, 1, 9, 9, 57, 58","%Y, %m, %d, %H, %M, %S")
datetime.datetime(2020, 1, 9, 9, 57, 58)
```


#### 对象方法strftime(format)，返回字符串
`>datetime-->>string`

```python
datetime.datetime(2020, 1, 9, 9, 57, 58)
>>> dd.strftime("%Y-%m-%d %H:%M:%S")
'2020-01-09 09:57:58'
```

#### 字符串format函数格式化


```python
>>> dd
datetime.datetime(2020, 1, 9, 9, 57, 58)
>>> a = "{:%Y-%M-%d :%H:%M:%S}".format(dd)
>>> a
'2020-57-09 :09:57:58'
```



#### **附录：python中时间日期格式化符号：**

| 符号 | 说明                                      |
| ---- | ----------------------------------------- |
| `%y` | 两位数的年份表示（00-99）                 |
| `%Y` | 四位数的年份表示（000-9999）              |
| `%m` | 月份（01-12）                             |
| `%d` | 月内中的一天（0-31）                      |
| `%H` | 24小时制小时数（0-23）                    |
| `%I` | 12小时制小时数（01-12）                   |
| `%M` | 分钟数（00=59）                           |
| `%S` | 秒（00-59）                               |
| `%a` | 本地简化星期名称                          |
| `%A` | 本地完整星期名称                          |
| `%b` | 本地简化的月份名称                        |
| `%B` | 本地完整的月份名称                        |
| `%c` | 本地相应的日期表示和时间表示              |
| `%j` | 年内的一天（001-366）                     |
| `%p` | 本地A.M.或P.M.的等价符                    |
| `%U` | 一年中的星期数（00-53）星期天为星期的开始 |
| `%w` | 星期（0-6），星期天为星期的开始           |
| `%W` | 一年中的星期数（00-53）星期一为星期的开始 |
| `%x` | 本地相应的日期表示                        |
| `%X` | 本地相应的时间表示                        |
| `%Z` | 当前时区的名称                            |
| `%%` | %号本身                                   |                                          





## 列表解析式

###  语法
- 列表解析式的语法：[返回值 for 元素 in 可迭代对象 if 条件]
- 使用中括号[]，内部是for循环
- if条件语句可选
- 返回一个新的列表

>列表解析式是一种语法糖，编译器会优化，不会因为简写而影响效率，反而因优化提高了效率。减少程序员工作量，减少出错。简化了代码，但可读性增强。

### 例子
1. 比如要生成一个列表，元素0~9，对每一个元素自增1后求平方返回新列表，下面看不用列表解析式和用列表解析式的代码。

```python
>>> lst = []
>>> for i in range(10):
	i = (i+1)**2
	lst.append(i)

>>> lst
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

```python
>>> lst = [(i+1)**2 for i in range(10)]
>>> lst
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

2. 打印20以内的偶数


```python
>>> lst = []
>>> for i in range(20):
	if i%2 == 0:
		lst.append(i)
>>> print(lst)
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
>>>
```


```python
>>> lst = [i for i in range(20) if i%2==0]
>>> print(lst)
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```

### 思考
有这样的赋值语句newlist = [print(i) for i in range(10)]，请问newlist的元素打印出来是什么？

```python
newlist = [print(i) for i in range(10)]
print(newlist)

结果为：
0
1
2
3
4
5
6
7
8
9
[None, None, None, None, None, None, None, None, None, None]
```

### 应该注意if条件后面不能在跟elif
比如获取20以内同时被2、3整除，下面的代码是不行的。

```python
>>> lst = [i for i in range(20) if i%2==0 elif 1%3==0]
SyntaxError: invalid syntax
```
and可以

```python
>>> lst = [i for i in range(20) if i%2==0 and i%3==0]
>>> lst
[0, 6, 12, 18]
```


### 列表解析式进阶

#### 第一种
[expr for item in iterable if cond1 if cond2]

这等价于：

```python
ret = []
for item in iterable:
  if cond1:
      if cond2:
        ret.append(expr)
```

获取20以内同时被2、3整除

```python
>>> lst = [i for i in range(20) if i%2==0 if i%3==0]
>>> lst
[0, 6, 12, 18]
```

#### 第二种

[expr for i in iterable1 for j in iterable2 ]

等价于：

```python
ret = []
for i in iterable1:
　　for j in iterable2:
　　　　ret.append(expr)
```
相当于嵌套for循环。

1. 列表里的元素为字典

```python
>>> lst = [{i:j} for i in range(5) for j in 'abc']
>>> lst
[{0: 'a'}, {0: 'b'}, {0: 'c'}, {1: 'a'}, {1: 'b'}, {1: 'c'}, {2: 'a'}, {2: 'b'}, {2: 'c'}, {3: 'a'}, {3: 'b'}, {3: 'c'}, {4: 'a'}, {4: 'b'}, {4: 'c'}]
```

2. 列表的元素为集合


```python
>>> lst = [{i,j} for i in range(5) for j in 'abc']
>>> lst
[{0, 'a'}, {0, 'b'}, {0, 'c'}, {1, 'a'}, {1, 'b'}, {1, 'c'}, {2, 'a'}, {2, 'b'}, {'c', 2}, {3, 'a'}, {'b', 3}, {'c', 3}, {4, 'a'}, {'b', 4}, {'c', 4}]
>>> lst = [{1,0} for i in range(5) for j in 'abc']
>>> lst #不存在set去重的考虑
[{0, 1}, {0, 1}, {0, 1}, {0, 1}, {0, 1}, {0, 1}, {0, 1}, {0, 1}, {0, 1}, {0, 1}, {0, 1}, {0, 1}, {0, 1}, {0, 1}, {0, 1}]
>>> id(lst[0])
3024216889608
>>> id(lst[1])
3024216887592
```


3. 复杂结构

```python
>>> lst = [(i,j) for i in range(6) for j in range(20,25) if i >=3 if i**2 >j]
>>> lst
[(5, 20), (5, 21), (5, 22), (5, 23), (5, 24)]
```

### 练习
#### 第一题
有一个列表lst = [1,4,9,16,2,5,10,15]，生成一个新列表，要求新列表元素是lst相邻2项的和

```python
lst = [1,4,9,16,2,5,10,15]
result = []
for i in range(len(lst)-1):
    result.append(lst[i]+lst[i+1])
print(result)

[5, 13, 25, 18, 7, 15, 25]

#下面用列表解析式
lst = [1,4,9,16,2,5,10,15]
result = [lst[i]+lst[i+1] for i in range(len(lst)-1)]
print(result)

[5, 13, 25, 18, 7, 15, 25]
```
#### 第二题
打印九九乘法表

先看下普通写法
```python
for i in range(1,10):
    for j in range(1,i+1):
        print("{}*{}={:>2}".format(j,i,j*i),end= '\n' if j == i else ' ')
```
用列表解析式
```python
lst = [print("{}*{}={:>2}".format(j,i,j*i),end= '\n' if j == i else ' ') for i in range(10) for j in range(2,i+1)]
```


## 生成器表达式Generator expression

### 语法
- 生成器的语法为：(返回值 for 元素 in 可迭代对象 if 条件)
- 它就是将列表解析式的中括号换成小括号就行了
- 它返回的是一个可迭代的生成器对象

```python
>>> (x for i in range(5))
<generator object <genexpr> at 0x000002C0216572C8>
```
### 和列表解析式的区别
- 生成器表达式是按需计算(或称惰性求值、延迟计算)，需要的时候才计算
- 列表解析式是立即返回值

### 生成器
- 生成器是Python中一个特殊的程序，用于控制循环的迭代行为。相对于一般函数用return来一次性返回所有值，生成器使用yield关键字，一次只返回一个值。
- 是一个可迭代对象
- 是一个迭代器

>这样的设计有很大的好处：在数据处理时，如果函数return出来的是一个非常大的数组，那么会非常占用内存，有时会报MemoryError的错误，而使用yield后一次仅仅返回一个元素值，可以优化内存占用的情况


### 例子

#### 练习一
利用生成器表达式生成生成器
```python
>>> lst = [1,4,9,16,2,5,10,15]
>>> result = (lst[i]+lst[i+1] for i in range(len(lst)-1))  #生成器表达式为我们生成一个生成器对象出来
>>> type(result)
<class 'generator'>
```
利用生成器

```python
>>> a = (i*2 for i in range(5))
>>> type(a)
<class 'generator'>
>>> next(a)
0
>>> next(a)
2
>>> for i in a:
	print(i)

4
6
8

>>> next(a)
Traceback (most recent call last):
  File "<pyshell#21>", line 1, in <module> #走到尽头
    next(a)
StopIteration

>>> for i in a:
	print(i)
				#输出为空
>>>
```

#### 练习二


```python
>>> it = ( print("{}".format(i+1)) for i in range(2))
>>> first = next(it)
1
>>> second = next(it)
2
>>> val = first + second
Traceback (most recent call last):
  File "<pyshell#28>", line 1, in <module>
    val = first + second
TypeError: unsupported operand type(s) for +: 'NoneType' and 'NoneType'
>>> first
>>> second
>>> None+None
Traceback (most recent call last):
  File "<pyshell#31>", line 1, in <module>
    None+None
TypeError: unsupported operand type(s) for +: 'NoneType' and 'NoneType'
```


### 列表解析式和生成器表达式的区别

#### 计算方法
生成器表达式延迟计算，列表解析式立即计算

#### 内存占用
- 单从返回值本身来说，生成器表达式节省内存，列表解析式返回新的列表
- 生成器没有数据，内存占用极少，它是使用的时候一个个返回数据，如果将这些返回的数据合起来占用的内存和列表解析式也差不多，但是它不需要占用这么多内存
- 列表解析式构造新的列表需要立即占用内存，不管你是否立即使用这么多数据

#### 计算速度
- 单看计算时间看，生成器表达式耗时非常短，列表解析式时间长
- 但是生成器本身并没有返回任何值，只返回了一个生成器对象
- 列表解析式构造并返回了一个新的列表，所有看起来耗时了



### 应用


## 集合解析式
### 语法
- {返回值 for 元素 in 可迭代对象 if 条件}
- 列表解析式的中括号换成大括号就行
- 立即返回一个集合


### 用法
- {(x,x+1) for x in range(10)}
- {[x] for x in range(10)}  #错误的，集合里的元素为可哈希，列表不可哈希

```python
>>> {(x,x+1) for x in range(5)}
{(0, 1), (1, 2), (4, 5), (2, 3), (3, 4)}
```

## 字典解析式

### 语法
- {x:(x+1) for x in range(5)}

```python
{0: 1, 1: 2, 2: 3, 3: 4, 4: 5}
```

- {x:[x,x+1] for x in range(5)}

```python
{0: [0, 1], 1: [1, 2], 2: [2, 3], 3: [3, 4], 4: [4, 5]}
```

- {(x,):[x,x+1] for x in range(5)}

```python
{(0,): [0, 1], (1,): [1, 2], (2,): [2, 3], (3,): [3, 4], (4,): [4, 5]}
```

- {chr(0x41+x):x**2 for i in range(10)}

```python
{'C': 4}
```

- {str(x):y for x in range(5) for y in range(4)}

```python
{'0': 3, '1': 3, '2': 3, '3': 3, '4': 3}
```
