---
layout: post
title:  "[LeetCode September Challange]Day23-Gas Station"
date:   2020-09-23 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Greedy, Amazon, Microsoft, Google, Uber, Apple, C++]
---
There are *N* gas stations along a circular route, where the amount of gas at station *i* is <font color="red">gas[i]</font>.  

You have a car with an unlimited gas tank and it costs <font color="red">cost[i]</font> of gas to travel from station *i* to its next station (*i*+1). You begin the journey with an empty tank at one of the gas stations.  

Return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1.  

# Note:  
- If there exists a solution, it is guaranteed to be unique.
- Both input arrays are non-empty and have the same length.
- Each element in the input arrays is a non-negative integer.

# Example 1:  
	Input: 
	gas  = [1,2,3,4,5]
	cost = [3,4,5,1,2]

	Output: 3

	Explanation:
	Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
	Travel to station 4. Your tank = 4 - 1 + 5 = 8
	Travel to station 0. Your tank = 8 - 2 + 1 = 7
	Travel to station 1. Your tank = 7 - 3 + 2 = 6
	Travel to station 2. Your tank = 6 - 4 + 3 = 5
	Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.
	Therefore, return 3 as the starting index.

# Example 2:  
	Input: 
	gas  = [2,3,4]
	cost = [3,4,3]

	Output: -1

	Explanation:
	You can't start at station 0 or 1, as there is not enough gas to travel to the next station.
	Let's start at station 2 and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
	Travel to station 0. Your tank = 4 - 3 + 2 = 3
	Travel to station 1. Your tank = 3 - 3 + 3 = 3
	You cannot travel back to station 2, as it requires 4 unit of gas but you only have 3.
	Therefore, you can't travel around the circuit once no matter where you start.

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
	        int cur_tank, total_tank, start_station;
	        cur_tank = total_tank = start_station = 0;
	        
	        for (int i=0; i<gas.size(); ++i) {
	            int d = gas[i] - cost[i];
	            total_tank += d;
	            cur_tank += d;
	            if (cur_tank < 0) {
	                start_station = i + 1;
	                cur_tank = 0;
	            }
	        }
	        
	        return total_tank < 0 ? -1 : start_station;
	    }
	};

total_tank用來計算「總加油-總秏油」，若total_tank<0，代表入不敷出。  

cur_tank代表從start_station到目前加油站，油箱的量。  
若循訪過程中，cur_tank<0，代表以目前的start_station來說是不可能走完全程的，再用下一站試試看。