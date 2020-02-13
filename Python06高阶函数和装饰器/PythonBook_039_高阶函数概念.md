# 高阶函数
- 在Python中，函数是一等公民(First-Class Object)
- 函数也是对象，是可调用对象
- 函数可以作为普通变量，也可以作为函数的参数，返回值

## 高阶函数定义
### 数学概念
y=f(g(x))

### 计算机体系中的定义
在数学和计算机体系中，高阶函数应当至少满足条件之一:
    - 接受一个或多个函数作为参数
    - 输出一个函数

### 看看是不是高阶函数
```Python
def counter(base):
    def inc(count=1,base=base):
        base += count
        return base
    return inc
```
### 接着看下
```Python
def counter(base):
    def inc(count=1,base=base):
        #nonlocal base
        base += count
        return base
    return inc
c = counter(10)
print(counter(10))
print(counter(10))
a = counter(10)
b = counter(10)
print(a,b,a == b)

结果如下
<function counter.<locals>.inc at 0x000001D92EFB0DC8>
<function counter.<locals>.inc at 0x000001D92EFB0DC8>
<function counter.<locals>.inc at 0x000001D92EFB0DC8> <function counter.<locals>.inc at 0x000001D92EFB0D38> False
# 因为第一个counter（10）利用完毕就释放了，地址复用
# 但是第二个分别被a,b记住了，并没有释放，所有内存地址不一样
```

### 变形
```Python
inc = 100
def inc():
    return 1
def fn():
    return inc
c1 = fn()
c2 = fn()
print(c1==c2,c1 is c2)

结果如下
True True
```
>-  因为两次fn()都是调用inc对象，inc对象是全局的，肯定是同一个函数对象
- 而上面的inc对象是内部函数生成的，所有每一次调用fn()都是重新生成的inc对象，这两个地址是不一样的


### 继续看


注意 == 如果无法比较内容，就用is来比较地址
```Python
print([1,2] == [1,2],[1,2] is [1,2])

结果如下
True False
```

## 练习写一个sort函数

### 实现排序的功能
可以利用简单插入排序，来实现这个功能，返回一个列表
```Python
lst = [2,5,4,1]
def sort(obj):
    new_list = []
    for i in obj:
        for j,num in enumerate(new_list):
            if i > num:
                new_list.insert(j,i)
                break
        else:
            new_list.append(i)
    return new_list
print(sort(lst))
```



上面是一个降序排序，我们加入一个参数来控制是否reverse
```Python
lst = [2,5,4,1]
def sort(obj,reverse=False):
    new_list = []
    for i in obj:
        for j,num in enumerate(new_list):
            ord = i > num if not reverse else i < num
            if ord:
                new_list.insert(j,i)
                break
        else:
            new_list.append(i)
    return new_list
print(sort(lst,reverse=True))
```

上面加入了反转控制，现在我们加入key
```Python
lst = [2,5,4,1,'1']
def sort(obj,reverse=False,*,key=None):
    new_list = []
    for i in obj:
        ci = key(i) if key else i
        for j,num in enumerate(new_list):
            cnum = key(num) if key else num
            ord = ci > cnum if not reverse else ci < cnum
            if ord:
                new_list.insert(j,i)
                break
        else:
            new_list.append(i)
    return new_list
print(sort(lst,reverse=True,key=int))
```

引入lambda
```Python
lst = [2,5,4,1,'1']
def sort(obj,reverse=False,*,key=None):
    new_list = []
    for i in obj:
        ci = key(i) if key else i
        for j,num in enumerate(new_list):
            cnum = key(num) if key else num
            ord = ci > cnum if not reverse else ci < cnum
            if ord:
                new_list.insert(j,i)
                break
        else:
            new_list.append(i)
    return new_list
print(sort(lst,reverse=True,key=lambda x:6-int(x)))
```


## map()
map()就是通过自定义的方法得到映射后的数据,输出的惰性的迭代器  
类似于`x => xx`

```Python
x = map(lambda x:x*2,list(range(5)))
print(next(x))
print(next(x))
print(next(x))
```
### 利用map函数构造字典

- 字典解析式
```Python
>>> dct = {x:(x,x+1) for x in map(lambda i:i*2,range(10))}
>>> dct
{0: (0, 1), 2: (2, 3), 4: (4, 5), 6: (6, 7), 8: (8, 9), 10: (10, 11), 12: (12, 13), 14: (14, 15), 16: (16, 17), 18: (18, 19)}
```

- dict()
```Python
>>> d = dict(map(lambda x:(x,(x,x+1)),range(5)))
>>> d
{0: (0, 1), 1: (1, 2), 2: (2, 3), 3: (3, 4), 4: (4, 5)}
```

- zip()
```Python
x = dict(zip(range(5),map(lambda x:x+1,range(5))))
print(x)
```

### map()双参数

```Python
a = list((map(lambda x,y:(x,y),range(5),range(1,6))))
print(a)
```

### filter
类似于filter，前面写函数，用来过滤，后面写被执行对象

```Python
a = list(filter(None,range(10))) # 比较值的bool值
print(a)

b = list(filter(lambda x:None,range(10)))
print(b)

c = list(filter(lambda x:False,range(10)))
print(c)

d = list(filter(lambda x:x%3==0,range(15)))
print(d)

[1, 2, 3, 4, 5, 6, 7, 8, 9]
[]
[]
[0, 3, 6, 9, 12]
```

## 柯里化函数
`z = f(x,y) => z = f(x)(y)`

- 起始
```Python
def add(x,y):
    return x+y
a = add(4,5)
print(a)
```
- 变形
```Python
def fn1(x):
    def fn2(y):
        return x+y
    return fn2
print(fn1(1)(2))

def fn2(x):
    def fn3(y):
        def fn4(z):
            return x+y+z
        return fn4
    return fn3
print(fn2(2)(3)(4))

def fn(x,y):
    def fn1(z):
        return x+y+z
    return fn1
print(fn(1,2)(3))

def fnn(x):
    def fnnn(y,z):
        return x+y+z
    return fnnn

print(fnn(2)(3,4))

结果如下
3
9
6
9
```
