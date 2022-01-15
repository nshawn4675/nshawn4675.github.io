---
layout: post
title: "[LeetCode December Challange] Day 12 - Smallest Subtree with all the Deepest Nodes"
date: 2020-12-12 00:00:00 +0800
categories: LeetCode
tags: [Medium, Hash Table, Tree, Depth-first Search, Breadth-first Search, Binary Tree, Facebook, C++]
---

Given the <font color="red">root</font> of a binary tree, the depth of each node is **the shortest distance to the root**.

Return _the smallest subtree_ such that it contains **all the deepest nodes** in the original tree.

A node is called **the deepest** if it has the largest depth possible among any node in the entire tree.

The **subtree** of a node is tree consisting of that node, plus the set of all descendants of that node.

**Note:** This question is the same as 1123: https://leetcode.com/problems/lowest-common-ancestor-of-deepest-leaves/

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/865_ex1.png?raw=true)

    Input: root = [3,5,1,6,2,0,8,null,null,7,4]
    Output: [2,7,4]
    Explanation: We return the node with value 2, colored in yellow in the diagram.
    The nodes coloured in blue are the deepest nodes of the tree.
    Notice that nodes 5, 3 and 2 contain the deepest nodes in the tree but node 2 is the smallest subtree among them, so we return it.

# Example 2:

    Input: root = [1]
    Output: [1]
    Explanation: The root is the deepest node in the tree.

# Example 3:

    Input: root = [0,1,3,null,2]
    Output: [2]
    Explanation: The deepest node in the tree is 2, the valid subtrees are the subtrees of nodes 2, 1 and 0 but the subtree of node 2 is the smallest.

# Constraints:

- The number of nodes in the tree will be in the range <font color="red">[1, 500]</font>.
- <font color="red">0 <= Node.val <= 500</font>
- The values of the nodes in the tree are **unique**.

---

# Solution

Time complexity : O(n)  
Space complexity : O(h)

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
        TreeNode* subtreeWithAllDeepest(TreeNode* root) {
            return dfs(root).second;
        }

        pair<int, TreeNode*> dfs(TreeNode* node) {
            if (!node) return {0, nullptr};
            pair<int, TreeNode*> l = dfs(node->left),
                                r = dfs(node->right);
            int d_l = l.first, d_r = r.first;
            return {max(l.first, r.first)+1, d_l == d_r ? node : d_l > d_r ? l.second : r.second};
        }
    };

if node == nullptr，return {0, nullptr}

if left depth == right depth，左右皆有最深子樹，return {left.depth+1, node}。

if left depth > right depth，return {left.depth, left subtree}

if left depth < right depth，return {right.depth, right subtree}
