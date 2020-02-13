# 匿名函数

## 匿名
- 匿名 -- 就是隐藏名字，即没有名称
- 匿名函数 -- 没有名字的函数

## Lambda表达式
Python中，使用Lambda表达式构建匿名函数
- 公式 = lambda 参数 : 函数表达式
- 参数列表不是必要元素，没有形参可以不写
- lambda表达式的":"后面不允许出现"="或者"return"
- lambda也只能接纳一行表达式，也称为单行函数
- 不需要使用return，表达式的值就是函数的返回值。
- lambda通常作为高阶函数的传参中

## 例子
- 返回值为None的函数
```Python
>>> print((lambda x:None)(5))
None
```

- 函数对象写入列表
```Python
>>> [lambda x:x**x][0](3)
27
```


- 没有参数的匿名函数
```Python
>>> [lambda x:x**x][0](3)
27
```


- sorted函数就是高阶函数
```Python
>>> lst = [1,2,"a","b"]
>>> sorted(lst,key=str)
[1, 2, 'a', 'b']
```

- sorted排序int
```Python
>>> lst
[1, 2, 'a', 'b']
>>> def fn(x):
	if isinstance(x,str):
		return ord(x)
	else:
		return x

>>> sorted(lst,key=fn)
[1, 2, 'a', 'b']
>>> sorted(lst,key=lambda x:ord(x) if isinstance(x,str) else x)
[1, 2, 'a', 'b']
```

- 加法匿名函数，带缺省值
```Python
>>> (lambda x,y=30:x+y)(2)
32
```

- keyword-only 传参
```Python
>>> (lambda x,*,y=10:x+y)(2,y=50)
52
```

- 可变参数
```Python
>>> (lambda *args:args)(10,20,30)
(10, 20, 30)

>>> (lambda *args:[x for x in args])(*range(10))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

>>> (lambda *args:[*args])(*range(10))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

- 生成器
```Python
>>> (lambda *args:(x for x in args))(*range(10))
<generator object <lambda>.<locals>.<genexpr> at 0x000001DB62EF9348>

>>> for  x in (lambda *args:(x for x in args))(*range(10)):
	print(x)

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

>>> (i for i in  (lambda *args:(x for x in args))(*range(10)))
<generator object <genexpr> at 0x000001DB62EF92C8>
```

- 高阶函数
```Python
>>> [i for i in (lambda *args:map(lambda x:x+1,args))(*range(5))]
[1, 2, 3, 4, 5]

a = defaultdict(lambda x=0:x+1)
print(a[0])

b = defaultdict(lambda :[])
```
