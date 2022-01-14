---
layout: post
title:  "253. Meeting Rooms II"
date:   2020-10-20 00:00:00 +0800
categories: LeetCode
tags: [Medium, Heap, Greedy, Sort, Amazon, Bloomberg, Facebook, eBay, Google, Apple, Microsoft, Yandex, Snapchat, Oracle, Roblox, C++]
---
Given an array of meeting time intervals consisting of start and end times <font color="red">[[s1,e1],[s2,e2],...]</font> \(si < ei\), find the minimum number of conference rooms required.  

# Example 1:  
	Input: [[0, 30],[5, 10],[15, 20]]
	Output: 2

# Example 2:  
	Input: [[7,10],[2,4]]
	Output: 1

**NOTE:** input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

______________________  

# Solution  

### Min-Heap  

Time complexity : O(nlog(n))  
Space complexity : O(n)  

	class Solution {
	public:
	    int minMeetingRooms(vector<vector<int>>& intervals) {
	        if (0 == intervals.size()) return 0;
	        
	        sort(intervals.begin(), intervals.end(),
	             [](vector<int>& a, vector<int>& b) {
	                 return a[0]<=b[0];
	             });
	        
	        priority_queue<int> min_heap;
	        min_heap.push(-intervals[0][1]);
	        int ans = 1;
	        for (int idx=1; idx<intervals.size(); ++idx) {
	            while (0 < min_heap.size() && intervals[idx][0] >= -min_heap.top())
	                min_heap.pop();
	            min_heap.push(-intervals[idx][1]);
	            ans = max(ans, (int)min_heap.size());
	        }
	        return ans;
	    }
	};

首先對所有meeting的開始時間，由小至大排序，一一處理。  
min heap是用來存放各個已開始meeting的結束時間，
在這邊的實現，是用max heap，但存放負的結束時間，用以達到min heap的效果。  

每次有meeting要開始時，就去檢查各個已開始的meeting是否已結束？\(剛好到結束時間或已過\)  
將用畢的房間歸還(pop掉)，再開新房間使用。  

### Chronological Ordering

Time complexity : O(nlog(n))  
Space complexity : O(n)  

	class Solution {
	public:
	    int minMeetingRooms(vector<vector<int>>& intervals) {
	        if (0 == intervals.size()) return 0;
	        
	        vector<int> start_time, end_time;
	        for (vector<int> interval: intervals) {
	            start_time.push_back(interval[0]);
	            end_time.push_back(interval[1]);
	        }
	        sort(start_time.begin(), start_time.end());
	        sort(end_time.begin(), end_time.end());
	        
	        int start_idx = 0, end_idx = 0, ans = 0;
	        while (start_idx < intervals.size()) {
	            if (end_time[end_idx] <= start_time[start_idx]) {
	            	// meeting end
	                --ans;
	                ++end_idx;
	            }
	            // meeting start
	            ++ans;
	            ++start_idx;
	        }
	        return ans;
	    }
	};

個別將start、end時間小至大排序。  
每一次有meeting要開始時，看看有沒有結束的房間可以使用。  