---
layout: post
title:  "[LeetCode January Challange] Day 13 - Boats to Save People"
date:   2021-01-13 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Two Pointers, Greedy, Roblox]
---
The <font color="red">i</font>-th person has weight <font color="red">people[i]</font>, and each boat can carry a maximum weight of <font color="red">limit</font>.

Each boat carries at most 2 people at the same time, provided the sum of the weight of those people is at most <font color="red">limit</font>.

Return the minimum number of boats to carry every given person.  (It is guaranteed each person can be carried by a boat.)

# Example 1:

	Input: people = [1,2], limit = 3
	Output: 1
	Explanation: 1 boat (1, 2)

# Example 2:

	Input: people = [3,2,2,1], limit = 3
	Output: 3
	Explanation: 3 boats (1, 2), (2) and (3)

# Example 3:

	Input: people = [3,5,3,4], limit = 5
	Output: 4
	Explanation: 4 boats (3), (3), (4), (5)

# Note:
- <font color="red">1 <= people.length <= 50000</font>
- <font color="red">1 <= people[i] <= limit <= 30000</font>

______________________  

# Solution  

Time complexity : O(nlogn)  
Space complexity : O(1)  

	class Solution {
	public:
	    int numRescueBoats(vector<int>& people, int limit) {
	        sort(people.rbegin(), people.rend());
	        int ans = 0;
	        for (int i=0, j=people.size()-1; i<=j; ++i) {
	            ++ans;
	            if (i == j) break;
	            if (people[i] + people[j] <= limit)
	                --j;
	        }
	        return ans;
	    }
	};

將體重由大→小排序，每次由最重的先裝，若還裝的下最輕的，就進去。