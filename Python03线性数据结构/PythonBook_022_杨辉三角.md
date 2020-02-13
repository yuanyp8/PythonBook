# 杨辉三角
杨辉三角（也称帕斯卡三角）相信很多人都不陌生，它是一个无限对称的数字金字塔，从顶部的单个1开始，下面一行中的每个数字都是上面两个数字的和。

杨辉三角，是二项式系数在三角形中的一种几何排列，在中国南宋数学家杨辉1261年所著的《详解九章算法》一书中出现。在欧洲，帕斯卡（1623—-1662）在1654年发现这一规律，所以这个表又叫做帕斯卡三角形。帕斯卡的发现比杨辉要迟393年，比贾宪迟600年
![](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=4131437290,1213734484&fm=173&app=25&f=JPEG?w=639&h=404&s=7A283462099DD9C85E75B1C70100E0B1)




仔细观察杨辉三角的图形，你能发现组成它的数有什么排列规律吗？

它的前几层是这样的：杨辉三角的两条斜边都是由数字1组成的，而其余的数则是等于它肩上的两个数之和，以此类推。

![](https://pic.rmb.bdstatic.com/99fd119be3ca7616ae635b28e7181f7e4222.gif)


## 杨辉三角的性质

**1、最外层的数字始终是 1**

![img](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=1653743099,1906317408&fm=173&app=25&f=JPEG?w=640&h=317&s=80BCC13283C64CE0065989EE0300E020)最外层的数字始终是 1



**2、第二层是自然数列**

![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=3567828285,2783526848&fm=173&app=25&f=JPEG?w=640&h=317&s=21106C32898A4CC05471CDF703005023)第二层数字为自然数列



**3、第三层是三角数列**

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=2262465670,2881879293&fm=173&app=25&f=JPEG?w=640&h=323&s=1394752349D8D8CA56681D670300B063)第三层数字

什么是三角数列，看一下下图就明白了，这个数列中的数字始终可以组成一个完美的等边三角形。



**4、三角数列相邻数字相加可得方数数列**

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=171315352,1238023630&fm=173&app=25&f=JPEG?w=640&h=314&s=31BAE83289D8C4C01C7167570300C0E2)三角数列相邻数字相加的方数数列

什么又是方数数列呢？雷同与三角数列，就是它的数字始终可以组成一个完美的正方形。

![img](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=2270021126,3862060621&fm=173&app=25&f=JPEG?w=462&h=166&s=41DEAC725ED0FE1BF627974E030070FD)方数数列



**5、每一层的数字之和是一个2倍增长的数列**

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=3759105928,2460779452&fm=173&app=25&f=JPEG?w=640&h=319&s=08085C328182C8EA5E60F1C4030060E1)每一层数列之和



**6、斐波那契数列**

没错，如果按照一定角度将直线上的数字相加，我们也可以从杨辉三角中找到斐波那契数列。

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=2655702577,3617396354&fm=173&app=25&f=JPEG?w=640&h=313&s=3C8A7432D98054C2D470E144030020E3)隐藏的斐波那契数列

斐波那契数列是指从 0，1 两个数开始，每一位数始终是前两位的和。这个数列有个神秘的特性，即越往后，相邻两数的比值越来越逼近黄金分割数 0.618 (或1.618，两数互为倒数)。斐波那契数列和黄金分割数不但在大自然中处处可见，在人类的艺术设计中也是应用非常广泛。

![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=2202688941,3338494355&fm=173&app=25&f=JPEG?w=640&h=403&s=87B67C22310F60EA5AD45DCA0000A0B2)斐波那契螺旋线



**7、素数**

素数是指只能被 1 和它本身整除的数字。然而在杨辉三角里，除了第二层自然数列包含了素数以外，其他部分的数字都完美避开了素数。

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=23004487,1292752071&fm=173&app=25&f=JPEG?w=640&h=318&s=7D8E743A88C854C00871FFC70300C0A4)素数的分布



**8、可以被特定数整除的数字形成了奇妙的分形结构**

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=2155112110,1956613729&fm=173&app=25&f=JPEG?w=639&h=310&s=1C9EC81200A014A02B2E76E50300E027)可以被 2 整除的数字



![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=2533944321,2995813514&fm=173&app=25&f=JPEG?w=639&h=323&s=22B4652249D85CCA56E87B7503004067)可以被 3 整除的数字



![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=3766848036,1501747140&fm=173&app=25&f=JPEG?w=640&h=313&s=41BCA4728BD84CC05E58CE570300C0E6)可以被 4 整除的数字



![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=2633138722,927693944&fm=173&app=25&f=JPEG?w=640&h=317&s=10A8703222A85CA029FFD7D7030030A1)可以被 5 整除的数字



