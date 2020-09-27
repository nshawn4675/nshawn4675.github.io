---
layout: post
title:  "[LeetCode September Challange]Day27-Evaluate Division"
date:   2020-09-27 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Union Find, Graph, Amazon, Google, Bloomberg, Facebook, Microsoft]
---
You are given <font color="red">equations</font> in the format <font color="red">A / B = k</font>, where <font color="red">A</font> and <font color="red">B</font> are variables represented as strings, and <font color="red">k</font> is a real number (floating-point number). Given some <font color="red">queries</font>, return the answers. If the answer does not exist, return <font color="red">-1.0</font>.  

The input is always valid. You may assume that evaluating the queries will result in no division by zero and there is no contradiction.  

# Example 1:  
	Input: equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
	Output: [6.00000,0.50000,-1.00000,1.00000,-1.00000]
	Explanation: 
	Given: a / b = 2.0, b / c = 3.0
	queries are: a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ?
	return: [6.0, 0.5, -1.0, 1.0, -1.0 ]

# Example 2:  
	Input: equations = [["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = [["a","c"],["c","b"],["bc","cd"],["cd","bc"]]
	Output: [3.75000,0.40000,5.00000,0.20000]

# Example 3:  
	Input: equations = [["a","b"]], values = [0.5], queries = [["a","b"],["b","a"],["a","c"],["x","y"]]
	Output: [0.50000,2.00000,-1.00000,-1.00000]

# Constraints:  
- **<font color="red">1 <= equations.length <= 20</font>**
- **<font color="red">equations[i].length == 2</font>**
- **<font color="red">1 <= equations[i][0], equations[i][1] <= 5</font>**
- **<font color="red">values.length == equations.length</font>**
- **<font color="red">0.0 < values[i] <= 20.0</font>**
- **<font color="red">1 <= queries.length <= 20</font>**
- **<font color="red">queries[i].length == 2</font>**
- **<font color="red">1 <= queries[i][0], queries[i][1] <= 5</font>**
- **<font color="red">equations[i][0], equations[i][1], queries[i][0], queries[i][1]</font>** consist of lower case English letters and digits.

______________________  

# Solution

### Graph  

Time complexity : O(e+q\*e)  
Space complexity : O(e)  

	class Solution {
	public:
	    vector<double> calcEquation(vector<vector<string>>& equations, vector<double>& values, vector<vector<string>>& queries) {
	        unordered_map<string, unordered_map<string, double>> g;
	        
	        // build graph
	        for (int i=0; i<equations.size(); ++i) {
	            string up = equations[i][0];
	            string down = equations[i][1];
	            double val = values[i];
	            g[up][down] =  val;
	            g[down][up] = 1/val;
	        }
	        
	        // dfs + backtracking
	        vector<double> ans;
	        for (vector<string> q: queries) {
	            string up = q[0];
	            string down = q[1];
	            if (!g.count(up) || !g.count(down))
	                ans.push_back(-1);
	            else {
	                unordered_set<string> visited;
	                ans.push_back(dfs(g, up, down, visited));
	            }
	        }
	        
	        return ans;
	    }
	private:
	    double dfs(unordered_map<string, unordered_map<string, double>>& g,
	               string cur_node, string des_node, unordered_set<string> visited) {
	        visited.insert(cur_node);
	        if (cur_node == des_node)
	            return 1;
	        else {
	            for (auto next: g[cur_node]) {
	                if (visited.count(next.first) != 0)
	                    continue;
	                double res = dfs(g, next.first, des_node, visited);
	                if (res > 0) return res * g[cur_node][next.first];
	            }
	        }
	        return -1;
	    }
	};

### Union Find / Disjoint Set

Time complexity : O(q+e)  
Space complexity : O(e)  

	class Solution {
	public:
	    vector<double> calcEquation(vector<vector<string>>& equations, vector<double>& values, vector<vector<string>>& queries) {
	        unordered_map<string, pair<string, double>> parents;
	        
	        for (int i=0; i<equations.size(); ++i) {
	            string A = equations[i][0];
	            string B = equations[i][1];
	            double val = values[i];
	            if (!parents.count(A) && !parents.count(B)) {
	                parents[A] = {B, val};
	                parents[B] = {B, 1};
	            } else if (!parents.count(A)) {
	                parents[A] = {B, val};
	            } else if (!parents.count(B)) {
	                parents[B] = {A, 1/val};
	            } else {
	                // merge
	                auto rA = find(A, parents);
	                auto rB = find(B, parents);
	                parents[rA.first] = {rB.first, val * rB.second / rA.second };
	                /*
	                A / rA = x, rA = A / X
	                B / rB = y, rB = B / y
	                NEW : val = A / B;
	                rA / rB = (A/X)*(y/B) = (A/B)*(y/x) = val * y / x
	                */
	            }
	        }
	        
	        vector<double> ans;
	        for (vector<string> q: queries) {
	            string A = q[0];
	            string B = q[1];
	            if (!parents.count(A) || !parents.count(B)) {
	                ans.push_back(-1);
	                continue;
	            }
	            auto rA = find(A, parents);
	            auto rB = find(B, parents);
	            if (rA.first != rB.first) {
	                ans.push_back(-1);
	            } else {
	                ans.push_back(rA.second / rB.second);
	            }
	        }
	        
	        return ans;
	    }
	private:
	    pair<string, double> find(string cur, unordered_map<string, pair<string, double>> parents) {
	        if (cur != parents[cur].first) {
	            auto r = find(parents[cur].first, parents);
	            parents[cur].first = r.first;
	            parents[cur].second *= r.second;
	        }
	        return parents[cur];
	    }
	};