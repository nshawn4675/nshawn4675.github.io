---
layout: post
title:  "[LeetCode July Challange]Day19-Add Binary"
date:   2020-07-19 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given two binary strings, return their sum (also a binary string).  

The input strings are both **non-empty** and contains only characters **1** or **0**.  

# Example 1:  
	Input: a = "11", b = "1"
	Output: "100"

# Example 2:  
	Input: a = "1010", b = "1011"
	Output: "10101"

# Constraints:  
- Each string consists only of **'0'** or **'1'** characters.
- **1 <= a.length, b.length <= 10^4**
- Each string is either **"0"** or doesn't contain any leading zero.

______________________  

# solution
time complexity : O(n)  
space complexity : O(n)

	class Solution {
	public:
	    string addBinary(string a, string b) {
	        string res;
	        int carry = 0;
	        for (int i=a.length(), j=b.length(); i>0||j>0;) {
	            int sum = carry +
	                      (i > 0 ? a[--i] - '0' : 0) +
	                      (j > 0 ? b[--j] - '0' : 0);
	            carry = sum >> 1;
	            sum &= 1;
	            res = char(sum+'0') + res;
	        }
	        
	        return carry ? '1' + res : res;
	    }
	};

由右至左，一一處理每個位元。  
carry的部份，右移1 = 除2。  
sum的部份，&1 = 取最低位元。  
運算過程要注意「字元」與「數值」在ascii上的轉換。  