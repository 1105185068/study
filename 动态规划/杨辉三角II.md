# 杨辉三角
## 杨辉三角II
### 问题描述
给定一个非负索引 k，其中 k ≤ 33，返回杨辉三角的第 k 行。

如图：<https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif>

在杨辉三角中，每个数是它左上方和右上方的数的和。

**示例:**
```
输入: 3
输出: [1,3,3,1]
```
**进阶：**

你可以优化你的算法到 O(k) 空间复杂度吗？

### 问题分析
由杨辉三角I可知，直接可以使用计算出整个杨辉三角，然后返回题目所需要的某一行

### 代码示例
```python
class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        result=[]
        for i in range(rowIndex+1):
            now=[1]*(i+1)
            if i >=2:
                for n in range(1,i):
                    now[n]=pre[n-1]+pre[n]
            result+=now
            pre=now
        return pre
```
