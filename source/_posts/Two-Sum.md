---
title: Two Sum
date: 2017-08-12 21:59:56
tags: LeetCode
author: yxcui
---

![LeetCode 问题页](Two-Sum\Two-Sum.jpg)


### Question
> Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

### Example
>- Given nums = [2, 7, 11, 15], target = 9
>+ Because nums[0] + nums[1] = 2 + 7 = 9,
>- return [0, 1].

### Solution
``` python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """

        allindices = []
        for i in range(len(nums)):
            # The 'rest' is from 'target' minus each 'element' traversed from the list, and then judge whether the 'rest' is exist in list.
            rest = target - nums[i]

            if rest in nums:
                allindices.append((i, nums.index(rest)))

        indices = []
        for t in allindices:
            if t[0] != t[1]:
                indices.append(tuple(sorted(t)))
        return list(set(indices))

if __name__ == "__main__":
    s = Solution()
    indices = s.twoSum([0, 4, 3, 0], 0)
    print indices

```

### Review
>To improve the efficience of running, it's need to optimize. And if you have a better idea or suggestion, please leave your words here!

> [代码链接](https://github.com/yxcui/LeetCode/blob/master/Two%20Sum.py)