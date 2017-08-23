---
layout: post
title: LeeCode28 Implement strStr
categories: [LeetCode]
description: LeetCode
keywords: LeetCode
---

Implement strStr().
Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

每次从i位置开始匹配len(needle)长度字符串是否相等
```python
class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        l1 = len(haystack)
        l2 = len(needle)
        
        if l2 == 0:
            return 0
        
        for i in range(l1):
            if (l1 - i + 1) < l2:
                return -1
            if haystack[i] != needle[0]:
                continue
            if haystack[i : l2 + i] == needle:
                return i
        return -1
```

```c
class Solution {
public:
    int strStr(string haystack, string needle) {
        int n = haystack.size();
        int m = needle.size();
        
        if(m == 0)
            return 0;
        if(n < m)
            return -1;
        
        for(int i=0; i<=n-m; i++){
            int j = 0;
            
            while(i+j < n && haystack[i+j] == needle[j]) //记录相等的长度
                j++;
            
            if(j == m)
                return i;
        }
        
        return -1;
        
        
    }
};
```