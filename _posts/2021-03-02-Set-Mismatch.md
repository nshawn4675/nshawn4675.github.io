---
layout: post
title: "[LeetCode March Challange] Day 02 - Set Mismatch"
date: 2021-03-02 00:00:00 +0800
categories: LeetCode
tags: [Easy, Array, Hash Table, Bit Manipulation, Sorting, Apple, Amazon, C++]
---
You have a set of integers <font color="red">s</font>, which originally contains all the numbers from <font color="red">1</font> to <font color="red">n</font>. Unfortunately, due to some error, one of the numbers in <font color="red">s</font> got duplicated to another number in the set, which results in **repetition of one** number and **loss of another** number.

You are given an integer array <font color="red">nums</font> representing the data status of this set after the error.

Find the number that occurs twice and the number that is missing and return *them in the form of an array*.

# Example 1:

	Input: nums = [1,2,2,4]
	Output: [2,3]

# Example 2:

	Input: nums = [1,1]
	Output: [1,2]

# Constraints:

- <font color="red">2 <= nums.length <= 10^4</font>
- <font color="red">1 <= nums[i] <= 10^4</font>

______________________  

# Solution  

# Marking

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    vector<int> findErrorNums(vector<int>& nums) {
	        int dup = -1, miss = -1;
	        for (int n: nums) {
	            if (nums[abs(n)-1] < 0)
	                dup = abs(n);
	            else
	                nums[abs(n)-1] *= -1;
	        }
	        for (int i=1; i<=nums.size(); ++i) {
	            if (0 < nums[i-1]) {
	                miss = i;
	                break;
	            }
	        }
	        return {dup, miss};
	    }
	};

利用變成負數來標記已見過的 num，用此找出 dup。  
再尋訪 nums 一次，若有看到未標記的(為正數)，則為 miss。


# Xor

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    vector<int> findErrorNums(vector<int>& nums) {
	        int xr = 0, xr1 = 0, xr2 = 0;
	        for (int n: nums) xr ^= n;
	        for (int i=1; i<=nums.size(); ++i) xr ^= i;
	        
	        int r_most_bit = xr & ~(xr-1);
	        for (int n: nums) {
	            if ((n & r_most_bit) != 0)
	                xr1 ^= n;
	            else
	                xr2 ^= n;
	        }
	        for (int i=1; i<=nums.size(); ++i) {
	            if ((i & r_most_bit) != 0)
	                xr1 ^= i;
	            else
	                xr2 ^= i;
	        }
	        
	        for (int n: nums) {
	            if (n == xr1)
	                return {xr1, xr2};
	        }
	        return {xr2, xr1};
	    }
	};

將 nums 及理想的 1 ~ n xor 一次，此時：
1. miss 的數會出現 1 次。
2. dup 的數會出現 3 次，但經由 xor 過程後，算 1 次(偶次數抵消)。

因此此時的 xor 值會是 miss xor dup。  
接著藉由找出最右邊的bit，做為 miss 或是 dup 的特徵。
藉由這個特徵，把 nums 和理想的 1 ~ n 分為兩組：
1. 與這個特徵有關的。(與其做 and 運算會大於0)
2. 與這個特徵無關的。(與其做 and 運算會等於0)

理想上這兩組的數量應是相等的，xor 之後應為0。  
但是我們有 miss 和 dup，因此這兩組 xor 完之後會是 miss 和 dup。  
但是哪一個是 miss，哪一個是 dup，不知道。  
所以最後再跑一次 loop，若在 nums 中被找到，即為 dup，另一個為 miss。