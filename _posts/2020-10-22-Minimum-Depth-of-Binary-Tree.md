---
layout: post
title:  "[LeetCode October Challange] Day 22 - Minimum Depth of Binary Tree"
date:   2020-10-22 00:00:00 +0800
categories: LeetCode
tags: [Easy, Tree, Depth-first Search, Breadth-first Search, Binary Tree, Facebook, Apple, C++]
---
Given a binary tree, find its minimum depth.  

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.  

**Note:** A leaf is a node with no children.  

# Example 1:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/111_ex1.jpg?raw=true)

	Input: root = [3,9,20,null,null,15,7]
	Output: 2

# Example 2:  
	Input: root = [2,null,3,null,4,null,5,null,6]
	Output: 5

# Constraints:  
- The number of nodes in the tree is in the range <font color="red">[0, 10^5]</font>.
- <font color="red">-1000 <= Node.val <= 1000</font>

______________________  

# Solution  

### recursive DFS

Time complexity : O(n)  
Space complexity : O(log(n))  

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
	    int minDepth(TreeNode* root) {
	        if (!root) return 0;
	        if (!root->left) return 1+minDepth(root->right);
	        if (!root->right) return 1+minDepth(root->left);
	        return 1+min(minDepth(root->left), minDepth(root->right));
	    }
	};

### iterative DFS  

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
	    int minDepth(TreeNode* root) {
	        if (!root) return 0;
	        stack<pair<TreeNode*, int>> s;
	        int ans = INT_MAX;
	        s.push({root, 1});
	        while (!s.empty()) {
	            pair<TreeNode*, int> node = s.top(); s.pop();
	            if (!node.first->left && !node.first->right)
	                ans = min(ans, node.second);
	            if (node.first->left) s.push({node.first->left, node.second+1});
	            if (node.first->right) s.push({node.first->right, node.second+1});
	        }
	        return ans;
	    }
	};

### iterative BFS  

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
	    int minDepth(TreeNode* root) {
	        if (!root) return 0;
	        queue<TreeNode*> q;
	        int ans = 0;
	        q.push(root);
	        while (!q.empty()) {
	            ++ans;
	            int q_size = q.size();
	            for (int i=0; i<q_size; ++i) {
	                TreeNode* node = q.front();
	                if (!node->left && !node->right) return ans;
	                if (node->left) q.push(node->left);
	                if (node->right) q.push(node->right);
	                q.pop();
	            }
	        }
	        return ans;
	    }
	};