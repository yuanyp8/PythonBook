# 字符串

## 字符串的定义
- 一个个字符组成的有序的序列，是字符的集合
- 使用单引号、双引号、三引号引住的字符序列
- 字符串是不可变对象
- Python3以后，字符串就是Unicode类型

### f前缀
```python
>>> x = 1
>>> y =2
>>> s1 = "{x} -> {y}"
>>> s2 = f"{x} -> {y}"
>>> s1
'{x} -> {y}'
>>> s2
'1 -> 2'
```

### 索引

```python
>>> s = 'abcdefg'
>>> s[0]
'a'
>>> s[1]
'b'
```
### 可迭代对象的使用

```python
>>> "".join("abcde")
'abcde'
>>> ":".join("abcde")
'a:b:c:d:e'


>>> a = list('abcde')
>>> a
['a', 'b', 'c', 'd', 'e']
>>> ":".join(a)
'a:b:c:d:e'

>>> ":".join(['abcde'])
'abcde'
```

## 字符串的操作


### 字符串分割
以下操作都是立刻返回，形成一个新的字符串，原字符串不变动

#### split（）
通过指定分隔符对字符串进行切片，默认使用空白字符分割，立即返回一个列表
```python
>>> a = 'abcde'
>>> a.split()
['abcde']
>>> a
'abcde'

#使用a为分隔符
>>> a
'abcde'
>>> a.split('a')
['', 'bcde']


#切割次数
>>> a= 'cabcabcabc'
>>> a.split('a',maxsplit=2)
['c', 'bc', 'bcabc']

#从右向左切
>>> b = 'abcabcabcabc'
>>> b.rsplit('a',maxsplit=1)
['abcabcabc', 'bc']

#splitlines
>>> a = 'abc \t\n def\n\r  \nfff'
>>> a.splitlines()
['abc \t', ' def', '', '  ', 'fff']
```


#### partition()
一切三块，保留分隔符
```python
>>> a = 'abcdeabcde'
>>> a.partition('b')
('a', 'b', 'cdeabcde')
```

### 字符串大小写
Python是大小写敏感的

#### upper()
把所有字符中的小写字母转换成大写字母

```python
>>> 'AbCd'.upper()
'ABCD'
```

#### lower()
把所有字符中的大写字母转换成小写字母

```python
>>> 'ABcd'.lower()
'abcd'
```

#### swapcase()
大小写对调


```python
>>> 'abCD'.swapcase()
'ABcd'
```


### 字符串排版
以下操作都是立刻返回，形成一个新的字符串，原字符串不变动
#### title()
标题的每个单词都大写

```python
>>> 'pleaseaskmewhy'.title()
'Pleaseaskmewhy'
>>> 'please ask me why'.title()
'Please Ask Me Why'
```

#### capitalize()
把第一个字母转化为大写字母，其余小写

```python
>>> 'pleaseaskmewhy'.capitalize()
'Pleaseaskmewhy'
>>> 'please ask me why'.capitalize()
'Please ask me why'
```



#### center(width[,fillchar])
- width打印宽度
- fillchar填充的字符

```python
>>> 'abc'.center(10,'#')
'###abc####
```
#### zfill(width)
没有填充字符，只有宽度
```python
>>> 'abc'.zfill(10)
'0000000abc'
>>> 'abcdefgghh'.zfill(10)
'abcdefgghh'
```

#### ljust(width[,fillchar])
左对齐

```python
>>> 'abc'.ljust(10,'#')
'abc#######'
```

#### rjust(width[,fillchar])
右对齐

```python
>>> 'abc'.rjust(10,'$')
'$$$$$$$abc'
```


### 字符串修改
#### replace(old,new[,count])
替换

```python
>>> 'abcabcabc'.replace('a','A')
'AbcAbcAbc'
>>> 'abcabcabc'.replace('a','A',2)
'AbcAbcabc'
```

#### strip()
将一个字符串的两边的空白字符拿掉
```python
>>> a = '  i am very very very sorry  '
>>> a.strip()
'i am very very very sorry'


>>> a = '    \t I am very very very ok\t'
>>> a.strip(' \t')
'I am very very very ok'
```

### 字符串查找
find()、index()、count()的时间复杂度都是`O(n)`
#### find()
查找子字符串，若找到返回从0开始的下标值，若找不到返回-1

```python
>>> 'hello'.find('h')
0
>>> 'hello'.find('a')
-1
```
#### rfind()
与find()类似，只不过从右向左查找，下标依然是从0开始

```python
>>> 'hello'.rfind('l')
3
```

#### index()
python 的index方法是在字符串里查找子串第一次出现的位置，类似字符串的find方法，不过比find方法更好的是，如果查找不到子串，会抛出异常，而不是返回-1

```python
>>> 'hello'.index('e')
1
>>> 'hello'.index('a')
Traceback (most recent call last):
  File "<pyshell#351>", line 1, in <module>
    'hello'.index('a')
ValueError: substring not found
```
#### rindex()
与index()类似，只不过从右向左查找，下标依然是从0开始

```python
>>> 'hello'.rindex('l')
3
```

#### count()
查找字符串出现的次数

```Python
>>> a = 'hello'*5
>>> a
'hellohellohellohellohello'
>>> a.count('hello')
5
```

#### len()
返回字符串的长度

```python
>>> a
'hellohellohellohellohello'
>>> len(a)
25
```

#### startswith()
用于检查字符串是否是以指定子字符串开头，如果是则返回 True，否则返回 False。如果参数 beg 和 end 指定值，则在指定范围内检查。
`str.startswith(str, beg=0,end=len(string))`

