---
layout: post
title:  "[LeetCode August Challange]Day12-Pascal's Triangle II"
date:   2020-08-12 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given a non-negative index k where k ≤ 33, return the k-th index row of the Pascal's triangle.  

Note that the row index starts from 0.

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/PascalTriangleAnimated2.gif?raw=true)

In Pascal's triangle, each number is the sum of the two numbers directly above it.  

# Example:  
	Input: 3
	Output: [1,3,3,1]

# Follow up:  
Could you optimize your algorithm to use only O(k) extra space?  

______________________  

# solution

Time complexity : O(k)  
Space complexity : O(k)  

	class Solution {
	public:
	    vector<int> getRow(int rowIndex) {
	        vector<int> res(rowIndex+1, 0);
	        res[0] = 1;
	        
	        for (int i=1; i<=rowIndex; ++i) {
	            for (int j=i; j>=1; --j) {
	                res[j] = res[j]+res[j-1];
	            }
	        }
	        
	        return res;
	    }
	};

例子：

	k = 4
	1 0 0 0 0
	1 1 0 0 0
	1 2 1 0 0
	1 3 3 1 0
	1 4 6 4 1