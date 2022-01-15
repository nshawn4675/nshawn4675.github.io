---
layout: post
title: "[LeetCode April Challange] Day 14 - Partition List"
date: 2021-04-14 00:00:00 +0800
categories: LeetCode
tags: [Medium, Linked List, Two Pointers, Microsoft, Amazon, Apple, Facebook, C++]
---
Given the <font color="red">head</font> of a linked list and a value <font color="red">x</font>, partition it such that all nodes **less than** <font color="red">x</font> come before nodes **greater than or equal** to <font color="red">x</font>.

You should **preserve** the original relative order of the nodes in each of the two partitions.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/86_ex1.jpg?raw=true)

    Input: head = [1,4,3,2,5,2], x = 3
    Output: [1,2,2,4,3,5]

# Example 2:

    Input: head = [2,1], x = 2
    Output: [1,2]

# Constraints:

- The number of nodes in the list is in the range <font color="red">[0, 200]</font>.
- <font color="red">-100 <= Node.val <= 100</font>
- <font color="red">-200 <= x <= 200</font>

______________________  

# Solution  

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
        ListNode* partition(ListNode* head, int x) {
            ListNode *lt_dummy_head = new ListNode();
            ListNode *egt_dummy_head = new ListNode();
            ListNode *lt = lt_dummy_head;
            ListNode *egt = egt_dummy_head;
            for (ListNode *curr=head; curr; curr=curr->next) {
                if (curr->val < x) {
                    lt->next = curr;
                    lt = lt->next;
                } else {
                    egt->next = curr;
                    egt = egt->next;
                }
            }
            egt->next = nullptr;
            lt->next = egt_dummy_head->next;
            return lt_dummy_head->next;
        }
    };

從頭到尾掃一遍，用兩個指標記錄 小於x & 大於等於x 的 node 順序。  
掃完後，將 lt 與 egt 串起來，egt 下一個設為 nullptr，完工。