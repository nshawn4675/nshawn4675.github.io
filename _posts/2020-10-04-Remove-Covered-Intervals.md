---
layout: post
title:  "[LeetCode October Challange] Day 4 - Remove Covered Intervals"
date:   2020-10-04 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Array, Two Pointers, Goldman Sachs, Microsoft]
---
Given a list of <font color="red">intervals</font>, remove all intervals that are covered by another interval in the list.  

Interval <font color="red">[a,b)</font> is covered by interval <font color="red">[c,d)</font> if and only if <font color="red">c <= a</font> and <font color="red">b <= d</font>.

After doing so, return the number of *remaining intervals*.  

# Example 1:  
	Input: intervals = [[1,4],[3,6],[2,8]]
	Output: 2
	Explanation: Interval [3,6] is covered by [2,8], therefore it is removed.

# Example 2: 
	Input: intervals = [[1,4],[2,3]]
	Output: 1

# Example 3:  
	Input: intervals = [[0,10],[5,12]]
	Output: 2

# Example 4:  
	Input: intervals = [[3,10],[4,10],[5,11]]
	Output: 2

# Example 5:  
	Input: intervals = [[1,2],[1,4],[3,4]]
	Output: 1

# Constraints:  
- <font color="red">1 <= intervals.length <= 1000</font>
- <font color="red">intervals[i].length == 2</font>
- <font color="red">0 <= intervals[i][0] < intervals[i][1] <= 10^5</font>
- All the intervals are **unique**.

______________________  

# Solution

Time complexity : O(nlog(n))  
Space complexity : O(1)  

	class Solution {
	public:
	    int removeCoveredIntervals(vector<vector<int>>& intervals) {
	        sort(intervals.begin(), intervals.end(),
	             [](vector<int>& a, vector<int>& b) {
	                 return a[0]==b[0] ? a[1]>b[1] : a[0]<b[0];
	             });
	        
	        int ans = 0, end, prev_end = 0;
	        for (vector<int> interval: intervals) {
	            end = interval[1];
	            if (prev_end < end) {
	                ++ans;
	                prev_end = end;
	            }
	        }
	        return ans;
	    }
	};

用start point小至大排序，若start point相同，則較長的end point優先。  
因start point已排序，只要一個一個判斷end point是否符合被蓋住的條件即可。