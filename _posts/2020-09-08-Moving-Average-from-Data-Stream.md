---
layout: post
title:  "346. Moving Average from Data Stream"
date:   2020-09-08 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Design, Queue]
---
Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

# Example:  
	MovingAverage m = new MovingAverage(3);
	m.next(1) = 1
	m.next(10) = (1 + 10) / 2
	m.next(3) = (1 + 10 + 3) / 3
	m.next(5) = (10 + 3 + 5) / 3

______________________  

# Solution

Time complexity : O(1)  
Space complexity : O(n)

	class MovingAverage {
	public:
	    /** Initialize your data structure here. */
	    MovingAverage(int size) {
	        n = size;
	        q = new int[n]();
	        sum = cnt = front = 0;
	    }
	    
	    double next(int val) {
	        cnt = cnt < n ? ++cnt : n;
	        front = (front+1)%n;
	        sum = sum - q[front] + val;
	        q[front] = val;
	        return double(sum)/cnt;
	    }
	private:
	    int sum, n, front, cnt, *q;
	};

	/**
	 * Your MovingAverage object will be instantiated and called as such:
	 * MovingAverage* obj = new MovingAverage(size);
	 * double param_1 = obj->next(val);
	 */

使用circular queue。  
用front作為記錄新資料取代舊資料的位置，小到大循環。  
sum記錄此window中的加總。  