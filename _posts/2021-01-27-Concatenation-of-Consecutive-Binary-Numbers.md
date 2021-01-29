---
layout: post
title:  "[LeetCode January Challange] Day 27 - Concatenation of Consecutive Binary Numbers"
date:   2021-01-27 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Math, Amazon]
---
Given an integer <font color="red">n, return *the **decimal value** of the binary string formed by concatenating the binary representations of <font color="red">1</font> to <font color="red">n</font> in order, **modulo** 10^9 + 7*.

# Example 1:

	Input: n = 1
	Output: 1
	Explanation: "1" in binary corresponds to the decimal value 1. 

# Example 2:

	Input: n = 3
	Output: 27
	Explanation: In binary, 1, 2, and 3 corresponds to "1", "10", and "11".
	After concatenating them, we have "11011", which corresponds to the decimal value 27.

# Example 3:

	Input: n = 12
	Output: 505379714
	Explanation: The concatenation results in "1101110010111011110001001101010111100".
	The decimal value of that is 118505380540.
	After modulo 109 + 7, the result is 505379714.

# Constraints:

- <font color="red">1 <= n <= 10^5</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int concatenatedBinary(int n) {
	        constexpr int MOD = 1e9+7;
	        unsigned long ans = 0;
	        for (int i=1, len=0; i<=n; ++i) {
	            if ((i&(i-1))==0) ++len;
	            ans = ((ans << len) % MOD + i) % MOD;
	        }
	        return ans;
	    }
	};

len 指的是 i 用 2 進位表示的長度。  
ans 從 1 開始，左移 i 所需的 bit，取 mod 後再加上 i。