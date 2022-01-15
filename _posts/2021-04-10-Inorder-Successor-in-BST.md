---
layout: post
title: "Inorder Successor in BST"
date: 2021-04-10 00:00:00 +0800
categories: LeetCode
tags: [Medium, Tree, Amazon, Microsoft, C++]
---
Given the <font color="red">root</font> of a binary search tree and a node <font color="red">p</font> in it, return *the in-order successor of that node in the BST*. If the given node has no in-order successor in the tree, return <font color="red">null</font>.

The successor of a node <font color="red">p</font> is the node with the smallest key greater than <font color="red">p.val</font>.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/285_ex1.png?raw=true)

    Input: root = [2,1,3], p = 1
    Output: 2
    Explanation: 1's in-order successor node is 2. Note that both p and the return value is of TreeNode type.

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/285_ex2.png?raw=true)

    Input: root = [5,3,6,2,4,null,null,1], p = 6
    Output: null
    Explanation: There is no in-order successor of the current node, so the answer is null.
 

# Constraints:

- The number of nodes in the tree is in the range <font color="red">[1, 10^4]</font>.
- <font color="red">-10^5 <= Node.val <= 10^5</font>
- All Nodes will have unique values.

______________________  

# Solution  

# Inorder traversal (iterative)  

Time complexity : O(n)  
Space complexity : O(n)  

    class Solution {
    public:
        TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
            stack<TreeNode*> stk;
            TreeNode* curr = root;
            bool is_p = false;
            while (curr || !stk.empty()) {
                while (curr) {
                    stk.push(curr);
                    curr = curr->left;
                }
                curr = stk.top(); stk.pop();
                if (is_p) return curr;
                if (curr == p) is_p = true;
                curr = curr->right;
            }
            return nullptr;
        }
    };

# Inorder Traversal (recursive)  

Time complexity : O(n)  
Space complexity : O(n)  

    class Solution {
    public:
        TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
            ans = nullptr;
            inorder(root, p);
            return ans;
        }
    private:
        TreeNode *prev, *ans;
        void inorder(TreeNode* node, TreeNode* p) {
            if (!node) return;
            inorder(node->left, p);
            if (prev == p) ans = node;
            prev = node;
            inorder(node->right, p);
        }
    };

# BST Traversal (iterative)  

Time complexity : O(n)  
Space complexity : O(1)  

    class Solution {
    public:
        TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
            TreeNode* ans = nullptr;
            while (root) {
                if (root->val <= p->val)
                    root = root->right;
                else {
                    ans = root;
                    root = root->left;
                }
            }
            return ans;
        }
    };

# BST Traversal (recursive)  

Time complexity : O(n)  
Space complexity : O(n)  

    class Solution {
    public:
        TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
            if (!root) return nullptr;
            if (root->val <= p->val)
                return inorderSuccessor(root->right, p);
            else {
                TreeNode *left_res = inorderSuccessor(root->left, p);
                return left_res ? left_res : root;
            }
        }
    };