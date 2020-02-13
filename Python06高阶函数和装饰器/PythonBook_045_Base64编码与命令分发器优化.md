## 什么是Base64编码算法
可以将任意的字节数组数据，通过算法，生成只有（大小写英文、数字、+、/）（一共64个字符）内容表示的字符串数据。
即将任意的内容转换为可见的字符串形式

## Base64算法的由来
以前发送邮件只支持可见字符的传送。由此，需要有一个方法将不可见的字符转换为可见的字符，便产生了Base64编码算法

## Base64算法的特点
- 将数据按照 3个字节一组的形式进行处理，每三个字节在编码之后被转换为4个字节。
即：如果一个数据有6个字节，可编码后将包含6/3*4=8个字节
- 当数据的长度无法满足3的倍数的情况下，最后的数据需要进行填充操作，即补“=” ，这里“=”是填充字符，不要理解为第65个字符

## Base64编码表
![](https://images2015.cnblogs.com/blog/493196/201510/493196-20151016194911194-515971600.png)


## 举例
```python
假设有三个字符abc
a   b   c # 字符模式  
0x616263  # 字节模式，16进制，且为大端模式
01100001 01100010 01100011 # 二进制表示
011000 010110 001001 100011 # 三分四
00011000 00010110 00001001 00100011 # 每一个前面补两位0
24       22       9        35  # 转化为16进制，就是Base64编码表的索引
Y        W        J        j   # 对应base64编码表找对应的值
```

验证一下
```python
>>> import base64
>>> base64.b64encode(b'abc')
b'YWJj'
```


## 做一个base64函数

### 写一个框架
```python
def b64encode(src:str):
    if isinstance(src, str):
        _src = src.encode()
    else:
        return None
```

### 分段
将所有输入的字符串按照格式整理分段
```python
def b64encode(src:str):
    if isinstance(src, str):
        _src = src.encode()
    else:
        return None
    for offset in range(0, len(_src), 3):
        triple = _src[offset:offset+3]

        r = 3 - len(triple)
        if r:
            triple += b'\x00' * r
        print(triple)

b64encode('abcdefg')
```


### 思考
```python
>>> 0b111111
63
>>> 0b111111 >>2
15

还有位与预算
0b11111111 & 0b00001111
= 0b00001111
```

### int.from_bytes(str)

```python
alphabet = b'ABCDEFGHIGKLMNOPQRSTUVWXYZabcdefghigklmnopqrstuvwxyz0123456789+/'

def b64encode(src: str):
    ret = bytearray()
    if isinstance(src, str):
        _src = src.encode()
    else:
        return None
    for offset in range(0, len(_src), 3):
        triple = _src[offset:offset+3]

        r = 3 - len(triple)
        if r:
            triple += b'\x00' * r
        x = int.from_bytes(triple, 'big')
        for i in range(18, -1, -6):
            index = x >> i & 0x3F
            ret.append(alphabet[index])
    print(ret)
    return ret

b64encode('abcdefg')

结果如下
bytearray(b'YWGgZGVmZwAA')
```

补0的需要替换一下
```python

alphabet = b'ABCDEFGHIGKLMNOPQRSTUVWXYZabcdefghigklmnopqrstuvwxyz0123456789+/'

def b64encode(src: str):
    ret = bytearray()
    if isinstance(src, str):
        _src = src.encode()
    else:
        return None
    for offset in range(0, len(_src), 3):
        triple = _src[offset:offset+3]

        r = 3 - len(triple)
        if r:
            triple += b'\x00' * r
        x = int.from_bytes(triple, 'big')
        for i in range(18, -1, -6):
            index = x >> i & 0x3F
            ret.append(alphabet[index])
        for i in range(r):
            ret[-i-1] = 61
    return ret

print(b64encode('abcdefg'))
```

优化一下
```python
alphabet = b'ABCDEFGHIGKLMNOPQRSTUVWXYZabcdefghigklmnopqrstuvwxyz0123456789+/'

def b64encode(src: str):
    ret = bytearray()
    if isinstance(src, str):
        _src = src.encode()
    else:
        return None
    for offset in range(0, len(_src), 3):
        triple = _src[offset:offset+3]

        r = 3 - len(triple)
        if r:
            triple += b'\x00' * r
        x = int.from_bytes(triple, 'big')
        for i in range(18, -1, -6):
            index = x >> i & 0x3F
            ret.append(alphabet[index])
        if r:
            ret[-r:] = b'='*r
    return ret

print(b64encode('abcdefg'))
```

## 命令分发器

```python
def command_dispatcher():
    command = {}

    def reg(name):
        def wrapper(fn):
            command[name] = fn
            return fn
        return wrapper

    def default_func():
        print("UNKNOWN COMMAND!")

    def dispatcher():
        while True:
            cmd = input('>>>')
            if cmd.strip() == '':
                break
            command.get(cmd, default_func)()
    return reg, dispatcher


reg, dispatcher = command_dispatcher()

@reg('f1')
def foo1():
    print('foo1')

@reg('f2')
def foo2():
    print('foo2')

dispatcher()
```

可以做一个加参数的分发器

### 方法一
```python
要实现下面的功能
@reg(f1, x=200, y = 300)
```
解法
```python
def command_dispatcher():
    command = {}

    def reg(name, *args, **kwargs):
        def wrapper(fn):
            command[name] = fn, args, kwargs
            return fn
        return wrapper

    def default_func():
        print("UNKNOWN COMMAND!")

    def dispatcher():
        while True:
            cmd = input('>>>')
            if cmd.strip() == '':
                break
            fn, args, kwargs = command.get(cmd, (default_func, (), {}))
            fn(*args, **kwargs)
    return reg, dispatcher


reg, dispatcher = command_dispatcher()

@reg('f1', 200, 300)
@reg('f2', 300, 400)
def foo1(x, y):
    print('foo1',x+y)

@reg('f4')
def foo2():
    print('foo2')

dispatcher()
```

### 方法二
```python
实现下面的功能
>> f2 100 200
foo2 300
```

```python
def command_dispatcher():
    command = {}

    def reg(name):
        def wrapper(fn):
            command[name] = fn
            return fn
        return wrapper

    def default_func(*args, **kwargs):
        print("UNKNOWN COMMAND!")

    def dispatcher():
        while True:
            cmd = input('>>>')
            if cmd.strip() == '':
                break
            args, kwargs = [], {}
            func_name, *params = cmd.replace(",", ' ').split()
            for param in params:
                x = param.split('=', maxsplit=1)
                if len(x) == 1:
                    args.append(int(x[0]))
                if len(x) == 2:
                    kwargs[x[0]] = int(x[1])
            command.get(func_name, default_func)(*args,**kwargs)
    return reg, dispatcher


reg, dispatcher = command_dispatcher()

@reg('f1')
def foo1(x, y):
    print('foo1',x+y)

dispatcher()
```
