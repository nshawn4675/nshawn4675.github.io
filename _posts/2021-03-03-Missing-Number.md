---
layout: post
title: "[LeetCode March Challange] Day 03 - Missing Number"
date: 2021-03-03 00:00:00 +0800
categories: LeetCode
tags: [Easy, Array, Hash Table, Math, Bit Manipulation, Sorting, Capital One, Facebook, Amazon, Apple, Oracle, Microsoft, Goldman Sachs, Cisco, Arista Networks, C++]
---
Given an array <font color="red">nums</font> containing <font color="red">n</font> distinct numbers in the range <font color="red">[0, n]</font>, return *the only number in the range that is missing from the array*.

**Follow up:** Could you implement a solution using only <font color="red">O(1)</font> extra space complexity and <font color="red">O(n)</font> runtime complexity?

# Example 1:

	Input: nums = [3,0,1]
	Output: 2
	Explanation: n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 2 is the missing number in the range since it does not appear in nums.

# Example 2:

	Input: nums = [0,1]
	Output: 2
	Explanation: n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 2 is the missing number in the range since it does not appear in nums.

# Example 3:

	Input: nums = [9,6,4,2,3,5,7,0,1]
	Output: 8
	Explanation: n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 8 is the missing number in the range since it does not appear in nums.

# Example 4:

	Input: nums = [0]
	Output: 1
	Explanation: n = 1 since there is 1 number, so all numbers are in the range [0,1]. 1 is the missing number in the range since it does not appear in nums.

# Constraints:

- <font color="red">n == nums.length</font>
- <font color="red">1 <= n <= 10^4</font>
- <font color="red">0 <= nums[i] <= n</font>
- All the numbers of <font color="red">nums</font> are **unique**.

______________________  

# Solution  

# Missing Sum

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int missingNumber(vector<int>& nums) {
	        const int N = nums.size();
	        const int SUM = (0+N)*(N+1)/2;
	        int sum = accumulate(nums.begin(), nums.end(), 0);
	        return SUM - sum;
	    }
	};

先利用數學公式算出理想的 0 ~ n 的總和應該是要多少。  
再求出 nums 中所有元素的總和。  
兩者相減即可知道是缺少哪一個元素的值。  

# Xor

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int missingNumber(vector<int>& nums) {
	        int miss = 0;
	        for (int n: nums) miss ^= n;
	        for (int i=0; i<=nums.size(); ++i)
	            miss ^= i;
	        return miss;
	    }
	};

將 0 ~ n 和 nums 中的元素全部 xor 之後。  
除了 miss 只出現一次外，其它都出現兩次，會藉由 xor 抵消掉。  
故最後運算節果只剩下 miss。