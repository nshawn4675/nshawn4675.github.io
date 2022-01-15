---
layout: post
title: "[LeetCode January Challange] Day 29 - Vertical Order Traversal of a Binary Tree"
date: 2021-01-29 00:00:00 +0800
categories: LeetCode
tags: [LeetCode, Hard, Hash Table, Tree, Depth-First Search, Breadth-First Search, Binary Tree, Facebook, Bloomberg, Amazon, Apple, ByteDance, Microsoft, C++]
---
Given the <font color="red">root</font> of a binary tree, calculate the **vertical order traversal** of the binary tree.

For each node at position <font color="red">(row, col)</font>, its left and right children will be at positions <font color="red">(row + 1, col - 1)</font> and <font color="red">(row + 1, col + 1)</font> respectively. The root of the tree is at <font color="red">(0, 0)</font>.

The **vertical order traversal** of a binary tree is a list of top-to-bottom orderings for each column index starting from the leftmost column and ending on the rightmost column. There may be multiple nodes in the same row and same column. In such a case, sort these nodes by their values.

Return *the **vertical order traversal** of the binary tree*.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/987_ex1.jpg?raw=true)

	Input: root = [3,9,20,null,null,15,7]
	Output: [[9],[3,15],[20],[7]]
	Explanation:
	Column -1: Only node 9 is in this column.
	Column 0: Nodes 3 and 15 are in this column in that order from top to bottom.
	Column 1: Only node 20 is in this column.
	Column 2: Only node 7 is in this column.

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/987_ex2.jpg?raw=true)

	Input: root = [1,2,3,4,5,6,7]
	Output: [[4],[2],[1,5,6],[3],[7]]
	Explanation:
	Column -2: Only node 4 is in this column.
	Column -1: Only node 2 is in this column.
	Column 0: Nodes 1, 5, and 6 are in this column.
	          1 is at the top, so it comes first.
	          5 and 6 are at the same position (2, 0), so we order them by their value, 5 before 6.
	Column 1: Only node 3 is in this column.
	Column 2: Only node 7 is in this column.

# Example 3:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/987_ex3.jpg?raw=true)

	Input: root = [1,2,3,4,6,5,7]
	Output: [[4],[2],[1,5,6],[3],[7]]
	Explanation:
	This case is the exact same as example 2, but with nodes 5 and 6 swapped.
	Note that the solution remains the same since 5 and 6 are in the same location and should be ordered by their values.

# Constraints:

- The number of nodes in the tree is in the range <font color="red">[1, 1000]</font>.
- <font color="red">0 <= Node.val <= 1000</font>

______________________  

# Solution  

Time complexity : O(nlogn)  
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
	    vector<vector<int>> verticalTraversal(TreeNode* root) {
	        int min_x = INT_MAX;
	        int max_x = INT_MIN;
	        int min_y = INT_MAX;
	        int max_y = INT_MIN;
	        map<pair<int, int>, priority_queue<int, vector<int>, greater<int>>> m;
	        function<void(int, int, TreeNode*)> DFS = [&](int x, int y, TreeNode* node) {
	            if (nullptr == node) return;
	        
	            m[{y, x}].push(node->val);
	            min_x = min(min_x, x);
	            max_x = max(max_x, x);
	            min_y = min(min_y, y);
	            max_y = max(max_y, y);

	            if (node->left) DFS(x-1, y+1, node->left);
	            if (node->right) DFS(x+1, y+1, node->right);
	        };
	        DFS(0, 0, root);
	        
	        vector<vector<int>> ans;
	        for (int x = min_x; x <= max_x; ++x) {
	            ans.push_back({});
	            for (int y = min_y; y <= max_y; ++y) {
	                if (0 == m.count({y, x})) continue;
	                while (!m[{y, x}].empty()) {
	                    ans.back().push_back(m[{y, x}].top());
	                    m[{y, x}].pop();
	                }
	            }
	        }
	        return ans;
	    }
	};

設計一 hash table：{y, x} -> {sorted_vals}  
{y, x} 的部份使用 pair，sorted_vals 的部份使用 min_heap

用 DFS 遍歷整棵樹，將相對應座標的值塞入。  

最後從左往右，由上而下，將記錄的資料變成 ans。