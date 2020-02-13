# 随机数、元组
## 随机数

### 从范围内给出一个随机数

```python
>>> import random
>>> random.randint(1,5)
2
```

###  从列表中随机的取一个元素

```python
>>> lst = [1,4,7,2,6,8,9,5,3]
>>> for i in range(5):
	print(random.choice(lst))

4
9
1
5
8
```

### 对列表随机洗牌

```python
>>> lst
[1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> random.shuffle(lst)
>>> lst
[9, 6, 1, 4, 5, 8, 2, 3, 7]
```

### 取样
从样本空间取n个**不同**的元素
```python
>>> lst
[9, 6, 1, 4, 5, 8, 2, 3, 7]
>>> random.sample(lst,3)
[5, 3, 2]
>>> random.sample(lst,5)
[6, 2, 5, 8, 4]
```

## 元组
- 一个有序的元素组成的集合
- 使用`()`表示
- 元组是不可变对象

>元组一旦创建，就不可更改

### 元组的定义

```python
>>> t1 = ()
>>> t2 = tuple()
>>> t3 = (1)*3  #注意，这不是元组
>>> t4 = (1,)
>>> t5 = (1,(2,3),'a',None)
```

### 元组只保存元素的索引
元组只保存门牌号码，房间内的东西是可以变动

```python
>>> tt = (1,[2,3])
>>> tt[1][0] = 101
>>> tt
(1, [101, 3])
```

```python
>>> a = ([1,2,3],)*3
>>> \

>>> a
([1, 2, 3], [1, 2, 3], [1, 2, 3])
>>> a[0][1] = 888
>>> a
([1, 888, 3], [1, 888, 3], [1, 888, 3])
```


## 命名元组namedtuple
nametuple(typename,field_names,verbose=False,rename=False)
- 命名元组，返回一个元组的子类，并定义了字段
- field_names可以是空白符或逗号分割的字段的字符串，可以是字段的列表

```python
from collections import namedtuple
Point = namedtuple('Point',['x','y'])
print(type(Point))
p1 = Point(3,4)
print(p1)
----
<class 'type'>
Point(x=3, y=4)
```
