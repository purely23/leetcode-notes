# 0015. 三数之和（3Sum）

**链接**：https://leetcode.com/problems/3sum/

**标签**：数组、双指针、排序　|　难度：中等

## 思路

目标是找出所有和为0的三元组，且不能重复。

暴力法的思路是三层循环枚举所有组合，再用集合去重，时间复杂度立刻变成三次方级别，且去重逻辑会变得很啰嗦。

关键转折点：如果先排序，问题就能降一维。固定第一个数之后，剩下两个数的和等于一个固定目标值，这就退化成了在有序数组里找两数之和，可以用双指针从两端向中间收缩，不需要再嵌套一层循环。排序带来的额外好处是去重可以通过跳过相邻重复值直接处理，不需要再用集合。

## 复杂度对比

| 方法 | 时间复杂度 | 空间复杂度 |
|---|---|---|
| 暴力三层循环 + 集合去重 | O(n^3) | O(n) |
| 排序 + 固定一位 + 双指针收缩 | O(n^2) | O(1)（不计排序栈开销） |

## 代码

```python
def threeSum(nums):
    nums.sort()
    n = len(nums)
    result = []
    for i in range(n - 2):
        if i > 0 and nums[i] == nums[i - 1]:
            continue
        if nums[i] > 0:
            break
        left, right = i + 1, n - 1
        while left < right:
            total = nums[i] + nums[left] + nums[right]
            if total < 0:
                left += 1
            elif total > 0:
                right -= 1
            else:
                result.append([nums[i], nums[left], nums[right]])
                while left < right and nums[left] == nums[left + 1]:
                    left += 1
                while left < right and nums[right] == nums[right - 1]:
                    right -= 1
                left += 1
                right -= 1
    return result
```

## 易错点

固定第一个数之后忘记跳过重复值，导致结果集出现重复三元组。

找到一组解之后，忘记同时收缩左右指针，导致死循环或漏解。

排序之后如果当前固定的数已经大于0，后面不可能再凑出和为0的组合，可以直接break，这一步容易漏掉，影响效率但不影响正确性。

## 关联题目

0001 两数之和：同样是求和问题，但数据规模小，直接用哈希表更合适，不需要排序，对比这两题能体会到"双指针收缩"适用的前提是数组有序，"哈希表查找"适用的前提是只需要常数次查找。

0018 四数之和：思路是在本题外面再套一层固定，本质是同一个收缩套路的递归扩展。

0011 盛最多水的容器：双指针收缩的思路来源同一类型，但收缩方向的判断依据不同，对比能加深对"双指针为什么这样移动"的理解，而不是死记套路。
