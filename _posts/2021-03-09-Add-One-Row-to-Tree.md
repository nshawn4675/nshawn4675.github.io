---
layout: post
title:  "[LeetCode March Challange] Day 09 - Add One Row to Tree"
date:   2021-03-09 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Tree, Glit Groupe]
---
Given the <font color="red">root</font> of a binary tree and two integers <font color="red">val</font> and <font color="red">depth</font>, add a row of nodes with value <font color="red">val</font> at the given depth <font color="red">depth</font>.

Note that the <font color="red">root</font> node is at depth <font color="red">1</font>.

The adding rule is:

- Given the integer <font color="red">depth</font>, for each not null tree node <font color="red">cur</font> at the depth <font color="red">depth - 1</font>, create two tree nodes with value <font color="red">val</font> as <font color="red">cur</font>'s left subtree root and right subtree root.
- **<font color="red">cur</font>**'s original left subtree should be the left subtree of the new left subtree root.
- **<font color="red">cur</font>**'s original right subtree should be the right subtree of the new right subtree root.
- If <font color="red">depth == 1</font> that means there is no depth <font color="red">depth - 1</font> at all, then create a tree node with value val as the new root of the whole original tree, and the original tree is the new root's left subtree.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/623_ex1.jpg?raw=true)

	Input: root = [4,2,6,3,1,5], val = 1, depth = 2
	Output: [4,1,1,2,null,null,6,3,1,5]

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/623_ex2.jpg?raw=true)

	Input: root = [4,2,null,3,1], val = 1, depth = 3
	Output: [4,2,null,1,1,3,null,null,1]

# Constraints:

- The number of nodes in the tree is in the range <font color="red">[1, 10^4]</font>.
- The depth of the tree is in the range <font color="red">[1, 10^4]</font>.
- <font color="red">-100 <= Node.val <= 100</font>
- <font color="red">-10^5 <= val <= 10^5</font>
- <font color="red">1 <= depth <= the depth of tree + 1</font>

______________________  

# Solution  

# BFS

Time complexity : O(n)  
Space complexity : O(logn)  

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
	    TreeNode* addOneRow(TreeNode* root, int val, int depth) {
	        if (root == nullptr) return nullptr;
	        else if (depth == 1) return new TreeNode(val, root, nullptr);
	        
	        queue<TreeNode*> q;
	        q.push(root);
	        int cur_d = 0;
	        while (!q.empty()) {
	            ++cur_d;
	            queue<TreeNode*> next_q;
	            while (!q.empty()) {
	                TreeNode* cur = q.front(); q.pop();
	                if (cur_d == depth-1) {
	                    cur->left = new TreeNode(val, cur->left, nullptr);
	                    cur->right = new TreeNode(val, nullptr, cur->right);
	                }
	                if (cur->left) next_q.push(cur->left);
	                if (cur->right) next_q.push(cur->right);
	            }
	            if (cur_d == depth) break;
	            q = next_q;
	        }
	        return root;
	    }
	};

# Recusion

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
	    TreeNode* addOneRow(TreeNode* root, int val, int depth) {
	        if (root == nullptr) return nullptr;
	        if (depth == 1) return new TreeNode(val, root, nullptr);
	        
	        if (depth == 2) {
	            root->left = new TreeNode(val, root->left, nullptr);
	            root->right = new TreeNode(val, nullptr, root->right);
	        } else {
	            addOneRow(root->left, val, depth-1);
	            addOneRow(root->right, val, depth-1);
	        }
	        return root;
	    }
	};