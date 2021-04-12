---
layout: post
title:  "[LeetCode April Challange] Day 11 - Deepest Leaves Sum"
date:   2021-04-11 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Tree, Depth-first Search, Google]
---
Given the <font color="red">root</font> of a binary tree, return *the sum of values of its deepest leaves*.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1302_ex.png?raw=true)

    Input: root = [1,2,3,4,5,null,6,7,null,null,null,null,8]
    Output: 15

# Example 2:

    Input: root = [6,7,8,2,7,1,3,9,null,1,4,null,null,null,5]
    Output: 19

# Constraints:

- The number of nodes in the tree is in the range <font color="red">[1, 10^4]</font>.
- <font color="red">1 <= Node.val <= 100</font>

______________________  

# Solution  

# Level Order Traversal  

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
        int deepestLeavesSum(TreeNode* root) {
            int ans = 0, i = 0;
            queue<TreeNode*> q;
            q.push(root);
            while (!q.empty()) {
                for (i=q.size()-1, ans=0; 0<=i; --i) {
                    TreeNode *cur = q.front(); q.pop();
                    ans += cur->val;
                    if (cur->left) q.push(cur->left);
                    if (cur->right) q.push(cur->right);
                }
            }
            return ans;
        }
    };