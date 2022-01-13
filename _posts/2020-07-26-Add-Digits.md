---
layout: post
title:  "[LeetCode July Challange]Day26-Add Digits"
date:   2020-07-26 00:00:00 +0800
categories: LeetCode
tags: [Math, Simulation, Number Theory, C++]
---
Given a non-negative integer **num**, repeatedly add all its digits until the result has only one digit.  

# Example 1:  
	Input: 38
	Output: 2 
	Explanation: The process is like: 3 + 8 = 11, 1 + 1 = 2. 
	             Since 2 has only one digit, return it.

# Follow up:  
Could you do it without any loop/recursion in O(1) runtime?

______________________  

# solution
time complexity : O(logn)  
space complexity : O(1)

	class Solution {
	public:
	    int addDigits(int num) {
	        while (num/10 != 0) {
	            int sum = 0;
	            while (num != 0) {
	                sum += num % 10;
	                num /= 10;
	            }
	            num = sum;
	        }
	        return num;
	    }
	};

直到num位數不為1位數前，一直做：  
將各個位數加起來，取代num。

O(1)的方式，用到數根計算方法：[Digital root](https://en.wikipedia.org/wiki/Digital_root#Congruence_formula)

結論：一個n進位數的數根(digital root)，即是它對n-1的餘數。  
故10進位的數字，其數根即是它對9的餘數。  
12,345 = 1 × (9,999 + 1) + 2 × (999 + 1) + 3 × (99 + 1) + 4 × (9 + 1) + 5  
12,345 = (1 × 9,999 + 2 × 999 + 3 × 99 + 4 × 9) + (1 + 2 + 3 + 4 + 5)  

	if (num % 9 > 0)
		digital_root = num % 9;
	else if (num % 9 == 0)
		digital_root = min(num, 9); // 0 or 9

code:  

	class Solution {
	public:
	    int addDigits(int num) {
	        return num % 9 ? num % 9 : min(num, 9);
	    }
	};
