---
layout: post
title:  "[LeetCode July Challange]Day27-Construct Binary Tree from Inorder and Postorder Traversal"
date:   2020-07-27 00:00:00 +0800
categories: LeetCode
tags: [Array, Hash Table, Divide and Conquer, Tree, Binary Tree, C++]
---
Given inorder and postorder traversal of a tree, construct the binary tree.  

# Note:  
You may assume that duplicates do not exist in the tree.  

For example, given  

	inorder = [9,3,15,20,7]
	postorder = [9,15,7,20,3]

return the following binary tree:  

	    3
	   / \
	  9  20
	    /  \
	   15   7

______________________  

# solution
time complexity : O(nlogn)  
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
	    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
	        int size = inorder.size();
	        if (size == 0) return nullptr;
	        
	        int rootVal = postorder[size-1];
	        printf("root = %d\n", rootVal);
	        TreeNode* cur = new TreeNode(rootVal);
	        int rootIdx = searchIdx(inorder, rootVal);
	        
	        int leftSize = rootIdx;
	        int rightSize = size-rootIdx-1;
	        vector<int> leftInorder(inorder.begin(), inorder.begin()+rootIdx);
	        vector<int> leftPostorder(postorder.begin(), postorder.begin()+leftSize);
	        /*printf("left inorder : ");
	        printVec(leftInorder);
	        printf("left postorder : ");
	        printVec(leftPostorder);*/
	        vector<int> rightInorder(inorder.begin()+rootIdx+1, inorder.end());
	        vector<int> rightPostorder(postorder.begin()+leftSize, postorder.begin()+leftSize+rightSize);
	        /*printf("right inorder : ");
	        printVec(rightInorder);
	        printf("right postorder : ");
	        printVec(rightPostorder);*/
	        
	        cur->left = buildTree(leftInorder, leftPostorder);
	        cur->right = buildTree(rightInorder, rightPostorder);
	        return cur;
	    }
	private:
	    int searchIdx(vector<int>& vec, int val) {
	        auto it = find(vec.begin(), vec.end(), val);
	        if (it != vec.end()) return distance(vec.begin(), it);
	        return -1;
	    }
	    void printVec(vector<int>& vec) {
	        for (int i: vec)
	            printf("%d ", i);
	        printf("\n");
	    }
	};

給定inorder、postorder，找出其完整的root(左右子樹皆連好)。  

首先找到root，就是postorder的最後一個元素。  
利用其value，找出他在inorder中的位置，就可以算出左右子樹的大小。  
有了左右子樹的大小，就可以得到左右子樹的inorder、postorder。  
再利用左右子樹的inorder、postorder，得出左右子樹的root。

inorder：[9,  **3**, *15, 20, 7*]  
postorder：[9, *15,  7, 20*, **3**]