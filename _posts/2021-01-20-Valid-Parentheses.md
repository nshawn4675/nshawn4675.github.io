---
layout: post
title:  "[LeetCode January Challange] Day 20 - Valid Parentheses"
date:   2021-01-20 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, String, Dynamic Programming, Amazon, Microsoft, Goldman Sachs, Google, Facebook, Bloomberg, Adobe, Apple, eBay, Oracle, Yandex, tcs]
---
Given a string <font color="red">s</font> containing just the characters <font color="red">'('</font>, <font color="red">')'</font>, <font color="red">'{'</font>, <font color="red">'}'</font>, <font color="red">'['</font> and <font color="red">']'</font>, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

# Example 1:

	Input: s = "()"
	Output: true

# Example 2:

	Input: s = "()[]{}"
	Output: true

# Example 3:

	Input: s = "(]"
	Output: false

# Example 4:

	Input: s = "([)]"
	Output: false

# Example 5:

	Input: s = "{[]}"
	Output: true

# Constraints:

- <font color="red">1 <= s.length <= 10^4</font>
- **<font color="red">s</font>** consists of parentheses only <font color="red">'()[]{}'</font>.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    bool isValid(string s) {
	        stack<char> stk;
	        for (char c: s) {
	            switch (c) {
	                case '(': stk.push(')'); break;
	                case '[': stk.push(']'); break;
	                case '{': stk.push('}'); break;
	                default:
	                    if (stk.empty() || c != stk.top()) return false;
	                    else stk.pop();
	            }
	        }
	        return stk.empty();
	    }
	};