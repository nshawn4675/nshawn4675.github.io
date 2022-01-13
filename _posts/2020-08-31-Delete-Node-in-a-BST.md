---
layout: post
title:  "[LeetCode August Challange]Day31-Delete Node in a BST"
date:   2020-08-31 00:00:00 +0800
categories: LeetCode
tags: [Tree, Binary Search Tree, Binary Tree, C++]
---
Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.  

Basically, the deletion can be divided into two stages:  
1. Search for a node to remove.
2. If the node is found, delete the node.

**Note:** Time complexity should be O(height of tree).  

# Example:  
	root = [5,3,6,2,4,null,7]
	key = 3

	    5
	   / \
	  3   6
	 / \   \
	2   4   7

	Given key to delete is 3. So we find the node with value 3 and delete it.

	One valid answer is [5,4,6,2,null,null,7], shown in the following BST.

	    5
	   / \
	  4   6
	 /     \
	2       7

	Another valid answer is [5,2,6,null,4,null,7].

	    5
	   / \
	  2   6
	   \   \
	    4   7

______________________  

# Solution

Time complexity : O(h)  
Space complexity : O(1)

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
	    TreeNode* deleteNode(TreeNode* root, int key) {
	        if (!root) return nullptr;
	        
	        if (key < root->val)
	            root->left = deleteNode(root->left, key);
	        else if (root->val < key)
	            root->right = deleteNode(root->right, key);
	        else {
	            // root->val == key
	            TreeNode* new_node = nullptr;
	            if (root->left && root->right) {
	                // root has both children
	                new_node = root->right;
	                TreeNode* parent = root;
	                while (new_node->left) {
	                    parent = new_node;
	                    new_node = new_node->left;
	                }
	                if (parent != root) {
	                    parent->left = new_node->right;
	                    new_node->right = root->right;
	                }
	                
	                new_node->left = root->left;
	            } else {
	                // root has no or one child.
	                new_node = root->left ? root->left : root->right;
	            }
	            delete root;
	            return new_node;
	        }
	        return root;
	    }
	};

首先要找到目標node，即node->val == key。  
因此若key < node->val，代表目標小於當前，則往左子樹走；若node->val < key，代表目標大於當前，則往右子樹走。  

找到目標node後，要刪掉它，此時node有以下情況：  
1. 沒有任何child。直接刪掉，return nullptr。
2. 有左子樹，無右子樹。刪掉後，return 左子樹。
3. 無左子樹，有右子樹。刪掉後，return 右子樹。
4. 有左右子樹，此時做法就很多元了，這邊採取的做法是「找到右子樹中值最小的來取代」。

如何「找到右子樹中值最小的node來取代」：  
最小的值，意指無左子樹，因此一直往左子樹走，走到無左子樹，就是值最小的node。  
找到後，再與目標node銜接即可。  