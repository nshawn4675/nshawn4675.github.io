---
layout: post
title: "[LeetCode December Challange] Day 9 - Binary Search Tree Iterator"
date: 2020-12-09 00:00:00 +0800
categories: jekyll update
tags:
  [
    LeetCode,
    Medium,
    Stack,
    Tree,
    Design,
    Facebook,
    Amazon,
    Bloomberg,
    Microsoft,
    Google,
    ByteDance,
  ]
---

Implement the <font color="red">BSTIterator</font> class that represents an iterator over the [in-order traversal](<https://en.wikipedia.org/wiki/Tree_traversal#In-order_(LNR)>) of a binary search tree (BST)：

- <font color="red">BSTIterator(TreeNode root)</font> Initializes an object of the <font color="red">BSTIterator</font> class. The <font color="red">root</font> of the BST is given as part of the constructor. The pointer should be initialized to a non-existent number smaller than any element in the BST.
- <font color="red">boolean hasNext()</font> Returns <font color="red">true</font> if there exists a number in the traversal to the right of the pointer, otherwise returns <font color="red">false</font>.
- <font color="red">int next()</font> Moves the pointer to the right, then returns the number at the pointer.
  Notice that by initializing the pointer to a non-existent smallest number, the first call to <font color="red">next()</font> will return the smallest element in the BST.

You may assume that <font color="red">next()</font> calls will always be valid. That is, there will be at least a next number in the in-order traversal when <font color="red">next()</font> is called.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/173_ex1.png?raw=true)

    Input
    ["BSTIterator", "next", "next", "hasNext", "next", "hasNext", "next", "hasNext", "next", "hasNext"]
    [[[7, 3, 15, null, null, 9, 20]], [], [], [], [], [], [], [], [], []]
    Output
    [null, 3, 7, true, 9, true, 15, true, 20, false]

    Explanation
    BSTIterator bSTIterator = new BSTIterator([7, 3, 15, null, null, 9, 20]);
    bSTIterator.next();    // return 3
    bSTIterator.next();    // return 7
    bSTIterator.hasNext(); // return True
    bSTIterator.next();    // return 9
    bSTIterator.hasNext(); // return True
    bSTIterator.next();    // return 15
    bSTIterator.hasNext(); // return True
    bSTIterator.next();    // return 20
    bSTIterator.hasNext(); // return False

# Constraints:

- The number of nodes in the tree is in the range <font color="red">[1, 10^5]</font>.
- <font color="red">0 <= Node.val <= 10^6</font>
- At most <font color="red">10^5</font> calls will be made to <font color="red">hasNext</font>, and <font color="red">next</font>.

# Follow up:

- Could you implement <font color="red">next()</font> and <font color="red">hasNext()</font> to run in average <font color="red">O(1)</font> time and use <font color="red">O(h)</font> memory, where <font color="red">h</font> is the height of the tree?

---

# Solution

### constructor

Time complexity : O(n)  
Space complexity : O(n)

### next

Time complexity : O(1)  
Space complexity : O(n)

### hasNext

Time complexity : O(1)  
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
    class BSTIterator {
    public:
        BSTIterator(TreeNode* root) {
            inorder(root);
        }

        int next() {
            int ret = ctnt.front();
            ctnt.pop();
            return ret;
        }

        bool hasNext() {
            return !ctnt.empty();
        }

        void inorder(TreeNode* node) {
            if (node == nullptr) return;

            inorder(node->left);
            ctnt.push(node->val);
            inorder(node->right);
        }
    private:
        queue<int> ctnt;
    };

    /**
    * Your BSTIterator object will be instantiated and called as such:
    * BSTIterator* obj = new BSTIterator(root);
    * int param_1 = obj->next();
    * bool param_2 = obj->hasNext();
    */
