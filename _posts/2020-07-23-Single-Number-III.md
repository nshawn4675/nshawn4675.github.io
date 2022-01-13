---
layout: post
title:  "[LeetCode July Challange]Day23-Single Number III"
date:   2020-07-23 00:00:00 +0800
categories: LeetCode
tags: [Array, Bit Manipulation, C++]
---
Given an array of numbers **nums**, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

# Example:  
	Input:  [1,2,1,3,2,5]
	Output: [3,5]

# Note:  
1. The order of the result is not important. So in the above example, **[5, 3]** is also correct.  
2. Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?  

______________________  

# solution
time complexity : O(n)  
space complexity : O(1)

	class Solution {
	public:
	    vector<int> singleNumber(vector<int>& nums) {
	        int diff = 0;
	        for (int num: nums)
	            diff ^= num;
	        diff &= -diff;
	        
	        vector<int> res = {0, 0};
	        for (int num: nums)
	            res[(num & diff) > 0] ^= num;
	        
	        return res;
	    }
	};

首先將輸入array中所有元素xor起來，由於數量為雙的元素會彼此抵銷，因此最後的結果是由剩下的那2個只出現一次且不同的數字xor得出。  

例：[1,2,1,3,2,5]，將所有元素xor起來後會是6，因為101 xor 011 = 110。  
可推論剩下的那2個數字(3和5)，在bit的觀點，他們的第2、3位元(從右數)是不同的(xor後為1)。  

因此就可以利用第2或是第3位元，將整個輸入array區分成2堆，例：第2位元是1的一堆[2,3,2]、是0的一堆[1,1,5]，那它們個別全部取xor，就會得到3和5，即為答案。  

為了計算方便以及一般化，統一取最右邊的1做為分堆點。它可以由自己和自己的負數(2's補數)取and得到，例：6 = 0110, -6 = 1010，0110 & 1010 = 0010。