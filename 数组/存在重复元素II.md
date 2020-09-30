# 存在重复元素II
## 问题描述
给定一个整数数组和一个整数 k，判断数组中是否存在两个不同的索引 i 和 j，使得 **nums [i] = nums [j]**，并且 i 和 j 的差的 ***绝对值*** 至多为 k。

**示例 1:**
```
输入: nums = [1,2,3,1], k = 3
输出: true
```
**示例 2:**
```
输入: nums = [1,0,1,1], k = 1
输出: true
```
**示例 3:**
```
输入: nums = [1,2,3,1,2,3], k = 2
输出: false
```

## 方法一：哈希表
## 题解
1. 初试化哈希表hash={}

2. 遍历数组：

  - 若nums[i]不在hash中，则令nums[i]为key，value为当前的索引i。
  - 若已存在：
> + 判断当前的索引和上一相同元素的索引差是否小于等于k，即i−hash[nums[i]]<=k。若满足，返回True。
>+ 将索引更新为当前索引，hash[nums[i]]=i
3. 返回False

## 复杂度分析
+ 时间复杂度：O(n)，进行了一次遍历。
+ 空间复杂度：O(n)，借助hash存储过程。

### 代码示例
```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        hash={} #创建一个空字典
        for i in range(len(nums)):
            if(nums[i] not in hash): # 如果该元素不在字典中
                hash[nums[i]]=i # 将其键设为该元素，值为该元素所在数组中位置
            else:
                if(i-hash[nums[i]]<=k): # 如果该元素在字典中，遍历时第二次遇到该元素,且其两次所在位置差的绝对值小于K
                    return True # 返回true
                else:
                    hash[nums[i]]=i #更新该元素的位置
        return False
```

## 方法二：暴力法(数据过大会超时)
**超出时间限制**
```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        n=len(nums)
        for i in range(n):
            for j in range(i+1,n):
                if nums[i]==nums[j] and j-i<=k:
                    return True
        return False
```
