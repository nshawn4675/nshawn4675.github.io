---
layout: post
title:  "[LeetCode August Challange]Day24-Sum of Left Leaves"
date:   2020-08-24 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Find the sum of all left leaves in a given binary tree.  

# Example:  
	    3
	   / \
	  9  20
	    /  \
	   15   7

	There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.

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
	    int sumOfLeftLeaves(TreeNode* root) {
	        sum_ = 0;
	        preTraversal(root);
	        return sum_;
	    }
	private:
	    int sum_;
	    void preTraversal(TreeNode* node) {
	        if (!node) return;
	        if (node->left && isLeaf(node->left))
	            sum_ += node->left->val;
	        
	        preTraversal(node->left);
	        preTraversal(node->right);
	    }
	    bool isLeaf(TreeNode* node) {
	        return !node->left && !node->right;
	    }
	};

尋訪二元樹，前中後皆可，找到左子節點且為葉節點，將其值加入sum_中即可。