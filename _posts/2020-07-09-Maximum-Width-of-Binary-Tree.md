---
layout: post
title:  "[LeetCode July Challange]Day9-Maximum Width of Binary Tree"
date:   2020-07-09 00:00:00 +0800
categories: LeetCode
tags: [Tree, Depth-First-Search, Breadth-First-Search, Binary Tree, C++]
---
Given a binary tree, write a function to get the maximum width of the given tree. The width of a tree is the maximum width among all levels. The binary tree has the same structure as a **full binary tree**, but some nodes are null.  

The width of one level is defined as the length between the end-nodes (the leftmost and right most non-null nodes in the level, where the **null** nodes between the end-nodes are also counted into the length calculation.  

# Example 1:  
	Input: 

	           1
	         /   \
	        3     2
	       / \     \  
	      5   3     9 

	Output: 4
	Explanation: The maximum width existing in the third level with the length 4 (5,3,null,9).

# Example 2:  
	Input: 

	          1
	         /  
	        3    
	       / \       
	      5   3     

	Output: 2
	Explanation: The maximum width existing in the third level with the length 2 (5,3).

# Example 3:  
	Input: 

	          1
	         / \
	        3   2 
	       /        
	      5      

	Output: 2
	Explanation: The maximum width existing in the second level with the length 2 (3,2).

# Example 4:  
	Input: 

	          1
	         / \
	        3   2
	       /     \  
	      5       9 
	     /         \
	    6           7
	Output: 8
	Explanation:The maximum width existing in the fourth level with the length 8 (6,null,null,null,null,null,null,7).

# Note:  
Answer will in the range of 32-bit signed integer.  

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
	    int widthOfBinaryTree(TreeNode* root) {
	        if (!root) return 0;
	        int ans = 1;
	        queue<pair<TreeNode*, int>> q;
	        q.push({root, 1});
	        while (!q.empty()) {
	            int size = q.size();
	            ans = max(ans, q.back().second - q.front().second + 1);
	            for (int i=0; i<size; ++i) {
	                TreeNode* cur = q.front().first;
	                unsigned int pos = q.front().second;
	                q.pop();
	                if (cur->left) q.push({cur->left, pos*2});
	                if (cur->right) q.push({cur->right, pos*2+1});
	            }
	        }
	        return ans;
	    }
	};

設計資料結構，以{node, pos(編號)}為儲存單位，從root開始一層一層往下處理。此處計數方式為：  

	           1
	         /   \
	        2     3
	       / \   / \  
	      4   5 6   7

以此類推。  

若當前node的編號為i，則其左子樹的編號為i\*2，右子樹為i\*2+1。  
每次處理一個新的層時，先計算這一層最左邊和最右邊node編號的距離，即為該層的寬度。  