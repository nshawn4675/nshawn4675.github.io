---
layout: post
title:  "[LeetCode July Challange]Day24-All Paths From Source to Target"
date:   2020-07-24 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given a directed, acyclic graph of **N** nodes.  Find all possible paths from node **0** to node **N-1**, and return them in any order.  

The graph is given as follows:  the nodes are 0, 1, ..., graph.length - 1.  graph[i] is a list of all nodes j for which the edge (i, j) exists.  

# Example:  
	Input: [[1,2], [3], [3], []] 
	Output: [[0,1,3],[0,2,3]] 
	Explanation: The graph looks like this:
	0--->1
	|    |
	v    v
	2--->3
	There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.

# Note:  
- The number of nodes in the graph will be in the range **[2, 15]**.
- You can print different paths in any order, but you should keep the order of nodes inside one path.

______________________  

# solution
time complexity : O(n!)  
space complexity : O(n)

	class Solution {
	public:
	    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
	        vector<int> curRes = {0};
	        dfs(curRes, graph[0], graph);
	        return res;
	    }
	private:
	    vector<vector<int>> res;
	    void dfs(vector<int> &curRes, vector<int> nexts, vector<vector<int>>& graph) {
	        if (0 == nexts.size()) {
	            res.push_back(curRes);
	            return;
	        }
	        
	        for (int num: nexts) {
	            curRes.push_back(num);
	            dfs(curRes, graph[num], graph);
	            curRes.pop_back();
	        }
	    }
	};

題目的輸入意思是：第一個node 0指向node 1、2，...以此類推。  
列舉從頭到尾的路線，利用dfs以及backtracking，即可一一得出答案。  