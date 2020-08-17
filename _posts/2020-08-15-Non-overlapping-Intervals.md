---
layout: post
title:  "[LeetCode August Challange]Day15-Non-overlapping Intervals"
date:   2020-08-15 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given a collection of intervals, find the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

# Example 1:  
	Input: [[1,2],[2,3],[3,4],[1,3]]
	Output: 1
	Explanation: [1,3] can be removed and the rest of intervals are non-overlapping.

# Example 2:  
	Input: [[1,2],[1,2],[1,2]]
	Output: 2
	Explanation: You need to remove two [1,2] to make the rest of intervals non-overlapping.

# Example 3:  
	Input: [[1,2],[2,3]]
	Output: 0
	Explanation: You don't need to remove any of the intervals since they're already non-overlapping.

# Note:  
1. You may assume the interval's end point is always bigger than its start point.
2. Intervals like [1,2] and [2,3] have borders "touching" but they don't overlap each other.

______________________  

# solution

Time complexity : O(nlogn)  
Space complexity : O(1)

	class Solution {
	public:
	    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
	        int n = intervals.size();

	        sort(intervals.begin(), intervals.end(), 
	             [](vector<int>& a, vector<int>& b) { return a[1] < b[1]; });

	        int res = 0, x = 0;
	        for (int i=1; i<n; ++i) {
	            if (intervals[i][0] < intervals[x][1]) ++res;
	            else x = i;
	        }

	        return res;
	    }
	};

首先對給定的時段，依據**結束時間點**小→大排序，會根據結束時間點排序的原因是，越早結束，越有多餘的時間排入下一個時間段。若用開始時間排序的話，有可能會得到一段很早開始、**很晚結束**的時間段。  

再來是依據這個排序好的結果，取第一段做標記(x)，標記(x)的用意是代表那段是不會重疊的時間段。  
從第二個時間段開始與x比較，其開始時間是否小於x？是的話即為重疊，重疊時間段數量結果+1，換下一位，不是的話即為未重覆且為剩餘時間段結束時間最早的，標記它為x，做到結束。  