---
layout: post
title:  "[LeetCode November Challange] Day 3 - Consecutive Characters"
date:   2020-11-03 00:00:00 +0800
categories: LeetCode
tags: [Easy, String, Microsoft, C++]
---
Given a string <font color="red">s</font>, the power of the string is the maximum length of a non-empty substring that contains only one unique character.  

Return **the power** of the string.  

# Example 1:  
	Input: s = "leetcode"
	Output: 2
	Explanation: The substring "ee" is of length 2 with the character 'e' only.

# Example 2:  
	Input: s = "abbcccddddeeeeedcba"
	Output: 5
	Explanation: The substring "eeeee" is of length 5 with the character 'e' only.

# Example 3:  
	Input: s = "triplepillooooow"
	Output: 5

# Example 4:  
	Input: s = "hooraaaaaaaaaaay"
	Output: 11

# Example 5:  
	Input: s = "tourist"
	Output: 1

# Constraints:  
- <font color="red">1 <= s.length <= 500</font>
- **<font color="red">s</font>** contains only lowercase English letters.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int maxPower(string s) {
	        int tmp_ans = 1;
	        int ans = 1;
	        for (int i=1; i<s.length(); ++i) {
	            tmp_ans = s[i] == s[i-1] ? ++tmp_ans : 1;
	            ans = max(tmp_ans, ans);
	        }
	        return ans;
	    }
	};