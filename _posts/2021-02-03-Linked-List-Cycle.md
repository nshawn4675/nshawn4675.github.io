---
layout: post
title:  "[LeetCode February Challange] Day 3 - Linked List Cycle"
date:   2021-02-03 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Linked List, Two Pointers, Microsoft, Amazon, Facebook, Goldman Sachs, Apple, Google, Tesla]
---
Given <font color="red">head</font>, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the <font color="red">next</font> pointer. Internally, <font color="red">pos</font> is used to denote the index of the node that tail's <font color="red">next</font> pointer is connected to. **Note that** <font color="red">pos</font> **is not passed as a parameter**.

Return <font color="red">true</font> *if there is a cycle in the linked list*. Otherwise, return <font color="red">false</font>.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/141_ex1.png?raw=true)

	Input: head = [3,2,0,-4], pos = 1
	Output: true
	Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/141_ex2.png?raw=true)

	Input: head = [1,2], pos = 0
	Output: true
	Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.

# Example 3:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/141_ex3.png?raw=true)

	Input: head = [1], pos = -1
	Output: false
	Explanation: There is no cycle in the linked list.

# Constraints:

- The number of the nodes in the list is in the range <font color="red">[0, 10^4]</font>.
- <font color="red">-10^5 <= Node.val <= 10^5</font>
- **<font color="red">pos</font>** is <font color="red">-1</font> or a **valid index** in the linked-list.
 

**Follow up:** Can you solve it using <font color="red">O(1)</font> (i.e. constant) memory?

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

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
	    bool hasCycle(ListNode *head) {
	        if (head == nullptr) return false;
	        
	        ListNode *slow, *fast;
	        slow = head;
	        fast = head->next;
	        while (slow != fast) {
	            if (fast == nullptr || fast->next == nullptr)
	                return false;
	            fast = fast->next->next;
	            slow = slow->next;
	        }
	        
	        return true;
	    }
	};

使用快慢指標，來判斷該 linked list 是否有迴圈。  
若有的話，快指標會在迴圈中追上慢指標。  

Floyd's Cycle Finding Algorithm