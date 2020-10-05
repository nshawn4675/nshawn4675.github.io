---
layout: post
title:  "[LeetCode October Challange] Day 5 - Complement of Base 10 Integer"
date:   2020-10-05 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Math, Cloudera]
---
Every non-negative integer <font color="red">N</font> has a binary representation.  For example, <font color="red">5</font> can be represented as <font color="red">"101"</font> in binary, <font color="red">11</font> as <font color="red">"1011"</font> in binary, and so on.  Note that except for <font color="red">N = 0</font>, there are no leading zeroes in any binary representation.  

The *complement* of a binary representation is the number in binary you get when changing every <font color="red">1</font> to a <font color="red">0</font> and <font color="red">0</font> to a <font color="red">1</font>.  For example, the complement of <font color="red">"101"</font> in binary is <font color="red">"010"</font> in binary.  

For a given number <font color="red">N</font> in base-10, return the complement of it's binary representation as a base-10 integer.  

# Example 1:  
	Input: 5
	Output: 2
	Explanation: 5 is "101" in binary, with complement "010" in binary, which is 2 in base-10.

# Example 2:  
	Input: 7
	Output: 0
	Explanation: 7 is "111" in binary, with complement "000" in binary, which is 0 in base-10.

# Example 3:  
	Input: 10
	Output: 5
	Explanation: 10 is "1010" in binary, with complement "0101" in binary, which is 5 in base-10.

# Note:  
1. <font color="red">0 <= N < 10^9</font>
2. This question is the same as [476](https://leetcode.com/problems/number-complement/).

______________________  

# Solution

Time complexity : O(1)  
Space complexity : O(1)  

	class Solution {
	public:
	    int bitwiseComplement(int N) {
	        if (0 == N) return 1;
	        int mask = N;
	        for (int i=1; i<=16; i*=2)
	            mask |= mask >> i;
	        return mask^N;
	    }
	};