---
layout: post
title:  "[LeetCode February Challange] Day 10 - Copy List with Random Pointer"
date:   2021-02-10 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Hash Table, Linked List, Amazon, Facebook, Bloomberg, Microsoft, Oracle, eBay, Yahoo, Qualtrics]
---
A linked list of length <font color="red">n</font> is given such that each node contains an additional random pointer, which could point to any node in the list, or <font color="red">null</font>.

Construct a [deep copy](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) of the list. The deep copy should consist of exactly <font color="red">n</font> **brand new** nodes, where each new node has its value set to the value of its corresponding original node. Both the <font color="red">next</font> and <font color="red">random</font> pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. **None of the pointers in the new list should point to nodes in the original list**.

For example, if there are two nodes <font color="red">X</font> and <font color="red">Y</font> in the original list, where <font color="red">X.random --> Y</font>, then for the corresponding two nodes <font color="red">x</font> and <font color="red">y</font> in the copied list, <font color="red">x.random --> y</font>.

Return *the head of the copied linked list*.

The linked list is represented in the input/output as a list of <font color="red">n</font> nodes. Each node is represented as a pair of <font color="red">[val, random_index]</font> where:

- **<font color="red">val</font>**: an integer representing <font color="red">Node.val</font>
- **<font color="red">random_index</font>**: the index of the node (range from <font color="red">0</font> to <font color="red">n-1</font>) that the <font color="red">random</font> pointer points to, or <font color="red">null</font> if it does not point to any node.
Your code will **only** be given the <font color="red">head</font> of the original linked list.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/138_ex1.png?raw=true)

	Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
	Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/138_ex2.png?raw=true)

	Input: head = [[1,1],[2,1]]
	Output: [[1,1],[2,1]]

# Example 3:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/138_ex3.png?raw=true)

	Input: head = [[3,null],[3,0],[3,null]]
	Output: [[3,null],[3,0],[3,null]]

# Example 4:

	Input: head = []
	Output: []
	Explanation: The given linked list is empty (null pointer), so return null.

# Constraints:

- <font color="red">0 <= n <= 1000</font>
- <font color="red">-10000 <= Node.val <= 10000</font>
- **<font color="red">Node.random</font>** is <font color="red">null</font> or is pointing to some node in the linked list.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	/*
	// Definition for a Node.
	class Node {
	public:
	    int val;
	    Node* next;
	    Node* random;
	    
	    Node(int _val) {
	        val = _val;
	        next = NULL;
	        random = NULL;
	    }
	};
	*/

	class Solution {
	public:
	    Node* copyRandomList(Node* head) {
	        unordered_map<Node*, Node*> m;
	        for (Node* cur = head; cur != nullptr; cur = cur->next) {
	            m[cur] = new Node(cur->val);
	        }
	        for (Node* cur = head; cur != nullptr; cur = cur->next) {
	            m[cur]->next = m[cur->next];
	            m[cur]->random = m[cur->random];
	        }
	        return m[head];
	    }
	};

利用 hash table，先針對各 node 做出一個分身。  
再 loop 一遍，針對各分身 node 的 next、 random 指向進行處理。