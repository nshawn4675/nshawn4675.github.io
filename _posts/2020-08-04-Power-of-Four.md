---
layout: post
title:  "[LeetCode August Challange]Day4-Power of Four"
date:   2020-08-04 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given an integer (signed 32 bits), write a function to check whether it is a power of 4.

# Example 1:  
	Input: 16
	Output: true

# Example 2:  
	Input: 5
	Output: false

**Follow up**: Could you solve it without loops/recursion?

______________________  

# solution

Time complexity : O(1)  
Space complexity : O(1)

	class Solution {
	public:
	    bool isPowerOfFour(int num) {
	        return (num>0) && !(num&(num-1)) && (num & 0x55555555);
	    }
	};

判斷是否為4的次方：  
1. num > 0
2. (num&(num-1)) == 0的話是2的次方。(或是num==(num&-num))
3. 因為4是2的次方，又只出現在奇數bit，因此與0x55555555 & 看是否>0。