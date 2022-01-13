---
layout: post
title:  "[LeetCode September Challange]Day8-Sum of Root To Leaf Binary Numbers"
date:   2020-09-08 00:00:00 +0800
categories: LeetCode
tags: [Tree, Depth-First-Search, Binary Tree, C++]
---
Given a binary tree, each node has value **<font color="red">0</font>** or **<font color="red">1</font>**.  Each root-to-leaf path represents a binary number starting with the most significant bit.  For example, if the path is **<font color="red">0 -> 1 -> 1 -> 0 -> 1</font>**, then this could represent **<font color="red">01101</font>** in binary, which is **<font color="red">13</font>**.  

For all leaves in the tree, consider the numbers represented by the path from the root to that leaf.  

Return the sum of these numbers.  

# Example 1:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/sum-of-root-to-leaf-binary-numbers-example.png?raw=true)

	Input: [1,0,1,0,1,0,1]
	Output: 22
	Explanation: (100) + (101) + (110) + (111) = 4 + 5 + 6 + 7 = 22

# Note:  
1. The number of nodes in the tree is between **<font color="red">1</font>** and **<font color="red">1000</font>**.
2. node.val is **<font color="red">0</font>** or **<font color="red">1</font>**.
3. The answer will not exceed **<font color="red">2^31 - 1</font>**.

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
	 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
	 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
	 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
	 * };
	 */
	class Solution {
	public:
	    int sumRootToLeaf(TreeNode* root) {
	        res = 0;
	        if (root) preorder(root, 0);
	        return res;
	    }
	private:
	    int res;
	    void preorder(TreeNode* node, int num) {
	        num = (num<<1) + node->val;
	        if (!node->left && !node->right)
	            res += num;
	        if (node->left) preorder(node->left, num);
	        if (node->right) preorder(node->right, num);
	    }
	};