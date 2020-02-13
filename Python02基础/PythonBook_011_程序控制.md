# Python程序控制

## 顺序控制
- 按照先后顺序一条条执行
- 例如，先点餐，后吃饭



## 分支控制
- 根据不同的情况判断，条件满足执行某条件下的语句
- 例如，点餐后,如果没有好,就玩手机;如果饭好了,就吃饭

### 单分支语句

```
if 1 <= 2:
    print('1 little than 2')
else:
    print('1 is not little than 2')
----        
1 little than 2
```

### 多分支语句
- 多分支结构，只要有一个条件成立，就不进行其他分支的判断

```
score = 81
if score == 100:
    print("Well")
elif score >= 80:
    print('Good')
elif score >= 60:
    print("Not Bad")
else:
    print("Hard Work")
----
Good
```

### 练习
随意给出五位以内的数，输出其位数;举例：333 三位数

```
a = int(input('Please give a number between 1~9999'))
if a >= 100:
    if a >= 1000:
        if a >= 10000:
            print("5")
        else:
            print("4")
    else:
        print("3")

elif a >=10:
    print("2")
else:
    print("1")
```


## 循环
- 条件满足时一直执行，不满足就不执行或不再执行
- 比如，如果存款小于100万，就一直攒钱;这里的条件是存款小于100万，这个条件成立，就一直执行攒钱这个动作

### while循环
语法
while True:
    pass

```
Flag = 10
while Flag:
    print(Flag)
    Flag -= 1
----
10
9
8
7
6
5
4
3
2
1
```


### for循环
for循环一般多用于遍历文件

#### 打印列表的元素

```
lst = [1,3,4,5,6]
for i in lst:
    print(i)
----
1
3
4
5
6
```
#### 打印0-9
>注意range的左闭右开区间


```
for i in range(10):
    print(i)
----
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
```
#### 定义`range`的步长

```
for i in range(10,-1,-2):
    print(i)
----
10
8
6
4
2
0
```
