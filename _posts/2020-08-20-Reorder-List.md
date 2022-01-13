---
layout: post
title:  "[LeetCode August Challange]Day20-Reorder List"
date:   2020-08-20 00:00:00 +0800
categories: LeetCode
tags: [Linked List, Two Pointers, Stack, Recursion, C++]
---
Given a singly linked list *L: L0→L1→…→Ln-1→Ln*,  
reorder it to: *L0→Ln→L1→Ln-1→L2→Ln-2*→…

You may **not** modify the values in the list's nodes, only nodes itself may be changed.

# Example 1:  
	Given 1->2->3->4, reorder it to 1->4->2->3.

# Example 2:  
	Given 1->2->3->4->5, reorder it to 1->5->2->4->3.

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
	    void reorderList(ListNode* head) {
	        if (!head) return;
	        
	        vector<ListNode*> vec;
	        for (ListNode* i=head; i!=nullptr; i=i->next)
	            vec.push_back(i);

	        int cur = 0;
	        for (int i=0, j=vec.size()-1; i<j;) {
	            if (cur == i) {
	                vec[i++]->next = vec[j];
	                cur = j;
	            } else {
	                vec[j--]->next = vec[i];
	                cur = i;
	            }
	        }
	        vec[cur]->next = nullptr;
	    }
	};

將list存入vector中，再利用雙指標的方式，一個從頭往後，一個從尾往前，慢慢重新建構出題目所需的答案。