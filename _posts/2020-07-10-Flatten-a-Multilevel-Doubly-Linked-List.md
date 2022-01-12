---
layout: post
title:  "[LeetCode July Challange]Day10-Flatten a Multilevel Doubly Linked List"
date:   2020-07-10 00:00:00 +0800
categories: LeetCode
tags: [Linked List, Depth-First-Search, Doubly-Linked List, C++]
---
You are given a doubly linked list which in addition to the next and previous pointers, it could have a child pointer, which may or may not point to a separate doubly linked list. These child lists may have one or more children of their own, and so on, to produce a multilevel data structure, as shown in the example below.  

Flatten the list so that all the nodes appear in a single-level, doubly linked list. You are given the head of the first level of the list.  

# Example 1:  
	Input: head = [1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]
	Output: [1,2,3,7,8,11,12,9,10,4,5,6]
	Explanation:

	The multilevel linked list in the input is as follows:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/multilevellinkedlist.png?raw=true)

	After flattening the multilevel linked list it becomes:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/multilevellinkedlistflattened.png?raw=true)

# Example 2:  
	Input: head = [1,2,null,3]
	Output: [1,3,2]
	Explanation:

	The input multilevel linked list is as follows:

	  1---2---NULL
	  |
	  3---NULL

# Example 3:  
	Input: head = []
	Output: []

# How multilevel linked list is represented in test case:  

We use the multilevel linked list from **Example 1** above:  

	 1---2---3---4---5---6--NULL
	         |
	         7---8---9---10--NULL
	             |
	             11--12--NULL

The serialization of each level is as follows:  

	[1,2,3,4,5,6,null]
	[7,8,9,10,null]
	[11,12,null]

To serialize all levels together we will add nulls in each level to signify no node connects to the upper node of the previous level. The serialization becomes:  

	[1,2,3,4,5,6,null]
	[null,null,7,8,9,10,null]
	[null,11,12,null]

Merging the serialization of each level and removing trailing nulls we obtain:  

	[1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]

# Constraints :  

- Number of Nodes will not exceed 1000.
- **1 <= Node.val <= 10^5**

______________________  

# solution
time complexity : O(n)  
space complexity : O(1)  

	/*
	// Definition for a Node.
	class Node {
	public:
	    int val;
	    Node* prev;
	    Node* next;
	    Node* child;
	};
	*/

	class Solution {
	public:
	    Node* flatten(Node* head) {
	        if (!head) return nullptr;
	        head->prev = nullptr;
	        
	        stack<Node*> preLv;
	        for (Node* i = head; i!=nullptr; i=i->next) {
	            if (i->child) {
	                // go to next level
	                preLv.push(i->next);
	                i->child->prev = i;
	                i->next = i->child;
	                i->child = nullptr;
	            } else if (i->next==nullptr && !preLv.empty()) {
	                // reach end, back to prev level.
	                i->next = preLv.top();
	                preLv.pop();
	                if (i->next) i->next->prev = i;
	            }
	        }
	        
	        return head;
	    }
	};

用一個指標從頭跑到尾，用一個stack存放該返回的node。  
思考「往下一層」與「返回上一層」的處理。  