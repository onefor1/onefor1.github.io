---
layout: post
title: LeeCode88 Merge Sorted Array
categories: [LeetCode]
description: LeetCode
keywords: LeetCode
---

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

想法： 
因为不能返回新的数组，只能在原来的nums1上进行修改，所以有两种比较方法：
（1）从前往后插入最小元素，那么每次nums1的元素都要往后移动很多元素
（2）从后往前插入最大元素，每次只会改变一个位置的元素
所以肯定选择第二种方法

```python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: void Do not return anything, modify nums1 in-place instead.
        """
        if not n:
            return
        while m and n:
            if nums1[m-1] > nums2[n-1]:
                nums1[m+n-1] = nums1[m-1]
                m -= 1
            else:
                nums1[m+n-1] = nums2[n-1]
                n -= 1
        if n:
            nums1[:n] = nums2[:n]
```