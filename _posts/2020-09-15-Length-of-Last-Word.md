---
layout: post
title:  "[LeetCode September Challange]Day15-Length of Last Word"
date:   2020-09-15 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, String]
---
Given a string *s* consists of upper/lower-case alphabets and empty space characters **<font color="red">' '</font>**, return the length of last word (last word means the last appearing word if we loop from left to right) in the string.  

If the last word does not exist, return 0.  

**Note:** A word is defined as a **maximal substring** consisting of non-space characters only.

# Example:  
	Input: "Hello World"
	Output: 5

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)

頭→尾

	class Solution {
	public:
	    int lengthOfLastWord(string s) {
	        istringstream iss(s);
	        string str;
	        int res = 0;
	        
	        while (iss >> str)
	            res = str.length();
	        
	        return res;
	    }
	};

頭←尾

	class Solution {
	public:
	    int lengthOfLastWord(string s) {
	        int res = 0, idx=s.length()-1;
	        while (0<=idx && s[idx] == ' ') --idx;
	        while (0<=idx && s[idx] != ' ') {
	            --idx;
	            ++res;
	        }
	        return res;
	    }
	};