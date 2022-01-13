---
layout: post
title:  "[LeetCode September Challange]Day13-Insert Interval"
date:   2020-09-13 00:00:00 +0800
categories: LeetCode
tags: [Hard, Array, C++]
---
Given a set of *non-overlapping* intervals, insert a new interval into the intervals (merge if necessary).  

You may assume that the intervals were initially sorted according to their start times.  

# Example 1:  
	Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
	Output: [[1,5],[6,9]]

# Example 2:  
	Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
	Output: [[1,2],[3,10],[12,16]]
	Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].

**NOTE:** input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(n)

	class Solution {
	public:
	    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
	        vector<vector<int>> l, r;
	        int new_start = newInterval[0];
	        int new_end = newInterval[1];
	        
	        for (vector<int> interval: intervals) {
	            if (interval[1] < new_start)
	                l.push_back(interval);
	            else if (new_end < interval[0])
	                r.push_back(interval);
	            else {
	                new_start = min(new_start, interval[0]);
	                new_end = max(new_end, interval[1]);
	            }
	        }
	        
	        vector<vector<int>> res(move(l));
	        res.push_back({new_start, new_end});
	        res.insert(res.end(), r.begin(), r.end());
	        return res;
	    }
	};

將結果根據新加入的interval分為三堆：左邊、與新interval合為一體的中間、右邊。  
左邊的定義：結束時間<新interval開始時間。  
右邊的定義：新interval結束時間<開始時間。  

分完三堆後，再將其統整即可。