---
layout: post
title: "[LeetCode March Challange] Day 10 - Integer to Roman"
date: 2021-03-10 00:00:00 +0800
categories: LeetCode
tags: [Medium, Hash Table, Math, String, Amazon, Microsoft, Bloomberg, Adobe, Google, Apple, Oracle, C++]
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

Given an integer, convert it to a roman numeral.

# Example 1:

	Input: num = 3
	Output: "III"

# Example 2:

	Input: num = 4
	Output: "IV"

# Example 3:

	Input: num = 9
	Output: "IX"

# Example 4:

	Input: num = 58
	Output: "LVIII"
	Explanation: L = 50, V = 5, III = 3.

# Example 5:

	Input: num = 1994
	Output: "MCMXCIV"
	Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.

# Constraints:

- <font color="red">1 <= num <= 3999</font>

______________________  

# Solution  

Time complexity : O(1)  
Space complexity : O(1)  

	class Solution {
	public:
	    string intToRoman(int num) {
	        string M[] = {"", "M", "MM", "MMM"};
	        string C[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
	        string X[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
	        string I[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
	        return M[num/1000] + C[(num%1000)/100] + X[(num%100)/10] + I[num%10];
	    }
	};