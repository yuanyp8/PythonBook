# 课后习题
## 猴子吃桃问题：
猴子第一天摘下若干个桃子，当即吃了一半，还不过瘾，又多吃了一个，第二天早上又将剩下的桃子吃掉一半，又多吃了一个。以后每天早上都吃前一天剩下的一半零一个。到第10天早上想再吃时，见只剩下一个桃子了。求第一天共摘多少个桃子？



```python

patch = 1
for i in range(9):
    patch = 2*(patch+1)
print(patch)

----
1534
```

## 求第m行第k个数
>第几行就有第几个元素，所以k肯定<=m
之前我们有补0法、对称法、单行覆盖法等

### 简单的方法

```python
m = 10
k = 5
lst = []
for i in range(m):
    lst.append([1]*(i+1))
    for j in range(i-1):
        lst[i][j+1] = lst[i-1][j] + lst[i-1][j+1]
print(lst[m-1][k-1])
```
### 考虑到中点和单行覆盖

```python
# 考虑中点和单行覆盖
m = 10
k = 5
triangle = [1]*m
for i in range(m):
    old = 1
    for j in range(i//2):
        tmp = old + triangle[j+1]
        old = triangle[j+1]
        triangle[j+1] = tmp
        triangle[i-j-1] = triangle[j+1]
print(triangle[:i+1][k-1])

----
126
```
### 组合数公式

#### 定义
组合是数学的重要概念之一。从 n 个不同元素中每次取出 m 个不同元素 ，不管其顺序合成一组，称为从 n 个元素中不重复地选取 m 个元素的一个组合。所有这样的组合的种数称为组合数。

![](https://bkimg.cdn.bcebos.com/pic/ca1349540923dd543f01bf4cdd09b3de9c8248a7?x-bce-process=image/resize,m_lfit,w_250,h_250,limit_1)

#### 代码

```python
# 杨辉三角的组合数解法
# 求第10行第4列的的杨辉三角数
# 因为列表索引为0起始，所以要减一

m = 10
k = 5

# (m-1)!/(k-1)!(m-k)!

target = []
factorial = 1
for i in range(1,m):
    factorial *= i
    if i == m-1:
        target.append(factorial)
    if i == k-1:
        target.append(factorial)
    if i == m-k:
        target.append(factorial)
print(target[2]//(target[0]*target[1]))

----
126
```

## 数字统计
随机产生10个数字
要求：
- 每个数字取值范围[1,20]
- 统计重复的数字有几个，分别是什么
- 统计不重复的数字，分别是什么
- 举例子：11，7，5，11，6，7，4，其中7和11重复了，3个数字4，5，6，没有重复


### 不用排序，直接遍历查询

```python
lst = [11,2,5,44,44,22,11]
target = [False]*len(lst)
samenum = []
diffnum = []
for i in range(len(lst)):
    flag = False
    if target[i]: continue
    for y in range(i+1,len(lst)):
        if lst[i] == lst[y]:
            target[y] = True
            flag = True

    if flag:
        samenum.append(lst[i])
        target[i] = True
    else:
        diffnum.append(lst[i])
print(samenum,diffnum)

----
[11, 44] [2, 5, 22]
```


### 接下来，计算出重复的次数

```python
lst = [11,2,5,44,44,22,11]
target = [0]*len(lst)
samenum = []
diffnum = []
for i in range(len(lst)):
    count = 0
    if target[i]:
        continue
    for y in range(i+1,len(lst)):
        if lst[i] == lst[y]:
            count += 1
            target[y] = count

    if count:
        count += 1
        samenum.append((lst[i],count))
        target[i] = count
    else:
        diffnum.append(lst[i])
print(samenum,'\n',diffnum)

----
[(11, 2), (44, 2)]
 [2, 5, 22]
```
