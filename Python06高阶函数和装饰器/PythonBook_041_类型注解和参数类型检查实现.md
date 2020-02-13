
# 类型注解


```python
def add(x,y):
    return x+y

>>> add(1,2)
3
>>> add([1],[2])
[1, 2]
>>> add("1","2")
'12'
>>> add((),(5,))
(5,)
>>>
```
- python是动态的强类型的语言，而静态语言是提前检查，但是python是在运行之后才能检查是否正确
- 而输入的信息是不可控的，这也是经常出bug的地方
- 所以python引入了类型注解(python3.5以后支持)
- 既然是注解，就不是强制的类型约束
- 所以仅仅是注释性的解释，可以见下面的代码
```python
>>> def add(x:int,y:int) ->int :
	return x+y

>>> add(4,5)
9
>>> add('2','3')
'23'
>>> r:list = add('2','3')
```

```python
函数注解Function Annotations
函数注解：
Python3.5版本引入（现在3.5版本应用比较多，注意版本差别）
对函数的参数进行类型注解
对函数的返回值进行类型注解
只对函数参数做一个辅助的说明，并不对函数参数进行类型检查
提供给第三方工具，做代码分析，发现隐藏的bug
函数注解的信息，保存在_annotations_属性中

变量注解
Python3.6引入。注意它也只是一种对变量的说明，非强制
```

## 如何解决这种动态语言定义的弊端
- 增加文档Documentation String
    - 当然，这只是一个惯例，不是强制标准，不能要求程序员一定为函数提供说明文档
    - 函数定义更新了，文档未必更新




```python
def add(x:int,y:int) -> int:
    """
       Give two nums(int),return a new num(int)
       :param x:int
       :param y:int
       :return: int
    """
    return x+y

def ad(x,y):
    return x+y

print(help(ad))
print(help(add))

结果如下
Help on function ad in module __main__:

ad(x, y)

None
Help on function add in module __main__:

add(x: int, y: int) -> int
    Give two nums(int),return a new num(int)
    :param x:int
    :param y:int
    :return: int

None
```

### annotation
```python
def add(x:int, y:int，z="sss") -> int:
    """
    :param x:int
    :param y:int
    :return: int
    """
    return x+y
print(add.__name__,add.__doc__,add.__annotations__,sep="\n~~~~~~~~~~\n")

结果如下
add
~~~~~~~~~~

    :param x:int
    :param y:int
    :return: int

~~~~~~~~~~
{'x': <class 'int'>, 'y': <class 'int'>, 'return': <class 'int'>}
```
>annotations是依据参数类型注解返回对应的解释，并不会返回缺省值的类型






## 参数类型检查
注意：类型检查是在调用时产生的

```python
def add(x:int, y:int) -> int:
    """
    :param x:int
    :param y:int
    :return: int
    """
    if not (isinstance(x,int) and isinstance(y,int)):
        return "ERROR"
    return x+y
```

这样太罗嗦，定制化程度高，需要一个通用的

但是annotations不合适，需要inspect

### inspect
signature(callable)函数，可以获取签名（函数签名包含了一个函数的信息，包括：函数名、参数类型、函数所在的类和名称空间及其他信息）
```python
def add(x:int, y:int) -> int:
    """
    :param x:int
    :param y:int
    :return: int
    """
    if not (isinstance(x,int) and isinstance(y,int)):
        return "ERROR"
    return x+y

import inspect
sig = inspect.signature(add)
print(sig.parameters)
print(sig.return_annotation)

结果如下
OrderedDict([('x', <Parameter "x: int">), ('y', <Parameter "y: int">)])
<class 'int'>
```
>- 可以看到得到的结果是一个有序字典,因为普通的annotations是一个无序的字典
- 当然，如果没有提前写参数注解，返回值是<class 'inspect empty'>
- empty 特殊的类，用来标记default属性或者注释annotation属性的空值

#### inspect.Parameter

- name : str(返回的就是这个形参的名字)
    The name of the parameter as a string.
- default : object(返回的就是这个形参的缺省值，类似__default__)
    The default value for the parameter if specified.  If the
    parameter has no default value, this attribute is set to
    `Parameter.empty`.
- annotation(返回的就是形参的类型)
    The annotation for the parameter if specified.  If the
    parameter has no annotation, this attribute is set to
    `Parameter.empty`.
- kind : str(返回的就是这个形参的传参方式)
    Describes how argument values are bound to the parameter.
    Possible values: `Parameter.POSITIONAL_ONLY`,
    `Parameter.POSITIONAL_OR_KEYWORD`, `Parameter.VAR_POSITIONAL`,
    `Parameter.KEYWORD_ONLY`, `Parameter.VAR_KEYWORD`.

```python
inspect.signature(fn).parameters._kind
    POSITIONAL_ONLY         = _POSITIONAL_ONLY
    POSITIONAL_OR_KEYWORD   = _POSITIONAL_OR_KEYWORD
    VAR_POSITIONAL          = _VAR_POSITIONAL
    KEYWORD_ONLY            = _KEYWORD_ONLY
    VAR_KEYWORD             = _VAR_KEYWORD
inspect.signature().parameters._name
```

### 代码
```python
def check(fn):
    @functools.wraps(fn)
    def wrapper(*args, **kwargs):
        msg = "The given item is wrong!"
        sig = inspect.signature(fn)
        params = sig.parameters
        for x,(y,z) in zip(args,params.items()):
            if not isinstance(x,params[y].annotation):
                raise TypeError(msg)
        for k,v in kwargs.items():
            if not isinstance(v,params[k].annotation):
                raise TypeError(msg)
        ret = fn(*args, **kwargs)
        return ret
    return wrapper

@check
def add(x:int,y:int) -> int:
    return x+y
add(4,y='9')

结果如下
Traceback (most recent call last):
  File "D:/Gitee/python/test/matrix.py", line 679, in <module>
    add(4,y='9')
  File "D:/Gitee/python/test/matrix.py", line 671, in wrapper
    raise TypeError(msg)
TypeError: The given item is wrong!
```
#### 问题
但是这有个弊病，如果我没指定x：int，一旦我给x传入"str",那么报错就是str!=inspect.empyt,
 显然这个不符合逻辑，需要优化

#### 优化
```python
# inspect
import inspect,functools
from inspect import Parameter

def check(fn):
    @functools.wraps(fn)
    def wrapper(*args, **kwargs):
        msg = "The given item is wrong!,except {},but receive {}"
        sig = inspect.signature(fn)
        params = sig.parameters
        for x,(y,z) in zip(args,params.items()):
            if not isinstance(x,z.annotation) and z.annotation != inspect._empty:
                raise TypeError(msg.format(z.annotation,type(x)))
        for k,v in kwargs.items():
            if not isinstance(v,params[k].annotation) and params[k].annotation != inspect._empty:
                raise TypeError(msg.format(params[k].annotation,type(v)))
        ret = fn(*args, **kwargs)
        return ret
    return wrapper

@check
def add(x:int,y:int) -> int:
    return x+y
add("3",5)

结果如下
Traceback (most recent call last):
  File "D:/Gitee/python/test/matrix.py", line 677, in <module>
    add("3",5)
  File "D:/Gitee/python/test/matrix.py", line 666, in wrapper
    raise TypeError(msg.format(z.annotation,type(x)))
TypeError: The given item is wrong!,except <class 'int'>,but receive <class 'str'>
```
