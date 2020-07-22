---
layout: post
title:  "[LeetCode July Challange]Day22-Binary Tree Zigzag Level Order Traversal"
date:   2020-07-22 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given a binary tree, return the *zigzag level order* traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).  

For example:
Given binary tree [3,9,20,null,null,15,7],

	    3
	   / \
	  9  20
	    /  \
	   15   7

return its zigzag level order traversal as:  

	[
	  [3],
	  [20,9],
	  [15,7]
	]

______________________  

# solution  
time complexity : O(n^2)  
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
	    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
	        if (!root) return {};
	        vector<vector<int>> res;
	        vector<TreeNode*> cur;
	        cur.push_back(root);
	        
	        while(!cur.empty()) {
	            vector<TreeNode*> next;
	            res.push_back({});
	            for (int i=0; i<cur.size(); ++i) {
	                res.back().push_back(cur[i]->val);
	                if (cur[i]->left) next.push_back(cur[i]->left);
	                if (cur[i]->right) next.push_back(cur[i]->right);
	            }
	            cur = next;
	        }
	        
	        for (int i=0; i<res.size(); ++i) {
	            if (i%2) reverse(res[i].begin(), res[i].end());
	        }
	        
	        return res;
	    }
	};

題目要得到一個「之」字型的traversal。  
流程：得出level order → 偶數層反轉即可。  

level order：  
cur代表目前所在層要處理的所有node。  
next代表下一層要處理的所有node。  
處理目前層，首先在res尾巴造容器，再一一處理node，分別將其值存入剛造好的容器、以及將其左右子node存到next。  
將所有目前層的node處理完後，用next替代，直到把所有層、所有node都處理完畢。  

最後因為得出的是level order，要把它轉變為「之」字型的樣子，所以將偶數層的內容反轉，即得出答案。