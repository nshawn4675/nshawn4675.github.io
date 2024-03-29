---
layout: post
title:  "[LeetCode November Challange] Day 2 - Insertion Sort List"
date:   2020-11-02 00:00:00 +0800
categories: LeetCode
tags: [Medium, Linked List, Sorting, Microsoft, Bloomberg, C++]
---
Sort a linked list using insertion sort.  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/147_ex.gif?raw=true)

A graphical example of insertion sort. The partial sorted list (black) initially contains only the first element in the list.  
With each iteration one element (red) is removed from the input data and inserted in-place into the sorted list  

# Algorithm of Insertion Sort:  
1. Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list.
2. At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there.
3. It repeats until no input elements remain.

# Example 1:  
	Input: 4->2->1->3
	Output: 1->2->3->4

# Example 2:  
	Input: -1->5->3->4->0
	Output: -1->0->3->4->5

______________________  

# Solution  

Time complexity : O(n^2)  
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
	    ListNode* insertionSortList(ListNode* head) {
	        ListNode* dummy = new ListNode();
	        while (head) {
	            ListNode *preNode=dummy, *nextNode=dummy->next;
	            while (nextNode && nextNode->val < head->val) {
	                preNode = nextNode;
	                nextNode = nextNode->next;
	            }
	            
	            ListNode* next_iter = head->next;
	            preNode->next = head;
	            head->next = nextNode;
	            head = next_iter;
	        }
	        return dummy->next;
	    }
	};