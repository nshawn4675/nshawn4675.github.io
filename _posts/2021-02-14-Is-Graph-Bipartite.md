---
layout: post
title: "[LeetCode February Challange] Day 14 - Is Graph Bipartite?"
date: 2021-02-14 00:00:00 +0800
categories: LeetCode
tags: [Medium, Depth-First Search, Breadth-First Search, Union Find, Graph, Facebook, eBay, ByteDance, C++]
---
There is an **undirected** graph with <font color="red">n</font> nodes, where each node is numbered between <font color="red">0</font> and <font color="red">n - 1</font>. You are given a 2D array <font color="red">graph</font>, where <font color="red">graph[u]</font> is an array of nodes that node <font color="red">u</font> is adjacent to. More formally, for each <font color="red">v</font> in <font color="red">graph[u]</font>, there is an undirected edge between node <font color="red">u</font> and node <font color="red">v</font>. The graph has the following properties:

- There are no self-edges (<font color="red">graph[u]</font> does not contain <font color="red">u</font>).
- There are no parallel edges (<font color="red">graph[u]</font> does not contain duplicate values).
- If <font color="red">v</font> is in <font color="red">graph[u]</font>, then <font color="red">u</font> is in <font color="red">graph[v]</font> (the graph is undirected).
- The graph may not be connected, meaning there may be two nodes <font color="red">u</font> and <font color="red">v</font> such that there is no path between them.

A graph is **bipartite** if the nodes can be partitioned into two independent sets <font color="red">A</font> and <font color="red">B</font> such that **every** edge in the graph connects a node in set <font color="red">A</font> and a node in set <font color="red">B</font>.

Return <font color="red">true</font> *if and only if it is **bipartite***.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/785_ex1.jpg?raw=true)

	Input: graph = [[1,2,3],[0,2],[0,1,3],[0,2]]
	Output: false
	Explanation: There is no way to partition the nodes into two independent sets such that every edge connects a node in one and a node in the other.

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/785_ex2.jpg?raw=true)

	Input: graph = [[1,3],[0,2],[1,3],[0,2]]
	Output: true
	Explanation: We can partition the nodes into two sets: {0, 2} and {1, 3}.

# Constraints:

- <font color="red">graph.length == n</font>
- <font color="red">1 <= n <= 100</font>
- <font color="red">0 <= graph[u].length < n</font>
- <font color="red">0 <= graph[u][i] <= n - 1</font>
- **<font color="red">graph[u]</font>** does not contain <font color="red">u</font>.
- All the values of <font color="red">graph[u]</font> are **unique**.
- If <font color="red">graph[u]</font> contains <font color="red">v</font>, then <font color="red">graph[v]</font> contains <font color="red">u</font>.

______________________  

# Solution  

Time complexity : O(N+E) (N : # nodes, E : # edges)  
Space complexity : O(N)  

	class Solution {
	public:
	    bool isBipartite(vector<vector<int>>& graph) {
	        const int n = graph.size();
	        vector<int> color(n, -1);
	        
	        for (int i=0; i<n; ++i) {
	            if (color[i] != -1)
	                continue;
	            stack<int> stk;
	            stk.push(i);
	            while (!stk.empty()) {
	                int node = stk.top(); stk.pop();
	                if (color[node] == -1) color[node] = 0;
	                for (int neigh: graph[node]) {
	                    if (color[neigh] == -1) {
	                        stk.push(neigh);
	                        color[neigh] = color[node] ^ 1;
	                    } else if (color[node] == color[neigh])
	                        return false;
	                }
	            }
	        }
	        
	        return true;
	    }
	};

遍歷過所有 node ，且用 BFS 的方式檢查上色狀況。
用 color 陣列記錄各個 node 被標記的顏色，-1 代表尚未標記，0 、 1 分別代表兩種不同顏色。  