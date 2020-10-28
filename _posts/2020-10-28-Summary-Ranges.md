---
layout: post
title:  "[LeetCode October Challange] Day 28 - Summary Ranges"
date:   2020-10-28 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Array, Capital One]
---
You are given a **sorted unique** integer array <font color="red">nums</font>.  

Return *the **smallest sorted** list of ranges that **cover all the numbers in the array exactly***. That is, each element of <font color="red">nums</font> is covered by exactly one of the ranges, and there is no integer <font color="red">x</font> such that <font color="red">x</font> is in one of the ranges but not in <font color="red">nums</font>.  

Each range <font color="red">[a,b]</font> in the list should be output as:
- **<font color="red">"a->b"</font>** if <font color="red">a != b</font>
- **<font color="red">"a"</font>** if <font color="red">a == b</font>


# Example 1:  
	Input: nums = [0,1,2,4,5,7]
	Output: ["0->2","4->5","7"]
	Explanation: The ranges are:
	[0,2] --> "0->2"
	[4,5] --> "4->5"
	[7,7] --> "7"

# Example 2:  
	Input: nums = [0,2,3,4,6,8,9]
	Output: ["0","2->4","6","8->9"]
	Explanation: The ranges are:
	[0,0] --> "0"
	[2,4] --> "2->4"
	[6,6] --> "6"
	[8,9] --> "8->9"

# Example 3:  
	Input: nums = []
	Output: []

# Example 4:  
	Input: nums = [-1]
	Output: ["-1"]

# Example 5:  
	Input: nums = [0]
	Output: ["0"]

# Constraints:  
- <font color="red">0 <= nums.length <= 20</font>
- <font color="red">-2^31 <= nums[i] <= 2^31 - 1</font>
- All the values of <font color="red">nums</font> are **unique**.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    vector<string> summaryRanges(vector<int>& nums) {
	        vector<string> ans = {};
	        const int n = nums.size();
	        
	        for (int start=0, end=1; end<=n; ++end) {
	            if (end == n || nums[end-1] != nums[end]-1) {
	                if (start == end-1)
	                    ans.push_back(to_string(nums[start]));
	                else
	                    ans.push_back(to_string(nums[start])+"->"+to_string(nums[end-1]));
	                start = end;
	            }
	        }
	        return ans;
	    }
	};

考慮目前的end與上一個是否差1，  
若不是的話要切斷，  
切斷時若start與end是同一個，就只要start即可，  
切斷時若start與end是不同的，就要start->end-1。