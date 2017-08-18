---
layout: post
title: LeeCode20 Valid Parentheses
categories: [LeetCode]
description: LeetCode
keywords: LeetCode
---

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

我的思路：遇到'(', '{', '[' 就存入List，遇到')', '}', ']'则pop出List中的最后一个元素与它匹配

Python第一版：
```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        left = [] #store the left brackets
        for ch in s:
            if ch in ['(', '{', '[']:
                left.append(ch)
            elif len(left):
                if ch == ')' and left.pop() != '(':
                    return False
                if ch == '}' and left.pop() != '{':
                    return False
                if ch == ']' and left.pop() != '[':
                    return False
            else:# left right-brackets not close
                return False
                
        if len(left): #left left-brackets not close
            return False
        
        return True
```

Python第二版：
```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = [] #store the left brackets
        brackets = {')':'(', '}':'{', ']':'['}
        for ch in s:
            if ch not in brackets:
                stack.append(ch)
            else:
                if not stack:
                    return False
                if stack.pop() != brackets[ch]:
                    return False
                
        return not stack
```

C++版：不用map效率会快一些
```c++
class Solution {
public:
    bool isValid(string s) {
        stack<char> left;
        map<char, char> brackets = {{'}', '{'}, {')', '('}, {']', '['}};
        int len = s.length();
        char ch;
        for(int i=0; i<len; i++){
            if(brackets.find(s[i]) == brackets.end()){
                left.push(s[i]);
            }else{
                if(left.empty())
                    return false;
            
                ch = left.top();
                if(ch != brackets[s[i]])
                    return false;
                left.pop();
            }
        }
        return left.empty();                
        
    }
};
```
