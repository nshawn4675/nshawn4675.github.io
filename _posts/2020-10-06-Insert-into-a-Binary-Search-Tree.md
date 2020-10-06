---
layout: post
title:  "[LeetCode October Challange] Day 6 - Insert into a Binary Search Tree"
date:   2020-10-06 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Tree, Amazon, Microsoft]
---
You are given the <font color="red">root</font> node of a binary search tree (BST) and a <font color="red">value</font> to insert into the tree. Return *the root node of the BST after the insertion*. It is **guaranteed** that the new value does not exist in the original BST.  

**Notice** that there may exist multiple valid ways for the insertion, as long as the tree remains a BST after insertion. You can return **any of them**.  

# Example 1:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/701_ex1.jpg?raw=true)

	Input: root = [4,2,7,1,3], val = 5
	Output: [4,2,7,1,3,5]
	Explanation: Another accepted tree is:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/701ex1_2.jpg?raw=true)

# Example 2:  
	Input: root = [40,20,60,10,30,50,70], val = 25
	Output: [40,20,60,10,30,50,70,null,null,25]

# Example 3:  
	Input: root = [4,2,7,1,3,null,null,null,null,null,null], val = 5
	Output: [4,2,7,1,3,5]

# Constraints:  
- The number of nodes in the tree will be in the range <font color="red">[0, 10^4]</font>.
- <font color="red">-108 <= Node.val <= 108</font>
- All the values <font color="red">Node.val</font> are **unique**.
- <font color="red">-108 <= val <= 108</font>
- It's **guaranteed** that <font color="red">val</font> does not exist in the original BST.

______________________  

# Solution

Time complexity : O(h)  
Space complexity : O(1)  

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
	    TreeNode* insertIntoBST(TreeNode* root, int val) {
	        if (!root) return new TreeNode(val);
	        
	        TreeNode* cur = root;
	        while (true) {
	            if (cur->left && val < cur->val)
	                cur = cur->left;
	            else if (cur->right && cur->val < val)
	                cur = cur->right;
	            else break;
	        }
	        
	        if (val < cur->val)
	            cur->left = new TreeNode(val);
	        else cur->right = new TreeNode(val);
	        
	        return root;
	    }
	};

先traverse到合適的位置，再新增該Node。