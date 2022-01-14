---
layout: post
title:  "[LeetCode October Challange] Day 1 - Number of Recent Calls"
date:   2020-10-01 00:00:00 +0800
categories: LeetCode
tags: [Easy, Design, Queue, Data Stream, Yandex, C++]
---
You have a <font color="red">RecentCounter</font> class which counts the number of recent requests within a certain time frame.  

Implement the <font color="red">RecentCounter</font> class:  
- **<font color="red">RecentCounter()</font>** Initializes the counter with zero recent requests.
- **<font color="red">int ping(int t)</font>** Adds a new request at time <font color="red">t</font>, where <font color="red">t</font> represents some time in milliseconds, and returns the number of requests that has happened in the past <font color="red">3000</font> milliseconds (including the new request). Specifically, return the number of requests that have happened in the inclusive range <font color="red">[t - 3000, t]</font>.

It is **guaranteed** that every call to <font color="red">ping</font> uses a strictly larger value of <font color="red">t</font> than the previous call.

# Example 1:  
	Input
	["RecentCounter", "ping", "ping", "ping", "ping"]
	[[], [1], [100], [3001], [3002]]
	Output
	[null, 1, 2, 3, 3]

	Explanation
	RecentCounter recentCounter = new RecentCounter();
	recentCounter.ping(1);     // requests = [1], range is [-2999,1], return 1
	recentCounter.ping(100);   // requests = [1, 100], range is [-2900,100], return 2
	recentCounter.ping(3001);  // requests = [1, 100, 3001], range is [1,3001], return 3
	recentCounter.ping(3002);  // requests = [1, 100, 3001, 3002], range is [2,3002], return 3

# Constraints:  
- <font color="red">1 <= t <= 109</font>
- Each test case will call <font color="red">ping</font> with **strictly increasing** values of <font color="red">t</font>.
- At most <font color="red">10^4</font> calls will be made to <font color="red">ping</font>.

______________________  

# Solution

Time complexity : O(1)  
Space complexity : O(1)  

	class RecentCounter {
	public:
	    RecentCounter() {
	        
	    }
	    
	    int ping(int t) {
	        while (!q.empty() && t - q.front() > 3000) q.pop();
	      q.push(t);
	      return q.size();
	    }
	private:
	  queue<int> q;
	};

	/**
	 * Your RecentCounter object will be instantiated and called as such:
	 * RecentCounter* obj = new RecentCounter();
	 * int param_1 = obj->ping(t);
	 */