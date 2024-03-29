---
layout: post
title: "[LeetCode February Challange] Day 1 - Number of 1 Bits"
date: 2021-02-01 00:00:00 +0800
categories: LeetCode
tags: [Medium, Bit Manipulation, Facebook, Google, Amazon, Bloomberg, Microsoft, Adobe, ByteDance, Uber, Apple, Flipkart, Salesforce, FactSet, C++]
---
Write a function that takes an unsigned integer and returns the number of '1' bits it has (also known as the [Hamming weight](http://en.wikipedia.org/wiki/Hamming_weight)).

# Note:

- Note that in some languages such as Java, there is no unsigned integer type. In this case, the input will be given as a signed integer type. It should not affect your implementation, as the integer's internal binary representation is the same, whether it is signed or unsigned.
- In Java, the compiler represents the signed integers using [2's complement notation](https://en.wikipedia.org/wiki/Two%27s_complement). Therefore, in **Example 3** above, the input represents the signed integer. <font color="red">-3</font>.

**Follow up:** If this function is called many times, how would you optimize it?

# Example 1:

	Input: n = 00000000000000000000000000001011
	Output: 3
	Explanation: The input binary string 00000000000000000000000000001011 has a total of three '1' bits.

# Example 2:

	Input: n = 00000000000000000000000010000000
	Output: 1
	Explanation: The input binary string 00000000000000000000000010000000 has a total of one '1' bit.

# Example 3:

	Input: n = 11111111111111111111111111111101
	Output: 31
	Explanation: The input binary string 11111111111111111111111111111101 has a total of thirty one '1' bits.

# Constraints:

- The input must be a **binary string** of length <font color="red">32</font>

______________________  

# Solution  

# Bit operation

Time complexity : O(log n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int hammingWeight(uint32_t n) {
	        int ans = 0;
	        while (0 < n) {
	            ans += n & 1;
	            n >>= 1;
	        }
	        return ans;
	    }
	};

# Built-in function

Time complexity : O(log n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int hammingWeight(uint32_t n) {
	        return __builtin_popcount(n);
	    }
	};