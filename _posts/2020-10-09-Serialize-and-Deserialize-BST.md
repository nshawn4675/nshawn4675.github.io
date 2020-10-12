---
layout: post
title:  "[LeetCode October Challange] Day 9 - Serialize and Deserialize BST"
date:   2020-10-09 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Tree, Amazon, Facebook, ByteDance]
---
Serialization is converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.  

Design an algorithm to serialize and deserialize a **binary search tree**. There is no restriction on how your serialization/deserialization algorithm should work. You need to ensure that a binary search tree can be serialized to a string, and this string can be deserialized to the original tree structure.  

**The encoded string should be as compact as possible**.  

# Example 1:  
	Input: root = [2,1,3]
	Output: [2,1,3]

# Example 2:  
	Input: root = []
	Output: []

# Constraints:  
- The number of nodes in the tree is in the range <font color="red">[0, 10^4]</font>.
- <font color="red">0 <= Node.val <= 10^4</font>
- The input tree is **guaranteed** to be a binary search tree.

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
	 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
	 * };
	 */
	class Codec {
	public:

	    // Encodes a tree to a single string.
	    string serialize(TreeNode* root) {
	        string s;
	        serialize(root, s);
	        return s;
	    }

	    // Decodes your encoded data to tree.
	    TreeNode* deserialize(string data) {
	        int pos = 0;
	        return deserialize(data, pos, INT_MIN, INT_MAX);
	    }
	private:
	    void serialize(TreeNode* node, string& s) {
	        if (!node) return;
	        s.append(reinterpret_cast<char*>(&node->val), sizeof(node->val));
	        serialize(node->left, s);
	        serialize(node->right, s);
	    }
	    
	    TreeNode* deserialize(string& s, int& pos, int cur_min, int cur_max) {
	        if (s.size() <= pos) return nullptr;
	        int val = *reinterpret_cast<int*>(s.data()+pos);
	        if (val < cur_min || cur_max < val) return nullptr;
	        pos += sizeof(val);
	        TreeNode* cur = new TreeNode(val);
	        cur->left = deserialize(s, pos, cur_min, val);
	        cur->right = deserialize(s, pos, val, cur_max);
	        return cur;
	    }
	};

	// Your Codec object will be instantiated and called as such:
	// Codec* ser = new Codec();
	// Codec* deser = new Codec();
	// string tree = ser->serialize(root);
	// TreeNode* ans = deser->deserialize(tree);
	// return ans;

Tree→string：每個int val轉換成長度為4bytes的string，用prefix的方式存。  
string→Tree：根據每4bytes的string，轉成int，用prefix的方式轉回。