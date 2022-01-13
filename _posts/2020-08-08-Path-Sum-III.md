---
layout: post
title:  "[LeetCode August Challange]Day8-Path Sum III"
date:   2020-08-08 00:00:00 +0800
categories: LeetCode
tags: [Tree, Depth-First-Search, Binary Tree, C++]
---
You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.  

# Example:  
	root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

	      10
	     /  \
	    5   -3
	   / \    \
	  3   2   11
	 / \   \
	3  -2   1

	Return 3. The paths that sum to 8 are:

	1.  5 -> 3
	2.  5 -> 2 -> 1
	3. -3 -> 11

______________________  

# solution

Time complexity : O(n^2)  
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
	    int pathSum(TreeNode* root, int sum) {
	        if (!root) return 0;
	        return count(root, sum) + pathSum(root->left, sum) + pathSum(root->right, sum);
	    }
	private:
	    int count(TreeNode* node, int remain) {
	        if (!node) return 0;
	        remain -= node->val;
	        return (remain==0) + count(node->left, remain) + count(node->right, remain);
	    }
	};

利用遞迴，遞回出每一個node當做start point的結果數量。  

另一個解法，利用計數 prefix sum 來做：  

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
	    int pathSum(TreeNode* root, int sum) {
	        ans_ = 0;
	        cnt_ = { {0, 1}};
	        inorderTraversal(root, 0, sum);
	        return ans_;
	    }
	private:
	    int ans_;
	    unordered_map<int, int> cnt_;
	    void inorderTraversal(TreeNode* node, int cur, int& target) {
	        if (!node) return;
	        cur += node->val;
	        ans_ += cnt_[cur-target];
	        ++cnt_[cur];
	        inorderTraversal(node->left, cur, target);
	        inorderTraversal(node->right, cur, target);
	        --cnt_[cur];
	    }
	};

prefix sum 演算法步驟：  
1. 初始化目前為止，某數出現了幾次的map，cnt_：\{\{0, 1\}\}。(0出現了1次)  
2. 跑過每個元素：  
	2-1. 計算目前總和。  
	2-2. 組成目標數的方式數量 ans_ = cnt_[curSum-target]  
	2-3. ++cnt_[curSum]

在此最後會--cnt_[cur]的原因是，因為返回了，會繼續往別的方向計算，之前計算的不是在同一個方向中，所以不能被算在內，必須扣掉。