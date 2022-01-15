---
layout: post
title: "[LeetCode April Challange] Day 20 - N-ary Tree Preorder Traversal"
date: 2021-04-20 00:00:00 +0800
categories: LeetCode
tags: [Easy, Stack, Tree, Depth-First Search, C++]
---
Given the <font color="red">root</font> of an n-ary tree, return *the preorder traversal of its nodes' values*.

Nary-Tree input serialization is represented in their level order traversal. Each group of children is separated by the null value (See examples)

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/589_ex1.png?raw=true)

    Input: root = [1,null,3,2,4,null,5,6]
    Output: [1,3,5,6,2,4]

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/589_ex2.png?raw=true)

    Input: root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
    Output: [1,2,3,6,7,11,14,4,8,12,5,9,13,10]

# Constraints:

- The number of nodes in the tree is in the range <font color="red">[0, 10^4]</font>.
- <font color="red">0 <= Node.val <= 10^4</font>
- The height of the n-ary tree is less than or equal to <font color="red">1000</font>.

**Follow up:** Recursive solution is trivial, could you do it iteratively?

______________________  

# Solution  

# Recursion

Time complexity : O(n)  
Space complexity : O(n)  

    /*
    // Definition for a Node.
    class Node {
    public:
        int val;
        vector<Node*> children;

        Node() {}

        Node(int _val) {
            val = _val;
        }

        Node(int _val, vector<Node*> _children) {
            val = _val;
            children = _children;
        }
    };
    */

    class Solution {
    public:
        vector<int> preorder(Node* root) {
            ans = {};
            dfs(root);
            return ans;
        }
    private:
        vector<int> ans;
        void dfs(Node *node) {
            if (node == nullptr) return;
            ans.push_back(node->val);
            for (Node *c: node->children) {
                if (c == nullptr) continue;
                dfs(c);
            }
        }
    };

# Iteration  

Time complexity : O(n)
Space complexity : O(n)  

    /*
    // Definition for a Node.
    class Node {
    public:
        int val;
        vector<Node*> children;

        Node() {}

        Node(int _val) {
            val = _val;
        }

        Node(int _val, vector<Node*> _children) {
            val = _val;
            children = _children;
        }
    };
    */

    class Solution {
    public:
        vector<int> preorder(Node* root) {
            vector<int> ans = {};
            stack<Node*> stk;
            stk.push(root);
            while (!stk.empty()) {
                Node *curr = stk.top(); stk.pop();
                if (curr == nullptr) continue;
                ans.push_back(curr->val);
                for (int i=curr->children.size()-1; 0<=i; --i)
                    stk.push(curr->children[i]);
            }
            return ans;
        }
    };