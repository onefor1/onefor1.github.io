---
layout: post
title: LeeCode8 String to Integer (atoi)
categories: [LeetCode]
description: LeetCode
keywords: LeetCode
---

Implement atoi to convert a string to an integer.

这里主要注意以下几个地方：
1. 数字开始之前的空格都要忽略
2. 数字只能以'+', '-', '0'开头
3. 数字开始之后，若出现任何非数字字符，则停止，后面的所有字符将忽略不计
4. 越界问题，数字总大小不能大于integer的最大值，或者小于interger的最小值

几个特殊的测试用例（[]内的内容）：
1. [2147483648]
2. [000+10]
3. [123abc]
4. [+-123]
5. [    123]

C++ Code:
```c++
class Solution {
public:
    int myAtoi(string str) {
        int len = str.length();
        if(len == 0) 
            return 0;
        long sum = 0; //save the result
        int num_length = 0; //the lenght of sum
        int start_index = 0; // the index of the string, where the number start count
        bool flag = true; //the flag of plus number or minus number
        for(int i=0; i<len; i++){
            if(start_index == i){
                if(str[i] == ' '){
                    start_index++;
                    continue;
                }
                if(str[i] == '+' || str[i] == '0'){
                    continue;
                }
                if(str[i] == '-'){
                    flag = false;
                    continue;
                }
            }
            
            if(str[i] >= '0' && str[i] <= '9'){
                sum = sum*10 + str[i] - '0';
                num_length += 1;
                if(num_length > 10){
                    break;
                }
            }else{
                break;
            }
        }
        
        if(flag){//max int: 2147483647, min int: -2147483648
            if(sum > INT_MAX)
                return INT_MAX;
        }else{
            sum = -sum;
            if(sum < INT_MIN)
                return INT_MIN;
        }
        return sum;
        
    }
};
```

Python Code:
```python
class Solution(object):
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        result = 0 
        flag = True #plus number or minus number
        num_len = 0 #the length of number
        start_index = 0 #the number start index of the input string
        INT_MAX = 2147483647
        INT_MIN = -2147483648
        
        for index, ch in enumerate(str):
            #handle for special ch: " ", "+", "-"
            if start_index == index:
                if ch == " ":
                    start_index += 1
                    continue
                if ch == "+":
                    continue;
                if ch == "-":
                    flag = False
                    continue
            
            if ch >= "0" and ch <= "9":
                result = result * 10 + ord(ch) - ord('0')
                num_len += 1
                if num_len > 10: #sum exceed the INT_MAX
                    break
            else:
                break
                
        if flag:
            if result > INT_MAX:
                return INT_MAX
        else:
            result = -result
            if result < INT_MIN:
                return INT_MIN
        return result
```