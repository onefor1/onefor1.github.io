---
layout: post
title: LeeCode21 Merge Two Sorted Lists
categories: [LeetCode]
description: LeetCode
keywords: LeetCode
---

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

注意：两个List均已各个排序，所以只要其中一个List结束，另一个List直接接到最后即可

Python代码如下：
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        if not l1 and not l2:
            return None
        point = head = ListNode(0)
        while l1 and l2:
            if l1.val < l2.val:
                point.next, l1 = l1, l1.next
            else:
                point.next, l2 = l2, l2.next
            point = point.next
        point.next = l1 if l1 else l2
        return head.next
```

C++代码如下：
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* head = new ListNode(0);
        ListNode* pointer = head;
        while(l1 && l2)
        {
            if(l1->val < l2->val)
            {
                pointer->next = l1;
                l1 = l1->next;
            }else{
                pointer->next = l2;
                l2 = l2->next;
            }
            pointer = pointer->next;
        }
        pointer->next = l1 ? l1 : l2;
        return head->next;
    }
};
```