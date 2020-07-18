---
layout: post
title:  "[LeetCode July Challange]Day18-Course Schedule II"
date:   2020-07-18 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
There are a total of *n* courses you have to take, labeled from **0** to **n-1**.  

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: **[0,1]**  

Given the total number of courses and a list of prerequisite **pairs**, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

# Example 1:  
	Input: 2, [[1,0]] 
	Output: [0,1]
	Explanation: There are a total of 2 courses to take. To take course 1 you should have finished   
	             course 0. So the correct course order is [0,1] .

# Example 2:  
	Input: 4, [[1,0],[2,0],[3,1],[3,2]]
	Output: [0,1,2,3] or [0,2,1,3]
	Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both     
	             courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. 
	             So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3] .

# Note:  
1. The input prerequisites is a graph represented by a **list of edges**, not adjacency matrices. Read more about [how a graph is represented](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs).
2. You may assume that there are no duplicate edges in the input prerequisites.

______________________  

# solution
time complexity : O(V+E)  
space complexity : O(V+E)
(V：# nodes, E : # edges)  

	class Solution {
	public:
	    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
	        // init graph
	        graph_ = vector<vector<int>>(numCourses);
	        for (vector<int> i: prerequisites)
	            graph_[i[1]].push_back(i[0]);
	        
	        // for each course, start dfs tracking.
	        stat_ = vector<int>(numCourses, 0);
	        for (int i=0; i<numCourses; ++i) {
	            if (findCircle(i)) return {};
	        }
	        
	        // correction topology order
	        reverse(res_.begin(), res_.end());
	        return res_;
	    }
	private:
	    vector<vector<int>> graph_;
	    vector<int> stat_;
	    vector<int> res_;  
	    enum {IDLE, CHECKING, CHECKED};
	    bool findCircle(int node) {
	        if (stat_[node] == CHECKING) return true;
	        else if (stat_[node] == CHECKED) return false;
	        stat_[node] = CHECKING;
	        for (int i: graph_[node]) {
	            if (findCircle(i)) return true;
	        }
	        stat_[node] = CHECKED;
	        res_.push_back(node);
	        return false;
	    }
	};

此題是拓樸排序問題。  
首先要了解的是如何用資料結構表示一張圖？  
在此定義的是{node num, {next neighbors}}  
例如：1號node指向2、3、4號node可用{1, {2, 3, 4}}來表示。  

首先利用題目，建立好一張圖。  
再根據各個node，dfs的方式、每個鄰居去檢查是否存在cycle？  
順便將一路上檢查的node按順序存起來。  
但是存放的順序，因為要確保檢查的node是沒有cycle的，所以是以dfs離開時的順序存放，與實際上檢查的順序相反。  
故實際上拓樸的順序要再reverse一次才是正確的。  