---
layout: post
title:  "[LeetCode April Challange] Day 18 - Remove Nth Node From End of List"
date:   2021-04-18 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Linked List, Two Pointers, Facebook, Amazon, Apple, Bloomberg, Microsoft]
---
Given the <font color="red">head</font> of a linked list, remove the <font color="red">n-th</font> node from the end of the list and return its head.

**Follow up:** Could you do this in one pass?

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/19_ex1.jpg?raw=true)

    Input: head = [1,2,3,4,5], n = 2
    Output: [1,2,3,5]

# Example 2:

    Input: head = [1], n = 1
    Output: []

# Example 3:

    Input: head = [1,2], n = 1
    Output: [1]

# Constraints:

- The number of nodes in the list is <font color="red">sz</font>.
- <font color="red">1 <= sz <= 30</font>
- <font color="red">0 <= Node.val <= 100</font>
- <font color="red">1 <= n <= sz</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

    /**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode() : val(0), next(nullptr) {}
    *     ListNode(int x) : val(x), next(nullptr) {}
    *     ListNode(int x, ListNode *next) : val(x), next(next) {}
    * };
    */
    class Solution {
    public:
        ListNode* removeNthFromEnd(ListNode* head, int n) {
            if (head == nullptr) return head;
            
            ListNode *dummy_head = new ListNode(0, head);
            ListNode *first = dummy_head;
            while (0 <= n--) first = first->next;
            
            ListNode *second = dummy_head;
            while (first) {
                first = first->next;
                second = second->next;
            }
            second->next = second->next->next;
            
            return dummy_head->next;
        }
    };

概念是先用 first 跑 n+1 個，再與 second 同步跑。最後當 first 到達結尾時，second 的下一個即是第 n 個。  
如此一來 將 second->next = second->next->next，即可跳過第 n 個。
