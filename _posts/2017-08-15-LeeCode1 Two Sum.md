---
layout: post
title: LeetCode1 Two Sum
categories: [LeetCode]
description: LeetCode
keywords: LeetCode
---

Example
```c
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
使用dict记录下每一个target - num[i]及其下标，若num中存在target - num[i]则直接返回，代码如下所示

```python
def twoSum(nums, target):
	'''
	leetcode 1: Two Sum
	'''
	d = {}
	for key, value in enumerate(nums):
		left = target - value
		if d.has_key(str(value)):
			return [d[str(value)], key]
		else:
			d[str(left)] = key
```