---
layout: post
title:  "[LeetCode January Challange] Day 2 - Find a Corresponding Node of a Binary Tree in a Clone of That Tree"
date:   2021-01-02 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Tree, Depth-first Search, Breadth-first Search, Recursion, Facebook]
---
Given two binary trees <font color="red">original</font> and <font color="red">cloned</font> and given a reference to a node <font color="red">target</font> in the original tree.

The <font color="red">cloned</font> tree is a **copy of** the <font color="red">original</font> tree.

Return *a reference to the same node* in the <font color="red">cloned</font> tree.

**Note** that you are **not allowed** to change any of the two trees or the <font color="red">target</font> node and the answer **must be** a reference to a node in the <font color="red">cloned</font> tree.

**Follow up:** Solve the problem if repeated values on the tree are allowed.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1379_ex1.png?raw=true)

	Input: tree = [7,4,3,null,null,6,19], target = 3
	Output: 3
	Explanation: In all examples the original and cloned trees are shown. The target node is a green node from the original tree. The answer is the yellow node from the cloned tree.

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1379_ex2.png?raw=true)

	Input: tree = [7], target =  7
	Output: 7

# Example 3:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1379_ex3.png?raw=true)

	Input: tree = [8,null,6,null,5,null,4,null,3,null,2,null,1], target = 4
	Output: 4

# Example 4:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1379_ex4.png?raw=true)

	Input: tree = [1,2,3,4,5,6,7,8,9,10], target = 5
	Output: 5

# Example 5:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1379_ex5.png?raw=true)

	Input: tree = [1,2,null,3], target = 2
	Output: 2

# Constraints:

- The number of nodes in the <font color="red">tree</font> is in the range <font color="red">[1, 10^4]</font>.
- The values of the nodes of the <font color="red">tree</font> are unique.
- **<font color="red">target</font>** node is a node from the <font color="red">original</font> tree and is not <font color="red">null</font>.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(h)  

	/**
	 * Definition for a binary tree node.
	 * struct TreeNode {
	 *     int val;
	 *     TreeNode *left;
	 *     TreeNode *right;
	 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
	 * };
	 */

	class Solution {
	public:
	    TreeNode* getTargetCopy(TreeNode* original, TreeNode* cloned, TreeNode* target) {
	        if (original == target) return cloned;
	        
	        if (!original) return nullptr;
	        if (TreeNode* left = getTargetCopy(original->left, cloned->left, target))
	            return left;
	        return getTargetCopy(original->right, cloned->right, target);
	    }
	};

使用DFS，兩邊同時移動，origin 找到的同時，clone 端即是所求。