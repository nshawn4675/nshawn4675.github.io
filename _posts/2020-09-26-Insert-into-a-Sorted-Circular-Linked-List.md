---
layout: post
title:  "Insert into a Sorted Circular Linked List"
date:   2020-09-26 00:00:00 +0800
categories: LeetCode
tags: [Medium, Linked List, Facebook, Quip (Saleforce), C++]
---
Given a node from a **Circular Linked List** which is sorted in ascending order, write a function to insert a value <font color="red">insertVal</font> into the list such that it remains a sorted circular list. The given node can be a reference to any single node in the list, and may not be necessarily the smallest value in the circular list.  

If there are multiple suitable places for insertion, you may choose any place to insert the new value. After the insertion, the circular list should remain sorted.  

If the list is empty (i.e., given node is <font color="red">null</font>), you should create a new single circular list and return the reference to that single node. Otherwise, you should return the original given node.  

# Example 1:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/708_ex1.jpg?raw=true)

	Input: head = [3,4,1], insertVal = 2
	Output: [3,4,1,2]
	Explanation: In the figure above, there is a sorted circular list of three elements. You are given a reference to the node with value 3, and we need to insert 2 into the list. The new node should be inserted between node 1 and node 3. After the insertion, the list should look like this, and we should still return node 3.

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/708_ex2.jpg?raw=true)


# Example 2:  
	Input: head = [], insertVal = 1
	Output: [1]
	Explanation: The list is empty (given head is null). We create a new single circular list and return the reference to that single node.

# Example 3:  
	Input: head = [1], insertVal = 0
	Output: [1,0]

# Constraints:  
- <font color="red">0 <= Number of Nodes <= 5 * 10^4</font>
- <font color="red">-10^6 <= Node.val <= 10^6</font>
- <font color="red">-10^6 <= insertVal <= 10^6</font>

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)  

	/*
	// Definition for a Node.
	class Node {
	public:
	    int val;
	    Node* next;

	    Node() {}

	    Node(int _val) {
	        val = _val;
	        next = NULL;
	    }

	    Node(int _val, Node* _next) {
	        val = _val;
	        next = _next;
	    }
	};
	*/

	class Solution {
	public:
	    Node* insert(Node* head, int insertVal) {
	        if (!head) {
	            head = new Node(insertVal);
	            head->next = head;
	            return head;
	        } 
	        
	        Node* pre = head;
	        Node* cur = head->next;
	        bool insert_here = false;
	        do {
	            if ((pre->val <= insertVal && insertVal <= cur->val) ||
	                (pre->val > cur->val && pre->val < insertVal) ||
	                (pre->val > cur->val && insertVal < cur->val))
	            {
	                pre->next = new Node(insertVal, cur);
	                return head;
	            }
	            
	            pre = cur;
	            cur = cur->next;
	        } while (pre != head);
	        
	        pre->next = new Node(insertVal, cur);
	        return head;
	    }
	};

從頭繞一圈，會遇到以下可以插入的位置：  
1. pre->val <= insertVal && insertVal <= cur->val：要插入的數字不大不小，插在中間。
2. pre->val > cur->val && pre->val < insertVal：要插入的數字為所有中最大的，要插在head與tail之間。
3. pre->val > cur->val && insertVal < cur->val：要插入的數字為所有中最小的，要插在head與tail之間。

若已經繞完一圈了，還找不到插入點，代表可能原先所有的數字都是一樣的，就隨便找個地方插入即可。