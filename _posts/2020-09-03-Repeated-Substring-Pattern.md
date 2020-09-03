---
layout: post
title:  "[LeetCode September Challange]Day3-Repeated Substring Pattern"
date:   2020-09-03 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given a non-empty string check if it can be constructed by taking a substring of it and appending multiple copies of the substring together. You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.  

# Example 1:  
	Input: "abab"
	Output: True
	Explanation: It's the substring "ab" twice.

# Example 2:  
	Input: "aba"
	Output: False

# Example 3:  
	Input: "abcabcabcabc"
	Output: True
	Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(n)

	class Solution {
	public:
	    bool repeatedSubstringPattern(string s) {
	        return (s+s).find(s, 1) < s.size();
	    }
	};

題目是說，判斷一字串是否為某一pattern重覆n次所組成：string = pattern+pattern+...+pattern。  
我們將原字串重覆一次，從第二個位置開始find自己，若：
1. 原字串不符合題目所述，則此find一定會找到第二個自己。例：new_string=string+「string」
2. 原字串符合題目所述，則此find一定會在找到第二個自己之前，找到自己。例：origin_str=pattern+pattern，new_string=pattern+「pattern+pattern」+pattern