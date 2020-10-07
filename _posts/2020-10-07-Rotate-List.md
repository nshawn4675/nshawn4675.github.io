---
layout: post
title:  "[LeetCode October Challange] Day 7 - Rotate List"
date:   2020-10-07 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Linked List, Two Pointers, Amazon, Bloomberg, Adobe]
---
Given a linked list, rotate the list to the right by *k* places, where *k* is non-negative.  

# Example 1:  
	Input: 1->2->3->4->5->NULL, k = 2
	Output: 4->5->1->2->3->NULL
	Explanation:
	rotate 1 steps to the right: 5->1->2->3->4->NULL
	rotate 2 steps to the right: 4->5->1->2->3->NULL

# Example 2:  
	Input: 0->1->2->NULL, k = 4
	Output: 2->0->1->NULL
	Explanation:
	rotate 1 steps to the right: 2->0->1->NULL
	rotate 2 steps to the right: 1->2->0->NULL
	rotate 3 steps to the right: 0->1->2->NULL
	rotate 4 steps to the right: 2->0->1->NULL

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
	    ListNode* rotateRight(ListNode* head, int k) {
	        if (!head) return nullptr;
	        else if (!head->next) return head;
	        
	        // find connect point & count len
	        ListNode* old_tail = head;
	        int len = 1;
	        for (;old_tail->next; old_tail=old_tail->next)
	            ++len;
	        old_tail->next = head;
	        
	        // find new tail, avoid dulplicate operation by mod operator.
	        ListNode* new_tail = head;
	        for (int i=1; i<len-k%len; ++i)
	            new_tail = new_tail->next;
	        head = new_tail->next;

	        new_tail->next = nullptr;
	        return head;
	    }
	};