---
layout: post
title:  "[LeetCode February Challange] Day 17 - Container With Most Water"
date:   2021-02-17 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Array, Two Pointers, Facebook, Amazon, Adobe, Microsoft, Google, Goldman Sachs, Yahoo, Salesforce, tcs]
---
Given <font color="red">n</font> non-negative integers <font color="red">a1, a2, ..., an</font> , where each represents a point at coordinate <font color="red">(i, ai)</font>. <font color="red">n</font> vertical lines are drawn such that the two endpoints of the line <font color="red">i</font> is at <font color="red">(i, ai)</font> and <font color="red">(i, 0)</font>. Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

**Notice** that you may not slant the container.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/11_ex1.jpg?raw=true)

	Input: height = [1,8,6,2,5,4,8,3,7]
	Output: 49
	Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

# Example 2:

	Input: height = [1,1]
	Output: 1

# Example 3:

	Input: height = [4,3,2,1,4]
	Output: 16

# Example 4:

	Input: height = [1,2,1]
	Output: 2

# Constraints:

- <font color="red">n == height.length</font>
- <font color="red">2 <= n <= 3 * 10^4</font>
- <font color="red">0 <= height[i] <= 3 * 10^4</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int maxArea(vector<int>& height) {
	        const int n = height.size();
	        int ans = INT_MIN;
	        int l = 0, r = n - 1;
	        while (l < r) {
	            int h = min(height[l], height[r]);
	            ans = max(ans, h*(r-l));
	            if (height[l] < height[r])
	                ++l;
	            else
	                --r;
	        }
	        return ans;
	    }
	};

2 Pointers，Greedy， 左右往中間跑，優先移動較短的，因較短的有較大的機會下一根比較長，而使 area 變大。