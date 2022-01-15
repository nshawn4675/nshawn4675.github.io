---
layout: post
title: "[LeetCode February Challange] Day 20 - Roman to Integer"
date: 2021-02-20 00:00:00 +0800
categories: LeetCode
tags: [Easy, Hash Table, Math, String, Boblox, Amazon, Apple, Microsoft, Adobe, Qualtrics, Oracle, Google, Uber, Goldman Sachs, eBay, C++]
---
Roman numerals are represented by seven different symbols: <font color="red">I</font>, <font color="red">V</font>, <font color="red">X</font>, <font color="red">L</font>, <font color="red">C</font>, <font color="red">D</font> and <font color="red">M</font>.

	Symbol       Value
	I             1
	V             5
	X             10
	L             50
	C             100
	D             500
	M             1000

For example, <font color="red">2</font> is written as <font color="red">II</font> in Roman numeral, just two one's added together. <font color="red">12</font> is written as <font color="red">XII</font>, which is simply <font color="red">X + II</font>. The number <font color="red">27</font> is written as <font color="red">XXVII</font>, which is <font color="red">XX + V + II</font>.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not <font color="red">IIII</font>. Instead, the number four is written as <font color="red">IV</font>. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as <font color="red">IX</font>. There are six instances where subtraction is used:

- **<font color="red">I</font>** can be placed before <font color="red">V</font> (5) and <font color="red">X</font> (10) to make 4 and 9. 
- **<font color="red">X</font>** can be placed before <font color="red">L</font> (50) and <font color="red">C</font> (100) to make 40 and 90. 
- **<font color="red">C</font>** can be placed before <font color="red">D</font> (500) and <font color="red">M</font> (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer.

# Example 1:

	Input: s = "III"
	Output: 3

# Example 2:

	Input: s = "IV"
	Output: 4

# Example 3:

	Input: s = "IX"
	Output: 9

# Example 4:

	Input: s = "LVIII"
	Output: 58
	Explanation: L = 50, V= 5, III = 3.

# Example 5:

	Input: s = "MCMXCIV"
	Output: 1994
	Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.

# Constraints:

- <font color="red">1 <= s.length <= 15</font>
- **<font color="red">s</font>** contains only the characters <font color="red">('I', 'V', 'X', 'L', 'C', 'D', 'M')</font>.
- It is **guaranteed** that <font color="red">s</font> is a valid roman numeral in the range <font color="red">[1, 3999]</font>.

______________________  

# Solution  

Time complexity : O(1)  
Space complexity : O(1)  

	class Solution {
	public:
	    int romanToInt(string s) {
	        const int n = s.size();
	        unordered_map<char, int> ht;
	        ht['I'] = 1;
	        ht['V'] = 5;
	        ht['X'] = 10;
	        ht['L'] = 50;
	        ht['C'] = 100;
	        ht['D'] = 500;
	        ht['M'] = 1000;
	        
	        int ans = ht[s[n-1]];
	        for (int i=s.size()-2; 0<=i; --i) {
	            if (ht[s[i]] < ht[s[i+1]])
	                ans -= ht[s[i]];
	            else
	                ans += ht[s[i]];
	        }
	        return ans;
	    }
	};