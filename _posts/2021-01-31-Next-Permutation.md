---
layout: post
title:  "[LeetCode January Challange] Day 31 - Next Permutation"
date:   2021-01-31 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Array, Facebook, Google, Amazon, Bloomberg, Microsoft, Adobe, ByteDance, Uber, Apple, Flipkart, Salesforce, FactSet]
---
Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such an arrangement is not possible, it must rearrange it as the lowest possible order (i.e., sorted in ascending order).

The replacement must be [in place](http://en.wikipedia.org/wiki/In-place_algorithm) and use only constant extra memory.

# Example 1:

	Input: nums = [1,2,3]
	Output: [1,3,2]

# Example 2:

	Input: nums = [3,2,1]
	Output: [1,2,3]

# Example 3:

	Input: nums = [1,1,5]
	Output: [1,5,1]

# Example 4:

	Input: nums = [1]
	Output: [1]

# Constraints:

- <font color="red">1 <= nums.length <= 100</font>
- <font color="red">0 <= nums[i] <= 100</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    void nextPermutation(vector<int>& nums) {
	        int i=(nums.size()-1) - 1;
	        while (0 <= i && nums[i]>=nums[i+1]) --i;
	        if (0 <= i) {
	            int j=nums.size()-1;
	            while (0 <= j && nums[i]>=nums[j]) --j;
	            if (0 <= j) swap(nums[i], nums[j]);
	        }
	        reverse((nums.begin()+i)+1, nums.end());
	    }
	};

一數列的排列，有著小 → 大的特性。  
123 < 132 < 213 < 231 < 312 < 321  

要找到下一個排列：
1. 希望下一個排列比當前的數大，需將後面的大數與前面的小數交換。
2. 希望下一個排列增加的幅度盡可能的小。
	1. 需由後往前處理。
	2. 將盡可能小的「大數」與前面的小數交換。(新的頭)
	3. 有了新的大數(頭)後，在其之後(尾巴)是降序，希望是升序，才符合下一個排列的性質，所以將尾巴 reverse 變為升序。

算法：
1. 由後往前找出第一個下降值的位置 i (nums[i] <= nums[i+1])。
2. 由後往前找出第一個比 nums[i] 還大的位置 j (nums[i] <= nums[j])。
3. swap(nums[i], nums[j])
4. reverse nums[i] 之後所有元素。