```python
>>> 'abc'.startswith('a')
True


>>> 'abcdef'.startswith('b',1,2)
True
```

#### endswith()
用于检查字符串是否是以指定子字符串结尾，如果是则返回 True，否则返回 False。如果参数 beg 和 end 指定值，则在指定范围内检查。

```Python
>>> 'abcdef'.endswith('f')
True
>>> 'abcdef'.endswith('cd',2,4)
True
```

> [Warning!]  
startswith 和 endswith 起始位置都是前包后不包


### 字符串判断is系列

#### string.isalnum()
如果 string 至少有一个字符并且所有字符都是字母或数字则返回 True,否则返回 False

```Python
>>> ''.isalnum()
False
>>> '3544'.isalnum()
True
```



#### string.isalpha()
如果 string 至少有一个字符并且所有字符都是字母则返回 True,否则返回 False

```Python
>>> 'abc'.isalpha()
True
>>> 'abc3'.isalpha()
False
>>> ''.isalpha()
False
```

#### string.isdecimal()
如果 string 只包含十进制数字则返回 True 否则返回 False.

```Python
>>> '3424'.isdecimal()
True
>>> '0b1010'.isdecimal()
False
```

#### string.isdigit()
如果 string 只包含数字则返回 True 否则返回 False.

```Python
>>> '0b1010'.isdigit()
False
>>> '3424'.isdigit()
True
```

#### string.islower()
如果 string 中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是小写，则返回 True，否则返回 False

```Python
>>> 'abc'.islower()
True
>>> 'Abc'.islower()
False
```



#### string.isspace()
如果 string 中只包含空格，则返回 True，否则返回 False.

```Python
>>> ''.isspace()
False
>>> ' '.isspace()
True
>>> '\t'.isspace()
True
```



#### string.isidentifier()
是不是字母和下划线开头，其他都是字母、下划线、数字

```Python
>>> 'for'.isidentifier()
True
>>> '2_f'.isidentifier()
False
```

#### string.isupper()  	
如果 string 中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是大写，则返回 True，否则返回 False

```Python
>>> 'ANC'.isupper()
True
```

## 字符串格式化
字符串的格式化是一种拼接字符串输出样式的手段，更灵活方便

### 其他方法
- `join()`只能使用分隔符，且要求被拼接的是可迭代对象且其元素是字符串
- `+`拼接字符串还算方便，但是非字符串需要先转化为字符串才能操作


### 在2.5版本之前，只能使用print style风格的print输出
- print-style formatting ，来自C语言的printf函数
- 格式要求：
    1. 占位符：使用%和格式字符串组成，例如%s、%d等
    2. s调用str()，r调用repr()。所有对象都可以被这两个转换
    3. 占位符还可以插入修饰字符，例如`%03d`表示打印三个位置，不够前面补0
    4. format % values，格式字符串和被格式的值之间使用分隔
    5. values只能是一个对象，或者是一个与格式字符串占位符数目相等的元组，或一个字典


```python
>>> "I am %s" % 'superman'
'I am superman'

>>> "1 %s %03d" %('is not',2)
'1 is not 002'
```

### 主流的方法是format()
`"{} {xxx}".format(*args,**kwargs) -> str`
- args是可变位置参数，是一个元组
- kwargs是可变关键字参数，是一个字典
- 花括号表示占位符
- {}表示按照顺序匹配位置参数，{n}表示取位置下参数索引为n的值
- {xxx}表示在关键字参数中搜索名称一致的
- {{}}表示打印花括号

#### 简单举例
```Python
>>> "I am {}".format('Superman')
'I am Superman'
```

#### 索引
```Python
>>> "{0} am {1}, and U are {2}".format('I','Superman','Jocker')
'I am Superman, and U are Jocker'
```

#### 打印时间
```python
>>> import datetime
>>> d = datetime.datetime.now()
>>> d
datetime.datetime(2019, 12, 25, 12, 5, 50, 227286)
>>> "{:%Y}".format(d)
'2019'
>>> "{:%Y-%m-%d %H:%M:%S}".format(d)
'2019-12-25 12:05:50'
```

#### kwargs

```python
>>> "{server}:{port}".format(server="127.0.0.1",port="8080")
'127.0.0.1:8080'
```

#### 排版

```python
>>> "{}*{}={}".format(2,3,6)
'2*3=6'
>>> "{}*{}={:>2}".format(2,8,16)
'2*8=16'
>>> "{}*{}={:>2}".format(2,3,6)
'2*3= 6'

#填充
>>> "{}*{}={:#^4}".format(2,3,6)
'2*3=#6##'
>>> "{}*{}={:#^4}".format(2,3,116)
'2*3=116#'
```

#### 解构

```Python
>>> ip = [192,168,0,1]
>>> "{}.{}.{}.{}".format(*ip)
'192.168.0.1
```


#### `{{}}`
```Python
>>> "{{{} is not ok}}".format('ok')
'{ok is not ok}'
```

#### 数字
```Python
>>> "{}".format(2**0.5)
'1.4142135623730951'
>>> "{:f}".format(2**0.5)  #f为浮点数格式，默认6位
'1.414214'
>>> "{:3.2f}".format(200**0.5) #3个占位符，保留小数点后2位
'14.14'
>>> "{:30.2f}".format(200**0.5) #30个占位符，保留小数点后2位
'                         14.14'
>>> "{:<30.2f}".format(200**0.5) #30个占位符，保留小数点后2位，左对齐
'14.14                         '
```
