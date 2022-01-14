---
layout: post
title:  "[LeetCode October Challange] Day 11 - Remove Duplicate Letters"
date:   2020-10-11 00:00:00 +0800
categories: LeetCode
tags: [Medium, String, Stack, Greedy, Monotonic Stack, Amazon, ByteDance, C++]
---
Given a string <font color="red">s</font>, remove duplicate letters so that every letter appears once and only once. You must make sure your result is **the smallest in lexicographical order** among all possible results.  

**Note:** This question is the same as [1081](https://leetcode.com/problems/smallest-subsequence-of-distinct-characters/)  

# Example 1:  
	Input: s = "bcabc"
	Output: "abc"

# Example 2:  
	Input: s = "cbacdcbc"
	Output: "acdb"

# Constraints:  
- <font color="red">1 <= s.length <= 10^4</font>
- **<font color="red">s</font>** consists of lowercase English letters.

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    string removeDuplicateLetters(string s) {
	        string ans = "";
	        int alpha_cnt[128]={0};
	        for (char c: s)
	            ++alpha_cnt[c];
	        for (char c: s) {
	            if (ans.find(c) != string::npos) {
	                --alpha_cnt[c];
	                continue;
	            }
	            while (c < ans.back() && 0 < alpha_cnt[ans.back()]) {
	                ans.pop_back();
	            }
	            ans.push_back(c);
	            --alpha_cnt[c];
	        }
	        return ans;
	    }
	};

題目要求，給定一字串，呈現各字母都只出現1次的字串，且順序要in-place。  

先計算各字母出現的頻率，再遍歷原字串。  

若目前檢查的字母c，已出現在答案中，則跳過。  
否則，檢查答案最後一個字母是否大於c，且該字母後面還會再出現，則將其移除。  
根據上步，已找到c的合適位置，將其插入。