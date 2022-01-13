---
layout: post
title:  "[LeetCode September Challange]Day19-Sequential Digits"
date:   2020-09-19 00:00:00 +0800
categories: LeetCode
tags: [Medium, Enumeration, C++]
---
An integer has *sequential digits* if and only if each digit in the number is one more than the previous digit.  

Return a **sorted** list of all the integers in the range <font color="red">[low, high]</font> inclusive that have sequential digits.  

# Example 1:  
	Input: low = 100, high = 300
	Output: [123,234]

# Example 2:  
	Input: low = 1000, high = 13000
	Output: [1234,2345,3456,4567,5678,6789,12345]

# Constraints:  
- <font color="red">10 <= low <= high <= 10^9</font>

______________________  

# Solution

Time complexity : O(1) (at most 64 time)  
Space complexity : O(1) (at most 36 nums)  

	class Solution {
	public:
	    vector<int> sequentialDigits(int low, int high) {
	        string sample = "123456789";
	        vector<int> ans;
	        int low_digits = to_string(low).length();
	        int high_digits = to_string(high).length();
	        
	        for (int len = low_digits; len <= high_digits; ++len) {
	            for (int start=0; start<=(9-len); ++start) {
	                int num = stoi(sample.substr(start, len));
	                if (low <= num && num <= high)
	                    ans.push_back(num);
	            }
	        }
	        
	        return ans;
	    }
	};