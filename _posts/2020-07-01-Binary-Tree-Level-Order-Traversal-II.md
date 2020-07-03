---
layout: post
title:  "[LeetCode July Challange]Day2-Binary Tree Level Order Traversal II"
date:   2020-07-02 00:00:00 +0800
categories: jekyll update
tags:
---
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).  

For example:  
Given binary tree [3,9,20,null,null,15,7],  

	    3  
	   / \  
	  9  20  
	    /  \  
	   15   7  

return its bottom-up level order traversal as:  

	 [  
	  [15,7],  
	  [9,20],  
	  [3]  
	 ]  

______________________  
# solution
time complexity : O(n)  
space complexity : O(n)  

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
	    vector<vector<int>> levelOrderBottom(TreeNode* root) {
	        vector<vector<int>> ans;
	        
	        // ans = BFS(root);
	        DFS(root, 0, ans);
	        
	        reverse(ans.begin(), ans.end());
	        return ans;
	    }
	private:
	    vector<vector<int>> BFS(TreeNode* root) {
	        if (!root) return {};
	        vector<vector<int>> ans;
	        vector<TreeNode*> cur, next;
	        cur.push_back(root);
	        while (!cur.empty()) {
	            ans.push_back({});
	            for (TreeNode* node : cur) {
	                ans.back().push_back(node->val);
	                if (node->left) next.push_back(node->left);
	                if (node->right) next.push_back(node->right);
	            }
	            cur.swap(next);
	            next.clear();
	        }
	        return ans;
	    }
	    
	    void DFS(TreeNode* node, int depth, vector<vector<int>>& ans) {
	        if (!node) return;
	        while (ans.size() <= depth) ans.push_back({});
	        ans[depth].push_back(node->val);
	        DFS(node->left, depth+1, ans);
	        DFS(node->right, depth+1, ans);
	        
	    }
	};

此題探討的是**二元樹的尋訪**，一般常見的二元樹尋訪，依據root被尋訪到的順序，有三個：前序(中前後)、中序(前中後)、後序(前後中)。  
此處是希望得到level order左至右且bottom up的結構，兩個思考方向得到top down的level order結果後，再reverse結果即可：  
1. BFS，用容器cur存放現在所在層應處理的node，且用容器next存放下一層要處理的node，一層一層往下做，直到所有node都被處理完畢。  
2. DFS，尋訪所有node(前中後皆可)，根據node所在層數，塞入容器相對應最後面的位置即可。  

(得到top down的level order → reverse)