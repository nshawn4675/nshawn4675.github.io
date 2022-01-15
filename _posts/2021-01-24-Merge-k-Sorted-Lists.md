---
layout: post
title: "[LeetCode January Challange] Day 24 - Merge k Sorted Lists"
date: 2021-01-24 00:00:00 +0800
categories: LeetCode
tags: [Hard, Linked List, Divide and Conquer, Heap (Priority Queue), Merge Sort, Amazon, Facebook, Bloomberg, Databricks, Microsoft, Oracle, Apple, ByteDance, Google, Uber, Adobe, Twitter, Wish, Palantir Technologies, Tesla, C++]
---
You are given an array of <font color="red">k</font> linked-lists <font color="red">lists</font>, each linked-list is sorted in ascending order.

*Merge all the linked-lists into one sorted linked-list and return it.*

# Example 1:

	Input: lists = [[1,4,5],[1,3,4],[2,6]]
	Output: [1,1,2,3,4,4,5,6]
	Explanation: The linked-lists are:
	[
	  1->4->5,
	  1->3->4,
	  2->6
	]
	merging them into one sorted list:
	1->1->2->3->4->4->5->6

# Example 2:

	Input: lists = []
	Output: []

# Example 3:

	Input: lists = [[]]
	Output: []

# Constraints:

- <font color="red">k == lists.length</font>
- <font color="red">0 <= k <= 10^4</font>
- <font color="red">0 <= lists[i].length <= 500</font>
- <font color="red">-10^4 <= lists[i][j] <= 10^4</font>
- **<font color="red">lists[i]</font>** is sorted in **ascending order**.
- The sum of <font color="red">lists[i].length</font> won't exceed <font color="red">10^4</font>.

______________________  

# Solution  

# Compare one by one

Time complexity : O(n x k) (k = # nodes)  
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
	    ListNode* mergeKLists(vector<ListNode*>& lists) {
	        int n = lists.size();
	        ListNode* dummy_head = new ListNode();
	        ListNode* cur = dummy_head;
	        
	        ListNode** candidate;
	        do {
	            candidate = nullptr;
	            for (int i=0; i<n; ++i) {
	                if (lists[i] == nullptr) continue;
	                else if (candidate == nullptr || lists[i]->val < (*candidate)->val)
	                    candidate = &lists[i];
	            }
	            if (candidate != nullptr) {
	                cur->next = new ListNode((*candidate)->val);
	                cur = cur->next;
	                *candidate = (*candidate)->next;
	            }
	        } while (candidate != nullptr);
	        
	        return dummy_head->next;
	    }
	};


一直比較各個 list 的第一個元素，取最小者。


# Merge List One by One

Time complexity : O(n x k)  
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
	    ListNode* mergeKLists(vector<ListNode*>& lists) {
	        if (lists.size() == 0) return nullptr;
	        while (1 < lists.size()) {
	            lists.push_back(merge2List(lists[0], lists[1]));
	            lists.erase(lists.begin());
	            lists.erase(lists.begin());
	        }
	        return lists[0];
	    }
	private:
	    ListNode* merge2List(ListNode* l1, ListNode* l2) {
	        if (nullptr == l1)
	            return l2;
	        else if (nullptr == l2)
	            return l1;
	        else if (l1->val <= l2->val) {
	            l1->next = merge2List(l1->next, l2);
	            return l1;
	        } else {
	            l2->next = merge2List(l2->next, l1);
	            return l2;
	        }
	    }
	};

# Merge with Divide And Conquer

Time complexity : O(n x logk)
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
	    ListNode *mergeTwoLists(ListNode* l1, ListNode* l2) {
	        if (NULL == l1) return l2;
	        else if (NULL == l2) return l1;
	        if (l1->val <= l2->val) {
	            l1->next = mergeTwoLists(l1->next, l2);
	            return l1;
	        }
	        else {
	            l2->next = mergeTwoLists(l1, l2->next);
	            return l2;
	        }
	    }
	    ListNode *mergeKLists(vector<ListNode *> &lists) {
	        if (lists.empty()) return NULL;
	        int len = lists.size();
	        while (len > 1) {
	            for (int i = 0; i < len / 2; ++i) {
	                lists[i] = mergeTwoLists(lists[i], lists[len - 1 - i]);
	            }
	            len = (len + 1) / 2;
	        }
	        
	        return lists.front();
	    }
	};