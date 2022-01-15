---
layout: post
title: "[LeetCode January Challange] Day 19 - Longest Palindromic Substring"
date: 2021-01-19 00:00:00 +0800
categories: LeetCode
tags: [Medium, String, Dynamic Programming, Amazon, Microsoft, Goldman Sachs, Google, Facebook, Bloomberg, Adobe, Apple, eBay, Oracle, Yandex, tcs, C++]
---
Given a string <font color="red">s</font>, return *the longest palindromic substring* in <font color="red">s</font>.

# Example 1:

	Input: s = "babad"
	Output: "bab"
	Note: "aba" is also a valid answer.

# Example 2:

	Input: s = "cbbd"
	Output: "bb"

# Example 3:

	Input: s = "a"
	Output: "a"

# Example 4:

	Input: s = "ac"
	Output: "a"

# Constraints:

- <font color="red">1 <= s.length <= 1000</font>
- **<font color="red">s</font>** consist of only digits and English letters (lower-case and/or upper-case),

______________________  

# Solution  

Time complexity : O(n^2)  
Space complexity : O(1)  

	class Solution {
	public:
	    string longestPalindrome(string s) {
	        int start = 0;
	        int maxlen = 0;
	        for (int i=0; i<s.size(); ++i) {
	            int curLen = max(calPalinLen(s, i, i), 
	                             calPalinLen(s, i, i+1));
	            if (maxlen < curLen) {
	                maxlen = curLen;
	                start = i - (maxlen-1)/2;
	            }
	        }
	        
	        return s.substr(start, maxlen);
	    }
	private:
	    int calPalinLen(const string &s, int l, int r) {
	        while (0 <= l && r < s.size() && s[l] == s[r]) {
	            --l;
	            ++r;
	        }
	        return (r-1)-(l+1)+1;
	    }
	};

從頭到尾，每個字或與下一個字當中間，向外擴散，找最長的 palindrome。