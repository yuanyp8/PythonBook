## 命令分发器
程序员可以轻松的注册一个函数到某一个命令，用户输入命令时，路由到注册的函数,
如果此命令没有对应的注册函数，执行默认的函数

### 分析
- 输入命令映射到函数对象，并执行这个函数，应该是cmd_tb[cmd]=fn,字典正好合适
- 如果输入一个cmd命令后，没有找到函数，就要调用缺省的函数执行，这正好是字典的缺省值参数
- cmd是字符串
- 接受用户的传入就可以使用input函数

### 基础框架
1. 定义一个装饰器，用来注册被定义的函数到字典
```python
from collections import defaultdict

def command_dispatcher():
    """
    定义一个装饰器，当你定义函数的时候，装饰器会把这个函数放入到字典中
    """
    command = defaultdict(list)

    def default_func():
        print("Unknown Command")

    def reg(name):
        def wrapper(func):
            command[name] = func
            return func
        return wrapper

    def dispatcher():
        while True:
            cmd = input(">>")
            if cmd.strip() in [[], '']:
                return default_func
            command.get(cmd, default_func)()

    return reg, dispatcher

reg, dispatcher = command_dispatcher()

@reg('foo1')
def foo1():
    print('foo1')
@reg('foo2')
def foo2():
    print('foo2')
dispatcher()
```



## 缓存器
实现一个cache装饰器，实现过期被清理的功能

### 思路
- 简化设计，函数的形参不包含可变位置参数，可变关键字参数和keyword-only传参
- 可以不包含缓存大小，也不用考虑满了之后换出的问题

### key算法的设计
- key必须是可hash，且k的缺省值必须考虑
- 可以利用inspect.parameter,是一个缺省参数的有序字典，会保存所有参数的信息
- 构建一个字典params_dict，按照位置顺序从args依次获取参数名和传入的实参，组成kv对，存入params_dict中
- kwargs所有值update到params_dict中去
- 如果使用看缺省参数，不会出现params_dict中，会出现在签名的parameters中，缺省值也在函数定义中


### 调用的方式

这是实现了所有的传参方式传入，并生成了字典
```python
from functools import wraps
import inspect
from collections import  defaultdict


def cache(fn):
    @wraps(fn)
    def wrapper(*args,**kwargs):
        sig = inspect.signature(fn)
        params = sig.parameters
        target = {}

        # target.update(zip(params.keys(),args)) # 按位传参
        # target.update(kwargs)                  # 关键字传参
        target.update(zip(params.keys(),args),**kwargs) # 合并关键字参数和位置参数
        for k, v in params.items():
            if k not in target.keys():
                target[k] = v.default  # 但是如果没有缺省值，那么v.default 就是inspect._empty

        #ret = fn(*args, **kwargs)
         ret = fn(**target)   
        return ret
    return wrapper
```

增加一个logger记录运行时间
```python

import datetime
import inspect
import time
from functools import wraps


def cache(fn):
    print("cache")
    local_cache = {}
    @wraps(fn)
    def wrapper(*args, **kwargs):
        sig = inspect.signature(fn)
        params = sig.parameters
        target = {}

        # target.update(zip(params.keys(),args))  # 按位传参
        # target.update(kwargs)                  # 关键字传参
        target.update(zip(params.keys(), args), **kwargs)  # 合并关键字参数和位置参数

        # for k, v in params.items():
        #    if k not in target.keys():
        #        target[k] = v.default   # 但是如果没有缺省值，那么v.default 就是inspect._empty
        target.update(((k, params[k].default) for k in (params.keys() - target.keys())))

        # ret = fn(*args, **kwargs)
        # ret = fn(**target)

        key = tuple(sorted(target.items()))
        if key not in local_cache.keys():
            local_cache[key] = fn(**target)

        return local_cache[key]
    return wrapper


def logger(fn):
    print("logger")
    @wraps(fn)
    def wrapper(*args, **kwargs):
        start_time = datetime.datetime.now()
        ret = fn(*args, **kwargs)
        delta = (datetime.datetime.now() - start_time).total_seconds()
        print("The function: {} cost {:.2f}s".format(fn.__name__, delta))
        return ret
    return wrapper

@logger
@cache
def add(x=4, y=5):
    time.sleep(2)
    return x+y


print(add(4, 5))
print(add(4, 5))
print(add())
print(add(y=5))
```
|     |     |     |
| --- | --- | --- |
|     |     |     |


什么时候清除，不能触发增加的时候再检查清除，因为会造成阻塞，后期考虑多线程
```python

```

```python

```
```python

```

```python

```


```python

```

```python

```

```python

```

```python

```

```python

```

```python

```
