---
layout: post
title:  "[LeetCode November Challange] Day 1 - Convert Binary Number in a Linked List to Integer"
date:   2020-11-01 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Linked List, Bit Manipulation, Mathworks, Cisco, Citrix]
---
Given <font color="red">head</font> which is a reference node to a singly-linked list. The value of each node in the linked list is either 0 or 1. The linked list holds the binary representation of a number.  

Return the *decimal value* of the number in the linked list.  

# Example 1:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1290_ex1.png?raw=true)

	Input: head = [1,0,1]
	Output: 5
	Explanation: (101) in base 2 = (5) in base 10

# Example 2:  
	Input: head = [0]
	Output: 0

#Example 3:  
	Input: head = [1]
	Output: 1

# Example 4:  
	Input: head = [1,0,0,1,0,0,1,1,1,0,0,0,0,0,0]
	Output: 18880

# Example 5:  
	Input: head = [0,0]
	Output: 0

# Constraints:  
- The Linked List is not empty.
- Number of nodes will not exceed <font color="red">30</font>.
- Each node's value is either <font color="red">0</font> or <font color="red">1</font>.

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
	    int getDecimalValue(ListNode* head) {
	        int ans = 0;
	        while(head)
	        {
	            ans <<= 1;
	            ans |= head->val;
	            head = head->next;
	        }
	        return ans;
	    }
	};