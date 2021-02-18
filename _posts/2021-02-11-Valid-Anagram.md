---
layout: post
title:  "[LeetCode February Challange] Day 11 - Valid Anagram"
date:   2021-02-11 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Hash Table, Sort, Bloomberg, Microsoft, Facebook, Amazon, Goldman Sachs, Apple, Oracle, Paypal, Adobe, Qualcomm]
---
Given two strings s and t , write a function to determine if t is an anagram of s.

# Example 1:

	Input: s = "anagram", t = "nagaram"
	Output: true

# Example 2:

	Input: s = "rat", t = "car"
	Output: false

# Note:

You may assume the string contains only lowercase alphabets.

# Follow up:

What if the inputs contain unicode characters? How would you adapt your solution to such case?

______________________  

# Solution  

### Sorting

Time complexity : O(nlong)  
Space complexity : O(1)  

	class Solution {
	public:
	    bool isAnagram(string s, string t) {
	        sort(s.begin(), s.end());
	        sort(t.begin(), t.end());
	        return s == t;
	    }
	};


### Hash Table

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    bool isAnagram(string s, string t) {
	        unordered_map<char, int> m;
	        for (char c: s) ++m[c];
	        for (char c: t) --m[c];
	        for (auto item: m) {
	            if (item.second != 0)
	                return false;
	        }
	        return true;
	    }
	};