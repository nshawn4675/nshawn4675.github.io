---
layout: post
title: "[LeetCode February Challange] Day 6 - Binary Tree Right Side View"
date: 2021-02-06 00:00:00 +0800
categories: LeetCode
tags: [Medium, Tree, Depth-First Search, Breadth-First Search, Binary Tree, Facebook, Amazon, ByteDance, eBay, Microsoft, Bloomberg, Apple, Accolite, C++]
---
Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

# Example:

	Input: [1,2,3,null,5,null,4]
	Output: [1, 3, 4]
	Explanation:

	   1            <---
	 /   \
	2     3         <---
	 \     \
	  5     4       <---

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
	    vector<int> rightSideView(TreeNode* root) {
	        ans = {};
	        dfs(root, 1);
	        return ans;
	    }
	private:
	    vector<int> ans;
	    void dfs(TreeNode* root, int level) {
	        if (root == nullptr) return;
	        if (ans.size() < level)
	            ans.push_back(root->val);
	        dfs(root->right, level+1);
	        dfs(root->left, level+1);
	    }
	};

用 DFS 且中右左的方式，可以保證在該 level 第一個拜訪的元素是該層最右邊的。