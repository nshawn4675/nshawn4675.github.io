---
layout: post
title:  "[LeetCode September Challange]Day5-All Elements in Two Binary Search Trees"
date:   2020-09-05 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given two binary search trees **<font color="red">root1</font>** and **<font color="red">root2</font>**.

Return a list containing all the *integers* from *both trees* sorted in **ascending** order.

 

# Example 1:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/AllElementsInTwoBST_ex1.png?raw=true)

	Input: root1 = [2,1,4], root2 = [1,0,3]
	Output: [0,1,1,2,3,4]

# Example 2:  
	Input: root1 = [0,-10,10], root2 = [5,1,7,0,2]
	Output: [-10,0,0,1,2,5,7,10]

# Example 3:  
	Input: root1 = [], root2 = [5,1,7,0,2]
	Output: [0,1,2,5,7]

# Example 4:  
	Input: root1 = [0,-10,10], root2 = []
	Output: [-10,0,10]

# Example 5:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/AllElementsInTwoBST_ex2.png?raw=true)

	Input: root1 = [1,null,8], root2 = [8,1]
	Output: [1,1,8,8]

# Constraints:  
- Each tree has at most **<font color="red">5000</font>** nodes.
- Each node's value is between **<font color="red">[-10^5, 10^5]</font>**.

______________________  

# Solution

Time complexity : O(n1+n2)  
Space complexity : O(n1+n2)

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
	    vector<int> getAllElements(TreeNode* root1, TreeNode* root2) {
	        traverseBST(root1, q1);
	        traverseBST(root2, q2);
	        
	        vector<int> res;
	        while (!q1.empty() && !q2.empty()) {
	            if (q1.front() < q2.front()) {
	                res.push_back(q1.front());
	                q1.pop();
	            } else {
	                res.push_back(q2.front());
	                q2.pop();
	            }
	        }
	        while (!q1.empty()) {
	            res.push_back(q1.front());
	            q1.pop();
	        }
	        while (!q2.empty()) {
	            res.push_back(q2.front());
	            q2.pop();
	        }
	        
	        return res;
	    }
	private:
	    queue<int> q1, q2;
	    void traverseBST(TreeNode* node, queue<int>& q) {
	        if (!node) return;
	        traverseBST(node->left, q);
	        q.push(node->val);
	        traverseBST(node->right, q);
	    }
	};

將兩顆樹的值，由小到大存入各個容器中，因是BST，故inorder traversal可得到小到大的順序。  
由小到大，將兩容器的數值合在一起。  