---
layout: post
title: "[LeetCode December Challange] Day 2 - Linked List Random Node"
date: 2020-12-02 00:00:00 +0800
categories: LeetCode
tags: [Medium, Linked List, Math, Reservoir Sampling, Randomized, Amazon, C++]
---

Given a singly linked list, return a random node's value from the linked list. Each node must have the **same probability** of being chosen.

# Follow up:

What if the linked list is extremely large and its length is unknown to you? Could you solve this efficiently without using extra space?

# Example:

    // Init a singly linked list [1,2,3].
    ListNode head = new ListNode(1);
    head.next = new ListNode(2);
    head.next.next = new ListNode(3);
    Solution solution = new Solution(head);

    // getRandom() should return either 1, 2, or 3 randomly. Each element should have equal probability of returning.
    solution.getRandom();

---

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
        /** @param head The linked list's head.
            Note that the head is guaranteed to be not null, so it contains at least one node. */
        Solution(ListNode* head) {
            h = head;
        }

        /** Returns a random node's value. */
        int getRandom() {
            int ans = INT_MIN;
            int acc = 0; // accumulate
            for (ListNode* cur = h; cur != nullptr; cur=cur->next) {
                float p = (float)rand() / (float)RAND_MAX;
                if (p < (1.0/(float)++acc))
                    ans = cur->val;
            }
            return ans;
        }
    private:
        ListNode* h;
    };

    /**
    * Your Solution object will be instantiated and called as such:
    * Solution* obj = new Solution(head);
    * int param_1 = obj->getRandom();
    */

在一個大小未知的群體中平均取樣，在此用的是 Reservoir Sampling 演算法，其做法為：

1. 遍歷群體中每個元素。
2. 隨機取一機率值，若其機率落於(1/第 i 個)\*100%內，則用第 i 個取代目前手上的。
3. 全部遍歷完後，最後的還在手上的，即為所選。

其原理為：

    若只看最後取到第一個的機率，
    1 hit * 2 miss * 3 miss * 4 miss * ... * n miss
    等於
    1 * (1 - 1/i) * (1 - 1/i+1) * (1 - 1/i+2) * ... * (1 - 1/n)
    等於
    1 * (i-1/i) * (i/i+1) * (i+1/i+2) * ... * (n-1/n)
    上下約掉後最後等於
    1/n

故遍歷完整個群體，各個元素被取到的機率皆為 1/n。
