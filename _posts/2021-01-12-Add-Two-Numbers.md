---
layout: post
title: "[LeetCode January Challange] Day 12 - Add Two Numbers"
date: 2021-01-12 00:00:00 +0800
categories: LeetCode
tags: [Medium, Linked List, Math, Recursion, Amazon, Bloomberg, Microsoft, Adobe, Apple, Google, Facebook, Uber, Yahoo, Coupang, VMware, Walmart Labs, Paypal, Docusign, C++]
---
You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/2_ex.jpg?raw=true)

	Input: l1 = [2,4,3], l2 = [5,6,4]
	Output: [7,0,8]
	Explanation: 342 + 465 = 807.

# Example 2:

	Input: l1 = [0], l2 = [0]
	Output: [0]

# Example 3:

	Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
	Output: [8,9,9,9,0,0,0,1]

# Constraints:

- The number of nodes in each linked list is in the range <font color="red">[1, 100]</font>.
- <font color="red">0 <= Node.val <= 9</font>
- It is guaranteed that the list represents a number that does not have leading zeros.

______________________  

# Solution  

Time complexity : O(max(l1+l2))  
Space complexity : O(max(l1+l2))  

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
	    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
	        ListNode* dummy = new ListNode();
	        ListNode* cur = dummy;
	        short carry = 0;
	        while (l1 || l2 || carry) {
	            short a = l1 ? l1->val : 0;
	            short b = l2 ? l2->val : 0;
	            short val = a + b + carry;
	            carry = val / 10;
	            cur->next = new ListNode(val%10);
	            cur = cur->next;
	            l1 = l1 ? l1->next : nullptr;
	            l2 = l2 ? l2->next : nullptr;
	        }
	        
	        return dummy->next;
	    }
	};