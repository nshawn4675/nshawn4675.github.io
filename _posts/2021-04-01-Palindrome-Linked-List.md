---
layout: post
title: "[LeetCode April Challange] Day 01 - Palindrome Linked List"
date: 2021-04-01 00:00:00 +0800
categories: LeetCode
tags: [Easy, Linked List, Two Pointers, Stack, Recursion, Microsoft, Facebook, Amazon, Adobe, Capital One, Google, Oracle, Bloomberg, Uber, Snapchat, payTM, C++]
---
Given the <font color="red">head</font> of a singly linked list, return <font color="red">true</font> if it is a palindrome.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/234_ex1.jpg?raw=true)

    Input: head = [1,2,2,1]
    Output: true

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/234_ex2.jpg?raw=true)

    Input: head = [1,2]
    Output: false
 

# Constraints:

- The number of nodes in the list is in the range <font color="red">[1, 10^5]</font>.
- <font color="red">0 <= Node.val <= 9</font>
 

**Follow up:** Could you do it in <font color="red">O(n)</font> time and <font color="red">O(1)</font> space?

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
        bool isPalindrome(ListNode* head) {
            ListNode *firstEnd = endOfFirstHalf(head);
            ListNode *revSecHalf = reverseList(firstEnd->next);
            
            ListNode *p1 = head, *p2 = revSecHalf;
            bool ans = true;
            while (ans && p2 != nullptr) {
                if (p1->val != p2->val) ans = false;
                p1 = p1->next;
                p2 = p2->next;
            }
            firstEnd->next = reverseList(firstEnd->next);
            return ans;
        }
    private:
        ListNode* endOfFirstHalf(ListNode *head) {
            ListNode *f, *s;
            f = s = head;
            while (f->next && f->next->next) {
                f = f->next->next;
                s = s->next;
            }
            return s;
        }
        
        ListNode* reverseList(ListNode *head) {
            ListNode *prev = nullptr;
            ListNode *curr = head;
            while (curr) {
                ListNode *tmpNext = curr->next;
                curr->next = prev;
                prev = curr;
                curr = tmpNext;
            }
            return prev;
        }
    };

1. 用快慢指標找到前半段的結尾。
2. 將後半段反轉。
3. 逐一比對。
4. 恢復反轉。
5. 返回結果。