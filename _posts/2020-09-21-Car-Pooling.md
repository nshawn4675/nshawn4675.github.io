---
layout: post
title:  "[LeetCode September Challange]Day21-Car Pooling"
date:   2020-09-21 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Sorting, Heap (Priority Queue), Simulation, Prefix Sum, C++]
---
You are driving a vehicle that has <font color="red">capacity</font> empty seats initially available for passengers.  The vehicle **only** drives east (ie. it **cannot** turn around and drive west.)  

Given a list of <font color="red">trips</font>, <font color="red">trip[i] = [num_passengers, start_location, end_location]</font> contains information about the <font color="red">i</font>-th trip: the number of passengers that must be picked up, and the locations to pick them up and drop them off.  The locations are given as the number of kilometers due east from your vehicle's initial location.  

Return <font color="red">true</font> if and only if it is possible to pick up and drop off all passengers for all the given trips.  

# Example 1:  
	Input: trips = [[2,1,5],[3,3,7]], capacity = 4
	Output: false

# Example 2:  
	Input: trips = [[2,1,5],[3,3,7]], capacity = 5
	Output: true

# Example 3:  
	Input: trips = [[2,1,5],[3,5,7]], capacity = 3
	Output: true

# Example 4:  
	Input: trips = [[3,2,7],[3,7,9],[8,3,9]], capacity = 11
	Output: true

# Constraints:  
1. <font color="red">trips.length <= 1000</font>
2. <font color="red">trips[i].length == 3</font>
3. <font color="red">1 <= trips[i][0] <= 100</font>
4. <font color="red">0 <= trips[i][1] < trips[i][2] <= 1000</font>
5. <font color="red">1 <= capacity <= 100000</font>

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1001)  

	class Solution {
	public:
	    bool carPooling(vector<vector<int>>& trips, int capacity) {
	        vector<int> delta(1001, 0);
	        
	        for (const auto& trip: trips) {
	            delta[trip[1]] -= trip[0];
	            delta[trip[2]] += trip[0];
	        }
	        
	        for (const int d: delta)
	            if ((capacity += d) < 0)
	                return false;
	        
	        return true;
	    }
	};

記錄每一站(最多1000站)，的乘客變化，即該站總共上車多少人、下車多少人。  

從頭，用初始容量，一站一站去接受載客量變化，若途中容量為負，則返回false。  

若一切順利，返回true。