如果我们把杨辉三角再放大，就会发现这些可以被特定数字整数的数的分布非常有规律，它们会形成类似分形的图案。




## 上代码


### 分解步骤，先打印前6行
每个数字等于上一行的左右两个数字之和。可用此性质写出整个杨辉三角。即第n+1行的第i个数等于第n行的第i-1个数和第i个数之和。

```python
triangle = [[1],[1,1]] #第一行第二行为特例
for i in range(2,6):  #从第三到第四行打印
    pre = triangle[i-1]  #当前行的上一行
    cur = [1]           #当前行的开头是1
    for j in range(i-1):
        cur.append(pre[j+0]+pre[j+1]) #当前行的值为上一行的两个数相加
    cur.append(1)  #当前行的末位是一
    triangle.append(cur)
print(triangle)

----
[[1], [1, 1], [1, 2, 1], [1, 3, 3, 1], [1, 4, 6, 4, 1], [1, 5, 10, 10, 5, 1]]

```

### 把前两行的特例也使用公式表达

```python
triangle  = []

for i in range(6):
    cur = [1]
    triangle.append(cur)
    if i == 0:
        continue
    pre = triangle[i - 1]
    for j in range(i-1):
        cur.append(pre[j+1]+pre[j])
    cur.append(1)
print(triangle)
```


### 补0法
对于每行的首尾都是1。每一行的操作都是2次append()，严重影响效率
这种补0的方法虽然效率不一定高，但是也是一种思路



```python
from copy import deepcopy

triangle  = [[1],[1,1]]

for i in range(2,6):
    cc = deepcopy(triangle)
    pre = cc[i-1]
    pre.append(0)
    row = [None]*(i+1)
    for j in range(i+1):
        row[j] = pre[j-1] + pre[j]
    triangle.append(row)
print(triangle)
```


### 考虑对称性

中点的确定：
[1]
[1,1]
[1,2,1]
[1,3,3,1]
[1,4,6,4,1]
[1,5,10,10,5,1]



把整个杨辉三角看成一个左对齐的二维矩阵。

|    i     |  位置   |     中点索引     |
| :------: | :-----: | :--------------: |
| i == 2时 | 在第3行 | 中点的列索引j==1 |
| i == 3时 | 在第4行 |      无中点      |
| i == 4时 | 在第5行 | 中点的列索引j==2 |

得到以下规律，如果i==2j，则有中点。



```python
n = 10
#先把所有的行宽打印出来
lst = [[1]*(i+1) for i in range(n)]
print(lst)
#每行的首尾不用改变，都是1
#找到中点，考虑对称性
for i in range(2,n):
    for j in range(i//2):
        lst[i][j+1]  = lst[i-1][j] + lst[i-1][j+1]
        if i !=2j:
            lst[i][-j-2] = lst[i][j+1]
print(lst)

```

### 单行覆盖

重复利用一个列表，不保存所有数据，用完就覆盖  
利用中点的对称性也要注意负索引，变更为正索引
```python
n = 10   
lst = [1]*n
for i in range(n):
    for j in range(i//2):
        var = lst[j] + lst[j+1]
        lst[j+1] = var
        if i != 2*(j+1):
            lst[i-j-1] = var
    print(lst[:i+1])

----
[1]
[1, 1]
[1, 2, 1]
[1, 3, 3, 1]
[1, 4, 7, 4, 1]
[1, 5, 12, 12, 5, 1]
[1, 6, 18, 30, 18, 6, 1]
[1, 7, 25, 55, 55, 25, 7, 1]
[1, 8, 33, 88, 143, 88, 33, 8, 1]
[1, 9, 42, 130, 273, 273, 130, 42, 9, 1]
```
前三行没有问题，但是第四行(i=3)的时候发现不对了，因为lst[i+1]被刷新了，刷新成了新的计算后的值    
这时候我们要利用一个新的变量来保护这个被覆盖的值

```python
n = 10   
lst = [1]*n
for i in range(n):
    old = 1
    for j in range(i//2):
        var = old + lst[j+1]
        lst[j+1],old = var,lst[j+1]
        if i != 2*(j+1):
            lst[i-j-1] = var

    print(lst[:i+1])

----
[1]
[1, 1]
[1, 2, 1]
[1, 3, 3, 1]
[1, 4, 6, 4, 1]
[1, 5, 10, 10, 5, 1]
[1, 6, 15, 20, 15, 6, 1]
[1, 7, 21, 35, 35, 21, 7, 1]
[1, 8, 28, 56, 70, 56, 28, 8, 1]
[1, 9, 36, 84, 126, 126, 84, 36, 9, 1]
```
