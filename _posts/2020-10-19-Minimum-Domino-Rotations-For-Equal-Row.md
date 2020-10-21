---
layout: post
title:  "[LeetCode October Challange] Day 19 - Minimum Domino Rotations For Equal Row"
date:   2020-10-19 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Array, Greedy, Google]
---
In a row of dominoes, <font color="red">A[i]</font> and <font color="red">B[i]</font> represent the top and bottom halves of the <font color="red">i-th</font> domino.  (A domino is a tile with two numbers from 1 to 6 - one on each half of the tile.)  

We may rotate the <font color="red">i-th</font> domino, so that <font color="red">A[i]</font> and <font color="red">B[i]</font> swap values.  

Return the minimum number of rotations so that all the values in <font color="red">A</font> are the same, or all the values in <font color="red">B</font> are the same.

If it cannot be done, return <font color="red">-1</font>.  

# Example 1:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/1007_ex1.png?raw=true)

	Input: A = [2,1,2,4,2,2], B = [5,2,6,2,3,2]
	Output: 2
	Explanation: 
	The first figure represents the dominoes as given by A and B: before we do any rotations.
	If we rotate the second and fourth dominoes, we can make every value in the top row equal to 2, as indicated by the second 
	figure.

# Example 2:  
	Input: A = [3,5,1,2,3], B = [3,6,3,3,4]
	Output: -1
	Explanation: 
	In this case, it is not possible to rotate the dominoes to make one row of values equal.

# Constraints:  
- <font color="red">2 <= A.length == B.length <= 2 * 10^4</font>
- <font color="red">1 <= A[i], B[i] <= 6</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int minDominoRotations(vector<int>& A, vector<int>& B) {
	        int ans = INT_MAX;
	        for (int dot=1; dot<=6; ++dot) {
	            int count_a = 0;
	            int count_b = 0;
	            bool isValid = true;
	            for (int idx=0; idx<A.size(); ++idx) {
	                if (A[idx] != dot && B[idx] != dot) {
	                    isValid = false;
	                    break;
	                }
	                if (A[idx] == dot && B[idx] != dot) ++count_a;
	                if (A[idx] != dot && B[idx] == dot) ++count_b;
	            }
	            if (isValid) ans = min(ans, min(count_a, count_b));
	        }
	        return ans == INT_MAX ? -1 : ans;
	    }
	};

窮舉點數1~6，去計算A、B有幾個，  
若該點數沒有在A、B出現，則代表該數不可能成立。  
若該點數出現在A、沒出現在B，代表可swap。  
若該點數沒出現在A、出現在B，代表可swap。  
最後統計該點數出現最少的那一個，可swap至多的一方，形成該row點數一致。