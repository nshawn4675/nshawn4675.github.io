---
layout: post
title:  "702. Search in a Sorted Array of Unknown Size"
date:   2020-10-23 00:00:00 +0800
categories: LeetCode
tags: [Medium, Binary Search, Microsoft, C++]
---
Given an integer array sorted in ascending order, write a function to search <font color="red">target</font> in <font color="red">nums</font>.  If <font color="red">target</font> exists, then return its index, otherwise return <font color="red">-1</font>. **However, the array size is unknown to you**. You may only access the array using an <font color="red">ArrayReader</font> interface, where <font color="red">ArrayReader.get(k)</font> returns the element of the array at index <font color="red">k</font> (0-indexed).

You may assume all integers in the array are less than <font color="red">10000</font>, and if you access the array out of bounds, <font color="red">ArrayReader.get</font> will return <font color="red">2147483647</font>.

# Example 1:  
	Input: array = [-1,0,3,5,9,12], target = 9
	Output: 4
	Explanation: 9 exists in nums and its index is 4

# Example 2:  
	Input: array = [-1,0,3,5,9,12], target = 2
	Output: -1
	Explanation: 2 does not exist in nums so return -1

# Constraints:  
- You may assume that all elements in the array are unique.
- The value of each element in the array will be in the range <font color="red">[-9999, 9999]</font>.
- The length of the array will be in the range <font color="red">[1, 10^4]</font>.

______________________  

# Solution  

Time complexity : O(log(n))  
Space complexity : O(1)  

	/**
	 * // This is the ArrayReader's API interface.
	 * // You should not implement it, or speculate about its implementation
	 * class ArrayReader {
	 *   public:
	 *     int get(int index);
	 * };
	 */

	class Solution {
	public:
	    int search(const ArrayReader& reader, int target) {
	        int l = 0, r = 1;
	        while (reader.get(r) < target) {
	            l = r;
	            r <<= 1;
	        }
	        printf("r = %d\n", r);
	        
	        while (l < r) {
	            int mid = (l+r)>>1;
	            int res = reader.get(mid);
	            if (res == target)
	                return mid;
	            if (target < res)
	                r = mid;
	            else l = mid+1;
	        }
	        
	        return reader.get(l) == target ? l : -1;
	    }
	};

流程：找出target範圍 → binary search尋找target。  

找出target範圍：window往右移，長度以2的指數成長，直到右界限值大於target。

binary search尋找target：根據上一步找出的範圍，用binary search的方式，找出target。