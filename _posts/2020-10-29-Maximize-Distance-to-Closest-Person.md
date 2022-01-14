---
layout: post
title:  "[LeetCode October Challange] Day 29 - Maximize Distance to Closest Person"
date:   2020-10-29 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Audible, Amazon, Microsoft, C++]
---
You are given an array representing a row of <font color="red">seats</font> where <font color="red">seats[i] = 1</font> represents a person sitting in the <font color="red">i-th</font> seat, and <font color="red">seats[i] = 0</font> represents that the <font color="red">i-th</font> seat is empty (0-indexed).  

There is at least one empty seat, and at least one person sitting.  

Alex wants to sit in the seat such that the distance between him and the closest person to him is maximized.  

Return *that maximum distance to the closest person*.  

# Example 1:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/849_ex.jpg?raw=true)

	Input: seats = [1,0,0,0,1,0,1]
	Output: 2
	Explanation: 
	If Alex sits in the second open seat (i.e. seats[2]), then the closest person has distance 2.
	If Alex sits in any other open seat, the closest person has distance 1.
	Thus, the maximum distance to the closest person is 2.

# Example 2:  
	Input: seats = [1,0,0,0]
	Output: 3
	Explanation: 
	If Alex sits in the last seat (i.e. seats[3]), the closest person is 3 seats away.
	This is the maximum distance possible, so the answer is 3.

# Example 3:  
	Input: seats = [0,1]
	Output: 1

# Constraints:  
- <font color="red">2 <= seats.length <= 2 * 10^4</font>
- **<font color="red">seats[i]</font>** is <font color="red">0</font> or <font color="red">1</font>.
- At least one seat is **empty**.
- At least one seat is **occupied**.

______________________  

# Solution  

**Next Array**  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    int maxDistToClosest(vector<int>& seats) {
	        const int n = seats.size();
	        vector<int> min_l_dist(n, n), min_r_dist(n, n);
	        for (int i=0; i<n; ++i) {
	            if (seats[i] == 1)
	                min_l_dist[i] = 0;
	            else if (0 < i)
	                min_l_dist[i] = min_l_dist[i-1]+1;
	        }
	        for (int i=n-1; 0<=i; --i) {
	            if (seats[i] == 1)
	                min_r_dist[i] = 0;
	            else if (i < n-1)
	                min_r_dist[i] = min_r_dist[i+1]+1;
	        }
	        
	        int ans = INT_MIN;
	        for (int i=0; i<n; ++i) {
	            if (seats[i] == 0)
	                ans = max(ans, min(min_l_dist[i], min_r_dist[i]));
	        }
	        return ans;
	    }
	};

分別記錄每個位置，離左、右邊最近一個人的距離。  
答案就是每個左右距離中最小者，取最大者。  


**Two Pointer**  

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int maxDistToClosest(vector<int>& seats) {
	        const int n = seats.size();
	        int l = -1, r = 0, ans = 0;
	        for (int i=0; i<n; ++i) {
	            if (seats[i] == 1)
	                l = i;
	            else {
	                while ((r < n && seats[r] == 0) || r < i)
	                    ++r;
	                int l_dist = l == -1 ? n : i-l;
	                int r_dist = r == n ? n : r-i;
	                ans = max(ans, min(l_dist, r_dist));
	            }
	        }
	        
	        return ans;
	    }
	};

從頭掃到尾，記錄當前位置，離左右兩旁最近有人的距離。  
一直找最大值即可。  