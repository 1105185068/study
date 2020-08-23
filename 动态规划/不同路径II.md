# 不同路径II
## 问题描述
一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

|Start|||||
|-|-|-|-|-|
||||||
|||||Finish|

**网格中的障碍物和空位置分别用 1 和 0 来表示。**

**说明**：m 和 n 的值均不超过 100。

**示例 1**:
```
输入:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
输出: 2
解释:
3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右
```
## 解题思路
两个最近写的走格子的DP题解：

<https://leetcode-cn.com/problems/wildcard-matching/solution/yi-ge-qi-pan-kan-dong-dong-tai-gui-hua-dpsi-lu-by-/>

<https://leetcode-cn.com/problems/maximum-length-of-repeated-subarray/solution/yi-zhang-biao-ba-ju-hua-kan-dong-dong-tai-gui-hua-/>

不过这道的题目比前面两道容易想很多
 
首先我们看两个表格，上边是地图，下边是可到达每一格的路线数量记录

**地图**

||||
|-|-|-|
||障||
||||

**路线数记录**

||||
|-|-|-|
||||
||||

机器人的行动路线，题目说只能是右or下，但**反过来说**：

即：每次到达一个新的格子，只要看左or上面的格子有没有路线即可，有的话就整合起来。

即：store[m][n]当前格字路线数 = store[m-1][n]上面格子路线数 + store[n-1][m]左边格子路线数

(其中，"store"为右边储存路线数量的表格)

初始化：一开始站在左上角位置，站都站在那了，那路线肯定=1(除非0,0位置就是障碍)；其他格子还没走，路线数先初始化为0

(注：代码中是下面这样写的, 所以遇到(0,0)位置就是障碍物的按情况是不会报错的)
```
如果该格子不是障碍格：
    如果该格子是(0,0)位置：
        该格子路线数=1
    ...以下省略
```
## 初始化图例：
**地图**

||||
|-|-|-|
||障||
||||

**路线数记录**

|1|0|0|
|-|-|-|
|0|0|0|
|0|0|0|

障碍处理：

有障碍 = 此路不通 = 此格没有路线 = 此格路线数为0

由于初始化每一格路线数 = 0，

所以遇到障碍格，不更新该格即可。
 
边界情况处理：

上面没格子，就只看左边

左边没格子，就只看上面
 
另外：

问：为了正确更新当前格子，如何保证左边、上面的格子已经更新过？

答：只要你的循环是从上到下、从左到右的，就能保证每次当前格的左边、上面的格子已经更新过。
 
返回：

由于最后到达的是右下角格子，直接返回这一格路线数即可
 
两个DP完例子供参考：

**地图1**

||||
|-|-|-|
||障||
||||

**路线数记录1**

|1|1|1|
|-|-|-|
|1|0|1|
|1|1|2|

**地图2**

||||
|-|-|-|
||障||
||||

**路线数记录2**

|1|1|1|
|-|-|-|
|1|2|3|
|1|3|6|

## 代码示例
1.可以新建一个"store"专门储存路线
```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        #新建矩阵版
        height, width = len(obstacleGrid),len(obstacleGrid[0])
        store = [[0]*width for i in range(height)]

        #从上到下，从左到右
        for m in range(height):#每一行
            for n in range(width):#每一列
                if not obstacleGrid[m][n]: #如果这一格没有障碍物
                    if m == n == 0: #或if not(m or n)
                        store[m][n] = 1
                     else:
                        a = store[m-1][n] if m!=0 else 0 #上方格子
                        b = store[m][n-1] if n!=0 else 0 #左方格子
                        store[m][n] = a+b
        return store[-1][-1]
```
2.如果想在原来地图上记录路线也行
```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        #原矩阵版
        height, width = len(obstacleGrid),len(obstacleGrid[0])

        #从上到下，从左到右
        for m in range(height):#每一行
            for n in range(width):#每一列
                if obstacleGrid[m][n]: #如果这一格有障碍物
                    obstacleGrid[m][n] = 0
                else:
                    if m == n == 0: #或if not(m or n)
                        obstacleGrid[m][n] = 1
                    else:
                        a = obstacleGrid[m-1][n] if m!=0 else 0 #上方格子
                        b = obstacleGrid[m][n-1] if n!=0 else 0 #左方格子
                        obstacleGrid[m][n] = a+b
        return obstacleGrid[-1][-1]
```
3.己解(通俗易懂)
```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        high=len(obstacleGrid) #表示高度
        wid=len(obstacleGrid[0]) #表示宽度
        for m in range(high):
            for n in range(wid):
                if obstacleGrid[m][n]:
                    obstacleGrid[m][n]=0
                else:
                    if m==0 and n==0:
                        obstacleGrid[m][n]=1
                    else:
                        if m!=0:
                            a=obstacleGrid[m-1][n]
                        else:
                            a=0
                        if n!=0:
                            b=obstacleGrid[m][n-1]
                        else:
                            b=0
                        obstacleGrid[m][n]=a+b
        return obstacleGrid[-1][-1]
```
