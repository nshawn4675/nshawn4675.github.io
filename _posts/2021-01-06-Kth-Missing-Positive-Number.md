---
layout: post
title:  "[LeetCode January Challange] Day 6 - Kth Missing Positive Number"
date:   2021-01-06 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Array, Hash Table, Facebook, Microsoft]
---
Given an array <font color="red">arr</font> of positive integers sorted in a **strictly increasing order**, and an integer <font color="red">k</font>.

*Find the <font color="red">k-th</font> positive integer that is missing from this array.*

# Example 1:

	Input: arr = [2,3,4,7,11], k = 5
	Output: 9
	Explanation: The missing positive integers are [1,5,6,8,9,10,12,13,...]. The 5th missing positive integer is 9.

# Example 2:

	Input: arr = [1,2,3,4], k = 2
	Output: 6
	Explanation: The missing positive integers are [5,6,7,...]. The 2nd missing positive integer is 6.

# Constraints:

- <font color="red">1 <= arr.length <= 1000</font>
- <font color="red">1 <= arr[i] <= 1000</font>
- <font color="red">1 <= k <= 1000</font>
- <font color="red">arr[i] < arr[j] for 1 <= i < j <= arr.length</font>

______________________  

# Solution  

# Hash Table

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    int findKthPositive(vector<int>& arr, int k) {
	        unordered_set<int> s;
	        for (int n: arr) s.insert(n);
	        
	        for (int i=1; i<=arr.back(); ++i) {
	            if (!s.count(i)) --k;
	            if (0 == k) return i;
	        }
	        
	        return arr.back() + k;
	    }
	};

用一 set 記錄出現的有哪些，再遍歷 1 ~ arr.back()。  
若有遇到 miss 的，--k。  
若 0 == k，則 i 為所求。  

若遍歷完 arr ，k 還有剩，則 arr.back() + k 為所求。  

# Binary Search

Time complexity : O(logn)  
Space complexity : O(1)  

	class Solution {
	public:
	    int findKthPositive(vector<int>& arr, int k) {
	        int l = 0, r = arr.size()-1;
	        while (l <= r) {
	            int m = l + (r-l)/2;
	            if (arr[m] - (m+1) < k)
	                l = m + 1;
	            else
	                r = m - 1;
	        }
	        
	        return k + l;
	    }
	};

normal：[1, 2, 3, 4, 5]  
arr：[2, 3, 4, 7, 11]  

2 - 1 = 1 (在 2 之前共 miss 1 個)  
7 - 4 = 3 (在 7 之前共 miss 3 個)

可推得在 idx 之前共 miss 的個數為：arr[idx] - (idx + 1)
又 arr 為 strictly increasing order ，故 miss 個數同為 strictly increasing order。  
在一個已排序的 array ，可以使用 Binary Search 加快搜索速度，目標是 miss 個數。  
跳出迴圈後，l = r + 1。  
我們的所求會界於 arr[r] ~ arr[l] 之間。  
所求即為由 arr[r] 往上加，加多少會到達 k。  

arr[r] + (k - 至 arr[r]之前 # miss)  
arr[r] + (k - (arr[r] - (r + 1)))  
arr[r] + k - arr[r] + r + 1  
k + r + 1  
k + l  

最後所求為 k + l。
