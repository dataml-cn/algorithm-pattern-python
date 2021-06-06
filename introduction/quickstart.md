# 快速开始

## 数据结构与算法

数据结构是一种数据的表现形式，如链表、二叉树、栈、队列等都是内存中一段数据表现的形式。
算法是一种通用的解决问题的模板或者思路，大部分数据结构都有一套通用的算法模板，所以掌握这些通用的算法模板即可解决各种算法问题。

后面会分专题讲解各种数据结构、基本的算法模板、和一些高级算法模板，每一个专题都有一些经典练习题，完成所有练习的题后，你对数据结构和算法会有新的收获和体会。

先介绍两个算法题，试试感觉~

**示例 1** [strStr](https://leetcode-cn.com/problems/implement-strstr/)

> 给定一个  haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从 0 开始)。如果不存在，则返回  -1。

**思路**
核心点遍历给定字符串字符，判断以当前字符开头字符串是否等于目标字符串

1. **遍历所有潜在可能候选集**，原字符串 haystack 中每个字符作为子串的开始，注意最后一个可能子串的索引
2. **检测潜在对象是否成立**，成立终止循环，不成立继续循环

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:

        # return self.strStr_str_equal(haystack, needle)
        return self.strStr_char_equal(haystack, needle)

    # CPU: 32ms, 96.92%, Memory: 14.8M, 95.42%
    def strStr_str_equal(self, haystack: str, needle: str) -> int:
        needle_len = len(needle)
        haystack_len = len(haystack)

        if needle_len == 0:
            return 0
        elif needle_len > haystack_len:
            return -1
        else:
            for i in range(haystack_len - needle_len + 1):
                if haystack[i: i + needle_len] == needle:
                    return i    
            return -1

    # CPU: 32ms, 96.92%, Memory: 15M, 56.91%
    def strStr_char_equal(self, haystack: str, needle: str) -> int:

        needle_len = len(needle)
        haystack_len = len(haystack)

        if needle_len == 0:
            return 0
        elif needle_len > haystack_len:
            return -1
        else:
            for i in range(haystack_len - needle_len + 1):
                j = 0
                for j in range(needle_len):
                    if haystack[i + j] != needle[j]: 
                        break
                if j == needle_len - 1 and haystack[i + j] == needle[j]:
                    return i    
            return -1
```

**注**

- 如果找到目标字符串，haystack[i: i + needle_len] == needle
- 如果找到目标字符串，len(needle) == j - 1, 且 haystack[i + j] == needle[j]


**示例 2** [subsets](https://leetcode-cn.com/problems/subsets/)

> 给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

**思路**
这是一个典型的应用回溯法的题目，简单来说就是穷尽所有可能性，通过不停的选择，撤销选择，来穷尽所有可能性，最后将满足条件的结果返回，算法模板如下

```pyton
result = []
def backtrack(选择列表, 路径):
    if 满足结束条件:
        result.add(路径)
        return
    for 选择 in 选择列表:
        做选择
        backtrack(选择列表, 路径)
        撤销选择
```

```python
class Solution:

    def subsets(self, nums: List[int]) -> List[List[int]]:
        # return self.subsets_enumerate(nums)
        return self.subsets_search(nums)
    
    # CPU: 36ms, 85.23%, MEMORY: 14.8M, 94.11%
    def subsets_enumerate(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        result = []

        for i in range(1<<n):

            t = []
            for j in range(n):
                if (i >> j & 1) == 1:
                    t.append(nums[j])
            result.append(t)

        return result

    
    # CPU: 24ms, 99.81%, MEMORY: 15M, 62.37%
    def subsets_search(self, nums: List[int]) -> List[List[int]]:

        def _search(tmp:List[int], pos, nums, result) -> None:
            result.append(tmp.copy())

            for i in range(pos + 1, len(nums)):
                tmp.append(nums[i])
                _search(tmp, i, nums, result)
                tmp.pop()

        result = []
        temp = []
        pos = -1

        _search(temp, pos, nums, result)

        return result
```

**注**

- 后面会深入讲解几个典型的回溯算法问题，如果当前不太了解可以暂时先跳过

## 注意点

- 快速定位到题目的知识点，找到知识点的**通用模板**，可能需要根据题目**特殊情况做特殊处理**。
- 先去朝一个解决问题的方向！**先抛出可行解**，而不是最优解！先解决，再优化！
- 代码的风格要统一，熟悉各类语言的代码规范，命名尽量简洁明了。
- 常见错误总结
  - 访问下标时，不能访问越界
  - 空值 null 问题 run time error

## 练习

- [x] [strStr](https://leetcode-cn.com/problems/implement-strstr/)
- [x] [subsets](https://leetcode-cn.com/problems/subsets/)
