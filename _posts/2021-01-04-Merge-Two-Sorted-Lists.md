---
layout: post
title: "[LeetCode January Challange] Day 4 - Merge Two Sorted Lists"
date: 2021-01-04 00:00:00 +0800
categories: LeetCode
tags: [Easy, Linked List, Recursion, Amazon, Adobe, Capital One, Google, Facebook, Bloomberg, Oracle, Apple, Microsoft, IBM, Uber, C++]
---
Merge two sorted linked lists and return it as a **sorted** list. The list should be made by splicing together the nodes of the first two lists.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/21_ex1.jpg?raw=true)

	Input: l1 = [1,2,4], l2 = [1,3,4]
	Output: [1,1,2,3,4,4]

# Example 2:

	Input: l1 = [], l2 = []
	Output: []

# Example 3:

	Input: l1 = [], l2 = [0]
	Output: [0]

# Constraints:

- The number of nodes in both lists is in the range <font color="red">[0, 50]</font>.
- <font color="red">-100 <= Node.val <= 100</font>
- Both <font color="red">l1</font> and <font color="red">l2</font> are sorted in **non-decreasing** order.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

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
	    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
	        ListNode* dummy = new ListNode();
	        ListNode* cur = dummy;
	        
	        while (l1 && l2) {
	            if (l1->val < l2->val)
	                append_node(&cur, &l1);
	            else
	                append_node(&cur, &l2);
	        }
	        
	        while (l1) append_node(&cur, &l1);
	        while (l2) append_node(&cur, &l2);
	        
	        return dummy->next;
	    }
	    
	    void append_node(ListNode** cur, ListNode** node) {
	        (*cur)->next = new ListNode((*node)->val);
	        *cur = (*cur)->next;
	        *node = (*node)->next;
	    }
	};

當 l1、l2 都還有東西時，互相比較，取小者。

當l1或是l2其中一方跑完，則取另一方所剩。