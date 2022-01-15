---
layout: post
title: "[LeetCode January Challange] Day 1 - Check Array Formation Through Concatenation"
date: 2021-01-01 00:00:00 +0800
categories: LeetCode
tags: [Easy, Array, Hash Table, CodeSignal, C++]
---
You are given an array of **distinct** integers <font color="red">arr</font> and an array of integer arrays <font color="red">pieces</font>, where the integers in <font color="red">pieces</font> are **distinct**. Your goal is to form <font color="red">arr</font> by concatenating the arrays in <font color="red">pieces</font> **in any order**. However, you are **not** allowed to reorder the integers in each array <font color="red">pieces[i]</font>.

Return <font color="red">true</font> *if it is possible to form the array* <font color="red">arr</font> *from* <font color="red">pieces</font>. Otherwise, return <font color="red">false</font>.

# Example 1:

	Input: arr = [85], pieces = [[85]]
	Output: true

# Example 2:

	Input: arr = [15,88], pieces = [[88],[15]]
	Output: true
	Explanation: Concatenate [15] then [88]

# Example 3:

	Input: arr = [49,18,16], pieces = [[16,18,49]]
	Output: false
	Explanation: Even though the numbers match, we cannot reorder pieces[0].

# Example 4:

	Input: arr = [91,4,64,78], pieces = [[78],[4,64],[91]]
	Output: true
	Explanation: Concatenate [91] then [4,64] then [78]

# Example 5:

	Input: arr = [1,3,5,7], pieces = [[2,4,6,8]]
	Output: false

# Constraints:

- <font color="red">1 <= pieces.length <= arr.length <= 100</font>
- <font color="red">sum(pieces[i].length) == arr.length</font>
- <font color="red">1 <= pieces[i].length <= arr.length</font>
- <font color="red">1 <= arr[i], pieces[i][j] <= 100</font>
- The integers in <font color="red">arr</font> are **distinct**.
- The integers in <font color="red">pieces</font> are **distinct** (i.e., If we flatten pieces in a 1D array, all the integers in this array are distinct).

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    bool canFormArray(vector<int>& arr, vector<vector<int>>& pieces) {
	        unordered_map<int, int> m;
	        for (int idx=0; idx<pieces.size(); ++idx)
	            m[pieces[idx][0]] = idx;
	        
	        vector<int> ans;
	        for (int a: arr) {
	            if (!m.count(a)) continue;
	            ans.insert(ans.end(), pieces[m[a]].begin(), pieces[m[a]].end());
	        }
	        return ans == arr;
	    }
	};

使用 hash table ，記錄每個 piece 的第一個元素來查表。