# 两个数组的交集II
## 问题描述
给定两个数组，编写一个函数来计算它们的交集。

**示例 1：**
```
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2,2]
```
**示例 2:**
```
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[4,9]
```

**说明：**

+ 输出结果中每个元素出现的次数，应与元素在两个数组中出现次数的最小值一致。
+ 我们可以不考虑输出结果的顺序。

**进阶：**

+ 如果给定的数组已经排好序呢？你将如何优化你的算法？
+ 如果 ***nums1*** 的大小比 ***nums2*** 小很多，哪种方法更优？
+ 如果 ***nums2*** 的元素存储在磁盘上，内存是有限的，并且你不能一次加载所有的元素到内存中，你该怎么办？

## 方法一：暴力法
### 代码示例
```python
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        if len(nums2) < len(nums1):
            nums1, nums2 = nums2, nums1
        output = []
        for i in nums1:
            for j in nums2:
                if i == j:
                    output.append(i)
                    nums2.remove(j)
                    break
        return output
```

## 方法二：直接法
```python
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        a=[]
        b=set(nums1)&set(nums2)
        for i in b:
            a+=[i]*(min(nums1.count(i),nums2.count(i)))
        return a
```

## 方法三：双指针
```python
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        nums1 = sorted(nums1)
        nums2 = sorted(nums2)
        i = 0
        j = 0
        output = []
        while i < len(nums1) and j < len(nums2):
            if nums1[i] > nums2[j]:
                j += 1
            elif nums1[i] < nums2[j]:
                i += 1
            else:
                output.append(nums1[i])
                i += 1
                j += 1
        return output
```

## 方法四：直接计数法
```python
import collections
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        a, b = map(collections.Counter, (nums1, nums2))
        return list((a & b).elements())
```
