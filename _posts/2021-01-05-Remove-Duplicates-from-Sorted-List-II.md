---
layout: post
title: "[LeetCode January Challange] Day 5 - Remove Duplicates from Sorted List II"
date: 2021-01-05 00:00:00 +0800
categories: LeetCode
tags: [Medium, Linked List, Two Pointers, Amazon, C++]
---
Given the <font color="red">head</font> of a sorted linked list, *delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.* Return *the linked list **sorted** as well.*

# Example 1:
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/82_ex1.jpg?raw=true)

	Input: head = [1,2,3,3,4,4,5]
	Output: [1,2,5]

# Example 2:
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/82_ex2.jpg?raw=true)

	Input: head = [1,1,1,2,3]
	Output: [2,3]

# Constraints:

- The number of nodes in the list is in the range <font color="red">[0, 300]</font>.
- <font color="red">-100 <= Node.val <= 100</font>
- The list is guaranteed to be **sorted** in ascending order.

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
	    ListNode* deleteDuplicates(ListNode* head) {
	        ListNode* dummy_head = new ListNode(0, head);
	        ListNode* prev = dummy_head;
	        
	        while (head) {
	            if (head->next && head->val == head->next->val) {
	                ListNode* del_start = head;
	                while (head->next && head->val == head->next->val)
	                    head = head->next;
	                ListNode* del_end = head->next;
	                
	                prev->next = head->next;
	                head = prev;
	                
	                while (del_start != del_end) {
	                    ListNode *tmp = del_start;
	                    del_start = del_start->next;
	                    delete tmp;
	                }
	            } else
	                prev = prev->next;
	            
	            head = head->next;
	        }
	        
	        return dummy_head->next;
	    }
	};

邊走邊找目標 node (重覆值出現的node)，找到時記錄其起末位置，供後續刪除用。  
一旦找到目標 node ，就一直往下走，直到不是目標 node 為止。  
將 prev 與結束位置相連，中間都是要刪掉的。