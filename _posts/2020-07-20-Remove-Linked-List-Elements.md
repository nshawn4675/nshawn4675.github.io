---
layout: post
title:  "[LeetCode July Challange]Day20-Remove Linked List Elements"
date:   2020-07-20 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Remove all elements from a linked list of integers that have value **val**.

# Example:  
	Input:  1->2->6->3->4->5->6, val = 6
	Output: 1->2->3->4->5

______________________  

# solution
time complexity : O(n)  
space complexity : O(1)

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
	    ListNode* removeElements(ListNode* head, int val) {
	        ListNode dummyHead, *pre, *cur;
	        dummyHead.next = head;
	        cur = head;
	        pre = &dummyHead;
	        
	        while (cur) {
	            if (cur->val == val) {
	                pre->next = cur->next;
	                delete cur;
	                cur = pre->next;
	            } else {
	                pre = cur;
	                cur = cur->next;
	            }
	        }
	        
	        return dummyHead.next;
	    }
	};

從頭一個一個往尾巴檢查。  
若有找到需要移除的node，則進行以下動作：  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/linklistremove.png?raw=true)  
若該node是不需要移除的，直接跳下一個。  