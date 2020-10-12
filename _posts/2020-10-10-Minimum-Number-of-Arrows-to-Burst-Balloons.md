---
layout: post
title:  "[LeetCode October Challange] Day 10 - Minimum Number of Arrows to Burst Balloons"
date:   2020-10-10 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Greedy, Sort, Facebook, Amazon]
---
There are some spherical balloons spread in two-dimensional space. For each balloon, provided input is the start and end coordinates of the horizontal diameter. Since it's horizontal, y-coordinates don't matter, and hence the x-coordinates of start and end of the diameter suffice. The start is always smaller than the end.  

An arrow can be shot up exactly vertically from different points along the x-axis. A balloon with <font color="red">x_start</font> and <font color="red">x_end</font> bursts by an arrow shot at <font color="red">x</font> if <font color="red">x_start ≤ x ≤ x_end</font>. There is no limit to the number of arrows that can be shot. An arrow once shot keeps traveling up infinitely.  

Given an array <font color="red">points</font> where <font color="red">points[i] = [x_start, x_end]</font>, return *the minimum number of arrows that must be shot to burst all balloons*.  

# Example 1:  
	Input: points = [[10,16],[2,8],[1,6],[7,12]]
	Output: 2
	Explanation: One way is to shoot one arrow for example at x = 6 (bursting the balloons [2,8] and [1,6]) and another arrow at x = 11 (bursting the other two balloons).

# Example 2:  
	Input: points = [[1,2],[3,4],[5,6],[7,8]]
	Output: 4

# Example 3:  
	Input: points = [[1,2],[2,3],[3,4],[4,5]]
	Output: 2

# Example 4:  
	Input: points = [[1,2]]
	Output: 1

# Example 5:  
	Input: points = [[2,3],[2,3]]
	Output: 1

# Constraints:  
- <font color="red">0 <= points.length <= 10^4</font>
- <font color="red">points.length == 2</font>
- <font color="red">-2^31 <= x_start < x_end <= 2^31 - 1</font>

______________________  

# Solution

Time complexity : O(nlog(n))  
Space complexity : O(1)  

	class Solution {
	public:
	    int findMinArrowShots(vector<vector<int>>& points) {
	        if (0 == points.size()) return 0;
	        sort(points.begin(), points.end(),
	             [](vector<int>& a, vector<int>& b) {
	                return a[1] < b[1];
	            });
	        int cur_end = points[0][1], ans = 1;
	        for (int i=1; i<points.size(); ++i) {
	            if (cur_end < points[i][0]) {
	                ++ans;
	                cur_end = points[i][1];
	            }
	        }
	        return ans;
	    }
	};

將所有的氣球，依據結束位置由小至大排序。  
再每結束位置之內，都射一發箭，即可。