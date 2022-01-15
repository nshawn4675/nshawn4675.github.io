---
layout: post
title: "[LeetCode February Challange] Day 2 - Trim a Binary Search Tree"
date: 2021-02-02 00:00:00 +0800
categories: LeetCode
tags: [Medium, Tree, Depth-First Search, Binary Search Tree, Binary Tree, Samsung, C++]
---
Given the <font color="red">root</font> of a binary search tree and the lowest and highest boundaries as <font color="red">low</font> and <font color="red">high</font>, trim the tree so that all its elements lies in <font color="red">[low, high]</font>. Trimming the tree should **not** change the relative structure of the elements that will remain in the tree (i.e., any node's descendant should remain a descendant). It can be proven that there is a **unique answer**.

Return *the root of the trimmed binary search tree*. Note that the root may change depending on the given bounds.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/669_ex1.jpg?raw=true)

	Input: root = [1,0,2], low = 1, high = 2
	Output: [1,null,2]

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/669_ex2.jpg?raw=true)

	Input: root = [3,0,4,null,2,null,null,1], low = 1, high = 3
	Output: [3,2,null,1]

# Example 3:

	Input: root = [1], low = 1, high = 2
	Output: [1]

# Example 4:

	Input: root = [1,null,2], low = 1, high = 3
	Output: [1,null,2]

# Example 5:

	Input: root = [1,null,2], low = 2, high = 4
	Output: [2]

# Constraints:

- The number of nodes in the tree in the range <font color="red">[1, 10^4]</font>.
- <font color="red">0 <= Node.val <= 10^4</font>
- The value of each node in the tree is **unique**.
- **<font color="red">root</font>** is guaranteed to be a valid binary search tree.
- <font color="red">0 <= low <= high <= 10^4</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	/**
	 * Definition for a binary tree node.
	 * struct TreeNode {
	 *     int val;
	 *     TreeNode *left;
	 *     TreeNode *right;
	 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
	 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
	 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
	 * };
	 */
	class Solution {
	public:
	    TreeNode* trimBST(TreeNode* root, int low, int high) {
	        if (root == nullptr) return nullptr;
	        if (root->val < low) return trimBST(root->right, low, high);
	        if (high < root->val) return trimBST(root->left, low, high);
	        
	        root->left = trimBST(root->left, low, high);
	        root->right = trimBST(root->right, low, high);
	        return root;
	    }
	};