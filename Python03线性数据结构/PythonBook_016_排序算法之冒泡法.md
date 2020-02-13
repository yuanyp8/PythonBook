# 排序算法

## 练习
依次给出三个数，排序后打印输出

## 方法
1. 转换int后，判断大小排序，使用分支结构
2. 使用max函数
3. 使用列表的sort方法
4. 冒泡法

### 1. 分支结构

```python
# 得到一个三个随机数的列表
lst = [random.randint(1,10) for i in range(3)]
print(lst)
# 用分支结构进行判断
if lst[0] >= lst[1]:
    if lst[0] >= lst[2]:
        if lst[1] >= lst[2]:
            print(lst[0],lst[1],lst[2])
        else:
            print(lst[0],lst[2],lst[1])
    else:
        print(lst[2],lst[0],lst[1])
else:
    if lst[1] >= lst[2]:
        if lst[0] >= lst[2]:
            print(lst[1],lst[0],lst[2])
        else:
            print(lst[1],lst[2],lst[0])
```
得出结果
```
[6, 8, 2]
8 6 2
```

### 2. 使用max函数

```python
import random

lst = [random.randint(1,10) for i in range(3)]
print(lst)

# 使用max函数得到最大值
max_num = max(lst)
lst.remove(max_num)
sec_num = max(lst)
lst.remove(sec_num)
print(max_num,sec_num,lst[0])  
```
得出结果
```
[10, 3, 2]
10 3 2
```
### 3. 使用sort排序

```python
lst = [random.randint(1,10) for i in range(3)]
print(lst)
lst = sorted(lst,reverse=True)
print(lst)
```
#### 4.使用冒泡法
>冒泡排序（Bubble Sort）也是一种简单直观的排序算法。它重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。走访数列的工作是重复地进行直到没有再需要交换，也就是说该数列已经排序完成。这个算法的名字由来是因为越小的元素会经由交换慢慢"浮"到数列的顶端。

![](https://www.runoob.com/wp-content/uploads/2019/03/bubbleSort.gif)


```python
# 给出10个随机数
import random

lst = [random.randint(1,100) for i in range(10)]
print(lst)
for i in range(len(lst)):
    flag = False
    for j in range(0,len(lst)-1-i):
        if lst[j] > lst[j+1]:
            tmp = lst[j]
            lst[j] = lst[j+1]
            lst[j+1] = tmp
            flag = True
    if not flag:
        break
print(lst)
```
得出结果
```
[34, 5, 35, 34, 85, 94, 38, 69, 85, 17]
[5, 17, 34, 34, 35, 38, 69, 85, 85, 94]
```

> 时间复杂度计算为最坏情况，时间复杂度为O(n^2)
