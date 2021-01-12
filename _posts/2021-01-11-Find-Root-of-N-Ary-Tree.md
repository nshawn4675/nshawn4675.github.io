---
layout: post
title:  "Find Root of N-Ary Tree"
date:   2021-01-11 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Google]
---
You are given all the nodes of an [N-ary tree](https://leetcode.com/articles/introduction-to-n-ary-trees/) as an array of <font color="red">Node</font> objects, where each node has a **unique value**.

Return the ***root** of the N-ary tree.*

**Custom testing:**

An N-ary tree can be serialized as represented in its level order traversal where each group of children is separated by the <font color="red">null</font> value (see examples).

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1506_ex1.png?raw=true)

For example, the above tree is serialized as  
<font color="red">[1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]</font>.

The testing will be done in the following way:

1. The **input data** should be provided as a serialization of the tree.
2. The driver code will construct the tree from the serialized input data and put each <font color="red">Node</font> object into an array **in an arbitrary order**.
3. The driver code will pass the array to <font color="red">findRoot</font>, and your function should find and return the root <font color="red">Node</font> object in the array.
4. The driver code will take the returned <font color="red">Node</font> object and serialize it. If the serialized value and the input data are the **same**, the test **passes**.
 

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1506_ex2.png?raw=true)

	Input: tree = [1,null,3,2,4,null,5,6]
	Output: [1,null,3,2,4,null,5,6]
	Explanation: The tree from the input data is shown above.
	The driver code creates the tree and gives findRoot the Node objects in an arbitrary order.
	For example, the passed array could be [Node(5),Node(4),Node(3),Node(6),Node(2),Node(1)] or [Node(2),Node(6),Node(1),Node(3),Node(5),Node(4)].
	The findRoot function should return the root Node(1), and the driver code will serialize it and compare with the input data.
	The input data and serialized Node(1) are the same, so the test passes.

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1506_ex3.png?raw=true)

	Input: tree = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
	Output: [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]

# Constraints:

- The total number of nodes is between <font color="red">[1, 5 * 10^4]</font>.
- Each node has a **unique** value.
 

# Follow up:

- Could you solve this problem in constant space complexity with a linear time algorithm?

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

	/*
	// Definition for a Node.
	class Node {
	public:
	    int val;
	    vector<Node*> children;

	    Node() {}

	    Node(int _val) {
	        val = _val;
	    }

	    Node(int _val, vector<Node*> _children) {
	        val = _val;
	        children = _children;
	    }
	};
	*/

	class Solution {
	public:
	    Node* findRoot(vector<Node*> tree) {
	        uint64_t res = 0;
	        for (Node* node: tree) {
	            res ^= (uint64_t)node;
	            for (Node* child: node->children)
	                res ^= (uint64_t)child;
	        }
	        return (Node*)res;
	    }
	};

一個思路是，只有 root 的 indegree 為0。  

另一個思路，即此解法，為拜訪所有 node 以及它的 child ，除了 root 只會被拜訪一次之外，其它的 node 皆被拜訪兩次。