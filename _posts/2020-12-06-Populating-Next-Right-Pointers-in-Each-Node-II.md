---
layout: post
title: "[LeetCode December Challange] Day 6 - Populating Next Right Pointers in Each Node II"
date: 2020-12-06 00:00:00 +0800
categories: jekyll update
tags:
  [
    LeetCode,
    Medium,
    Tree,
    Depth-first Search,
    Bloomberg,
    Amazon,
    Microsoft,
    Facebook,
    Google,
  ]
---

Given a binary tree

    struct Node {
        int val;
        Node *left;
        Node *right;
        Node *next;
    }

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to <font color="red">NULL</font>.

Initially, all next pointers are set to <font color="red">NULL</font>.

# Follow up:

- You may only use constant extra space.
- Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/117_ex1.png?raw=true)

    Input: root = [1,2,3,4,5,null,7]
    Output: [1,#,2,3,#,4,5,7,#]
    Explanation: Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.

# Constraints:

- The number of nodes in the given tree is less than <font color="red">6000</font>.
- <font color="red">-100 <= node.val <= 100</font>

---

# Solution

Time complexity : O(n)  
Space complexity : O(1)

    /*
    // Definition for a Node.
    class Node {
    public:
        int val;
        Node* left;
        Node* right;
        Node* next;

        Node() : val(0), left(NULL), right(NULL), next(NULL) {}

        Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

        Node(int _val, Node* _left, Node* _right, Node* _next)
            : val(_val), left(_left), right(_right), next(_next) {}
    };
    */

    class Solution {
    public:
        Node* connect(Node* root) {
            if (root == nullptr) return nullptr;
            leftmost = root;
            while (leftmost) {
                Node* cur = leftmost;
                leftmost = prev = nullptr;
                while (cur) {
                    processChild(cur->left);
                    processChild(cur->right);
                    cur = cur->next;
                }
            }
            return root;
        }
        void processChild(Node* node) {
            if (node == nullptr) return;

            if (prev == nullptr)
                leftmost = node;
            else
                prev->next = node;

            prev = node;
        }
    private:
        Node *leftmost, *prev;
    };

此題直覺解法是用 BFS 的 level order traversal，但其 Time complexity 和 Space complexity 皆為 O(n)。

變數解譯：

1. leftmost，代表每一層中最左邊的 Node。
2. prev，代表前一個 Node。
3. cur，代表目前的 Node。

做到 leftmost 為 nullptr 為止，每一層開始時會把 prev 設為 nullptr，故在 process 時發現 prev 為 nullptr，即知道此 Node 為該層的第一個 Node。
