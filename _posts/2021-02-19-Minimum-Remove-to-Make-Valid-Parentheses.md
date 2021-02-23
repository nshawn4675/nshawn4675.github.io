---
layout: post
title:  "[LeetCode February Challange] Day 19 - Minimum Remove to Make Valid Parentheses"
date:   2021-02-19 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, String, Stack, Facebook, ByteDance, Bloomberg, Amazon, Goldman Sachs, LinkedIn]
---
Given a string s of <font color="red">'('</font> , <font color="red">')'</font> and lowercase English characters. 

Your task is to remove the minimum number of parentheses ( <font color="red">'('</font> or <font color="red">')'</font>, in **any** positions ) so that the resulting parentheses string is valid and return any valid string.

Formally, a *parentheses string* is valid if and only if:

- It is the empty string, contains only lowercase characters, or
- It can be written as <font color="red">AB</font> (<font color="red">A</font> concatenated with <font color="red">B</font>), where <font color="red">A</font> and <font color="red">B</font> are valid strings, or
- It can be written as <font color="red">(A)</font>, where <font color="red">A</font> is a valid string.

# Example 1:

	Input: s = "lee(t(c)o)de)"
	Output: "lee(t(c)o)de"
	Explanation: "lee(t(co)de)" , "lee(t(c)ode)" would also be accepted.

# Example 2:

	Input: s = "a)b(c)d"
	Output: "ab(c)d"

# Example 3:

	Input: s = "))(("
	Output: ""
	Explanation: An empty string is also valid.

# Example 4:

	Input: s = "(a(b(c)d)"
	Output: "a(b(c)d)"

# Constraints:

- <font color="red">1 <= s.length <= 10^5</font>
- **<font color="red">s[i]</font>** is one of  <font color="red">'('</font> , <font color="red">')'</font> and lowercase English letters.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    string minRemoveToMakeValid(string s) {
	        int close = count(s.begin(), s.end(), ')');
	        int open = 0;
	        
	        string ans;
	        for (char c: s) {
	            if (c == '(') {
	                if (close <= open)
	                    continue;
	                ++open;
	            } else if (c ==')') {
	                --close;
	                if (open <= 0)
	                    continue;
	                --open;
	            }
	            ans += c;
	        }
	        return ans;
	    }
	};