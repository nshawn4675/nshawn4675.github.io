---
layout: post
title:  "[LeetCode August Challange]Day27-Find Right Interval"
date:   2020-08-27 00:00:00 +0800
categories: LeetCode
tags: [Array, Binary Search, Sorting, C++]
---
Given a set of intervals, for each of the interval i, check if there exists an interval j whose start point is bigger than or equal to the end point of the interval i, which can be called that j is on the "right" of i.  

For any interval i, you need to store the minimum interval j's index, which means that the interval j has the minimum start point to build the "right" relationship for interval i. If the interval j doesn't exist, store -1 for the interval i. Finally, you need output the stored value of each interval as an array.  

# Note:  
1. You may assume the interval's end point is always bigger than its start point.
2. You may assume none of these intervals have the same start point.

# Example 1:  
	Input: [ [1,2] ]

	Output: [-1]

	Explanation: There is only one interval in the collection, so it outputs -1.

# Example 2:  
	Input: [ [3,4], [2,3], [1,2] ]

	Output: [-1, 0, 1]

	Explanation: There is no satisfied "right" interval for [3,4].
	For [2,3], the interval [3,4] has minimum-"right" start point;
	For [1,2], the interval [2,3] has minimum-"right" start point.

# Example 3:  
	Input: [ [1,4], [2,3], [3,4] ]

	Output: [-1, 2, -1]

	Explanation: There is no satisfied "right" interval for [1,4] and [3,4].
	For [2,3], the interval [3,4] has minimum-"right" start point.

**NOTE:** input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

______________________  

# solution

Time complexity : O(nlog(n))
Space complexity : O(n)

	class Solution {
	public:
	    vector<int> findRightInterval(vector<vector<int>>& intervals) {
	        int n = intervals.size();
	        vector<int> res(n);
	        map<int, int> m;
	        for (int i=0; i<n; ++i)
	            m[intervals[i][0]] = i;
	        for (int i=0; i<n; ++i) {
	            auto ptr = m.lower_bound(intervals[i][1]);
	            res[i] = ptr == m.end() ? -1 : ptr->second;
	        }
	        return res;
	    }
	};

map的索引會自動排序好，且插入只需O(log(n))時間，首先將各個interval開始時間(題目表示不重覆)插入map中，得到一個開始時間小到大，map to 相對應原輸入array中idx的位置。  

再來針對每一個interval，去找它的右區間，即開始時間大於結束時間，且為最小者，只要以結束時間為目標，在map中搜尋lower bound即可，搜尋時間O(log(n))。  

(lower bound：不低於x的最小者)  
(upper bound：不高於x的最大者)