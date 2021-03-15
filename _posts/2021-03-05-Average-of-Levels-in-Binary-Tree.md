---
layout: post
title:  "[LeetCode March Challange] Day 05 - Average of Levels in Binary Tree"
date:   2021-03-05 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Tree, Facebook]
---
Given the <font color="red">root</font> of a binary tree, return *the average value of the nodes on each level in the form of an array*. Answers within <font color="red">10^-5</font> of the actual answer will be accepted.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/637_ex1.jpg?raw=true)

	Input: root = [3,9,20,null,15,7]
	Output: [3.00000,14.50000,11.00000]
	Explanation: The average value of nodes on level 0 is 3, on level 1 is 14.5, and on level 2 is 11.
	Hence return [3, 14.5, 11].

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/637_ex2.jpg?raw=true)

	Input: root = [3,9,20,15,7]
	Output: [3.00000,14.50000,11.00000]

# Constraints:

- The number of nodes in the tree is in the range <font color="red">[1, 10^4]</font>.
- <font color="red">-2^31 <= Node.val <= 2^(31 - 1)</font>

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
	    vector<double> averageOfLevels(TreeNode* root) {
	        vector<TreeNode*> q;
	        vector<double> ans;
	        
	        q.push_back(root);
	        while(!q.empty()) {
	            double avg = .0;
	            for (TreeNode* n: q) avg += n->val;
	            avg /= q.size();
	            ans.push_back(avg);
	            
	            vector<TreeNode*> next_q;
	            for (TreeNode* n: q) {
	                if (n->left) next_q.push_back(n->left);
	                if (n->right) next_q.push_back(n->right);
	            }
	            q = next_q;
	        }
	        
	        return ans;
	    }
	};