# 只出现一次的数字II
## 问题描述
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现了三次。找出那个只出现了一次的元素。

**说明：**

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

**示例 1:**
```
输入: [2,2,3,2]
输出: 3
```
**示例 2:**
```
输入: [0,1,0,1,0,1,99]
输出: 99
```
### 解题思路
可参照：**只出现一次的数字**，其方法类似，均采用统计频次法

## 字典法
**本题使用字典来统计频次，可使用get()方法，也可使用标准库collections中的Couter()来统计频次**

### 方法一：使用get()
#### Python 代码示例
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        d={}
        for ch in nums:
            d[ch]=d.get(ch,0)+1
        for key,value in d.items():
            if value ==1:
                return key
```

### 方法二：使用库函数
#### Python 代码示例
```python
from collections import Counter
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        a=Counter(nums)
        for key,value in a.items():
            if value==1:
                return key
```
