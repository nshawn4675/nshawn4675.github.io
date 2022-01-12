---
layout: post
title:  "[LeetCode July Challange]Day4-Ugly Number II"
date:   2020-07-04 00:00:00 +0800
categories: LeetCode
tags: [Hash Table, Math, Dynamic Programming, Heap (Priority Queue), C++]
---
Write a program to find the **n**-th ugly number.  

Ugly numbers are **positive numbers** whose prime factors only include **2, 3, 5**.  

# Example 1:  
	Input: n = 10  
	Output: 12  
	Explanation: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.  

# Note :  
1. 1 is typically treated as an ugly number.  
2. n does not exceed 1690.  

# Hint :  
1. The naive approach is to call **isUgly** for every number until you reach the nth one. Most numbers are not ugly. Try to focus your effort on generating only the ugly ones.  
2. An ugly number must be multiplied by either 2, 3, or 5 from a smaller ugly number.  
3. The key is how to maintain the order of the ugly numbers. Try a similar approach of merging from three sorted lists: L1, L2, and L3.  
4. Assume you have Uk, the kth ugly number. Then Uk+1 must be Min(L1 * 2, L2 * 3, L3 * 5).  

______________________  

# solution
time complexity : O(n)  
space complexity : O(n)  

	class Solution {
	public:
	    int nthUglyNumber(int n) {
	        vector<int> uglyNums = {1};
	        int idx2 = 0;
	        int idx3 = 0;
	        int idx5 = 0;
	        while (uglyNums.size() < n) {
	            int next2 = uglyNums[idx2] * 2;
	            int next3 = uglyNums[idx3] * 3;
	            int next5 = uglyNums[idx5] * 5;
	            int next = min(next2, min(next3, next5));
	            if (next == next2) ++idx2;
	            if (next == next3) ++idx3;
	            if (next == next5) ++idx5;
	            uglyNums.push_back(next);
	        }
	        return uglyNums[n-1];
	    }  
	};

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/uglyNums.png?raw=true)
初始：uglyNums第一個為1。  
直到uglyNums算到第n個前，從2、3、5的倍數相對應的記錄點中乘上相對應的值，找到最小的那個，其為下一個ugly num。(因ugly num的因數只有2、3、5，因此乘上2 or 3 or 5，還是ugly num)而被選為ugly num的記錄點+1。  
最後回傳uglyNums最後一個元素，即為結果。