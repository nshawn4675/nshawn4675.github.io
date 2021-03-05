---
layout: post
title:  "[LeetCode February Challange] Day 27 - Divide Two Integers"
date:   2021-02-27 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Math, Binary Search, Facebook, Amazon, Adobe]
---
Given two integers <font color="red">dividend</font> and <font color="red">divisor</font>, divide two integers without using multiplication, division, and mod operator.

Return the quotient after dividing <font color="red">dividend</font> by <font color="red">divisor</font>.

The integer division should truncate toward zero, which means losing its fractional part. For example, <font color="red">truncate(8.345) = 8</font> and <font color="red">truncate(-2.7335) = -2</font>.

# Note:

- Assume we are dealing with an environment that could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. For this problem, assume that your function **returns 2^31 − 1 when the division result overflows**.

# Example 1:

	Input: dividend = 10, divisor = 3
	Output: 3
	Explanation: 10/3 = truncate(3.33333..) = 3.

# Example 2:

	Input: dividend = 7, divisor = -3
	Output: -2
	Explanation: 7/-3 = truncate(-2.33333..) = -2.

# Example 3:

	Input: dividend = 0, divisor = 1
	Output: 0

# Example 4:

	Input: dividend = 1, divisor = 1
	Output: 1

# Constraints:

- <font color="red">-2^31 <= dividend, divisor <= 2^31 - 1</font>
- <font color="red">divisor != 0</font>

______________________  

# Solution  

Time complexity : O(logn)  
Space complexity : O(logn)  

	class Solution {
	public:
	    int divide(int dividend, int divisor) {
	        if (dividend == INT_MIN && divisor == -1)
	            return INT_MAX;

	        const int HALF_MIN = INT_MIN / 2;
	        
	        int negCnt = 2;
	        if (0 < dividend) {
	            negCnt -= 1;
	            dividend = -dividend;
	        }
	        if (0 < divisor) {
	            negCnt -= 1;
	            divisor = -divisor;
	        }
	        
	        int p = -1;
	        vector<int> powerOf2;
	        vector<int> divisorPowerOf2;
	        while (dividend <= divisor) {
	            powerOf2.push_back(p);
	            divisorPowerOf2.push_back(divisor);
	            if (divisor < HALF_MIN) break;
	            p += p;
	            divisor += divisor;
	        }
	        
	        int ans = 0;
	        for (int i=powerOf2.size()-1; 0<=i; --i) {
	            if (dividend <= divisorPowerOf2[i]) {
	                ans += powerOf2[i];
	                dividend -= divisorPowerOf2[i];
	            }
	        }
	        
	        return negCnt == 1 ? ans : -ans;
	    }
	};

注意：不能用「\*」、「/」、「%」，且運作在 32-bit 機器上，不可用 long long。  

特別 case：當 dividend = INT_MIN 且 divisor = -1時，ans 為INT_MAX+1，需調整為 INT_MAX。  

找出 HALF_MIN 的原因是避免後面的運算 overflow。  

記錄 dividend 和 divisor 的正負關係，用來決定最後的答案是正/負。  
同時將 dividend 及 divisor 轉到負數去做後續的計算 (可表示範圍較正數廣，避免 overflow)。

一開始的想法是不斷的將 dividend 減去 divisor，看減了多少次，但太慢。  
改善方法是 divisor 不斷的以 2 的次方增長，直到超出 dividend 為止。  
p 代表 2 的 power 次方數，也是以負數計算，避免 overflow。  

用 2 個陣列記錄可行的 2 的次方倍以及該 divisor 。  
最後再從可行的最大次方開始扣 dividend，同時將可行的倍數加到 ans 中。