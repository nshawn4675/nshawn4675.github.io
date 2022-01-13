---
layout: post
title:  "[LeetCode September Challange]Day25-Largest Number"
date:   2020-09-25 00:00:00 +0800
categories: LeetCode
tags: [Medium, String, Greedy, Sorting, Microsoft, Apple, Facebook, Amazon, Adobe, ByteDance, C++]
---
Given a list of non negative integers, arrange them such that they form the largest number.

# Example 1:  
	Input: [10,2]
	Output: "210"

# Example 2:  
	Input: [3,30,34,5,9]
	Output: "9534330"

**Note:** The result may be very large, so you need to return a string instead of an integer.

______________________  

# Solution

Time complexity : O(nlogn)  
Space complexity : O(n)  

	class Solution {
	public:
	    string largestNumber(vector<int>& nums) {
	        if (0 == nums.size()) return "0";
	        
	        vector<string> strs;
	        for (int n: nums)
	            strs.push_back(to_string(n));
	        
	        sort(strs.begin(), strs.end(), [](string& a, string& b) {return a+b > b+a;});
	        
	        string ans;
	        for (string s: strs)
	            ans += s;
	        
	        return ans[0] == '0' ? "0" : ans;
	    }
	};

希望sort到的字串從左邊往右邊看是大→小的。  

客製一個sorting function，來符合上面的需求。  

兩兩數字串在一起，要比較大的那一個。  