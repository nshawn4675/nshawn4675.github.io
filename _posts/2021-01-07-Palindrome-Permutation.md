---
layout: post
title:  "Palindrome Permutation"
date:   2021-01-07 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Hash Table, Facebook, Microsoft]
---
Given a string, determine if a permutation of the string could form a palindrome.

# Example 1:

	Input: "code"
	Output: false

# Example 2:

	Input: "aab"
	Output: true

# Example 3:

	Input: "carerac"
	Output: true

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    bool canPermutePalindrome(string s) {
	        bitset<256> b;
	        for (char c: s) b.flip(c);
	        return b.count() < 2;
	    }
	};

Ascii 最多 256 個，根據每個 char ，用一個 bool 記錄當前為止是否為奇數個。  
最後的加總意思為：奇數個的 char 個數。