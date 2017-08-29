---
layout: post
title: LeeCode88 Merge Sorted Array
categories: [LeetCode]
description: LeetCode
keywords: LeetCode
---

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.

Note:
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

想法：
python中for循环比较，比s1 == s1[::-1]判断反转字符串与自身是否相等要慢

```python
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        if not s:
            return True
        s1 = [i.lower() for i in s if i.isalnum()]

        return s1 == s1[::-1]
```