---
layout: post
title:  "[LeetCode July Challange]Day5-Hamming Distance"
date:   2020-07-05 00:00:00 +0800
categories: LeetCode
tags: [Bit Manipulation, C++]
---
The [Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance) between two integers is the number of positions at which the corresponding bits are different.  

Given two integers **x** and **y**, calculate the Hamming distance.  

# Note :  
0 <= **x**, **y** <= 2^31.  

# Example :  

	Input: x = 1, y = 4  
	  
	Output: 2  
	  
	Explanation:  
	1   (0 0 0 1)  
	4   (0 1 0 0)  
	       ↑   ↑  
	  
	The above arrows point to positions where the corresponding bits are different.  

______________________  

# solution
time complexity : O(1)  
space complexity : O(1)  

	class Solution {
	public:
	    int hammingDistance(int x, int y) {
	        return __builtin_popcount(x ^ y);
	    }
	};

此題在問，計算兩數在二進位表示時，有幾個位元不同。  
做法是將兩數取xor後，即可讓相同的bit為0，不同的bit為1。  
再將xor後的數，一個bit一個bit計數，即為答案。  