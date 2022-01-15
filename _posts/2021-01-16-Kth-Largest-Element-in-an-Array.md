---
layout: post
title: "[LeetCode January Challange] Day 16 - Kth Largest Element in an Array"
date: 2021-01-16 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Divide and Conquer, Sorting, Heap (Priority Queue), Quickselect, Facebook, Amazon, ByteDance, Walmart Labs, Apple, Microsoft, Salesforce, Google, LinkedIn, Adobe, Oracle, Expedia, Spotify, Zillow, C++]
---
Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

# Example 1:

	Input: [3,2,1,5,6,4] and k = 2
	Output: 5

# Example 2:

	Input: [3,2,3,1,2,4,5,5,6] and k = 4
	Output: 4

# Note:
You may assume k is always valid, 1 ≤ k ≤ array's length.

______________________  

# Solution  

# Min-Heap

Time complexity : O(nlogk) (k = size of min-heap)  
Space complexity : O(k)  

	class Solution {
	public:
	    int findKthLargest(vector<int>& nums, int k) {
	        priority_queue<int, vector<int>, greater<int>> pq;
	        for (int n: nums) {
	            pq.push(n);
	            if (k < pq.size())
	                pq.pop();
	        }
	        return pq.top();
	    }
	};

用 min-heap 來存最多 k 個元素，每次塞入若超過 k 個，則最小的元素優先剔除。  
最後存在 min-heap 中的 k 個即為前 k 個最大的元素。


# Quick Selection

Time complexity : O(n) (worst case = O(n^2))  
Space complexity : O(1)  

	class Solution {
	public:
	    int findKthLargest(vector<int>& nums, int k) {
	        int left = 0, right = nums.size()-1, kth = 0;
	        while (1) {
	            int idx = partition(nums, left, right);
	            if (idx == k - 1) {
	                kth = nums[idx];
	                break;
	            }
	            if (idx < k-1) left = idx + 1;
	            else right = idx - 1;
	        }
	        return kth;
	    }
	private:
	    int partition(vector<int>& nums, int left, int right) {
	        int pivot = nums[left], l = left + 1, r = right;
	        while (l <= r) {
	            if (nums[l] < pivot && pivot < nums[r])
	                swap(nums[l++], nums[r--]);
	            if (pivot <= nums[l]) ++l;
	            if (nums[r] <= pivot) --r;
	        }
	        swap(nums[left], nums[r]);
	        return r;
	    }
	};

Quickselect 的原理與 quick sort 差不多，但只往目標的那一邊移動。  
partition function 會將 nums 分兩類：比pivot大、比pivot小。並回傳pivot位置(idx)。  
當 idx == k - 1 時，即找到第 k 大的元素了。