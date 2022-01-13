---
layout: post
title:  "[LeetCode July Challange]Day17-Top K Frequent Elements"
date:   2020-07-17 00:00:00 +0800
categories: LeetCode
tags: [Array, Hash Table, Divide and Conquer, Sorting, Heap (Priority Queue), Bucket Sort, Counting, Quickselect, C++]
---
Given a non-empty array of integers, return the **k** most frequent elements.  

# Example 1:  
	Input: nums = [1,1,1,2,2,3], k = 2
	Output: [1,2]

# Example 2:  
	Input: nums = [1], k = 1
	Output: [1]

# Note:  
- You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
- Your algorithm's time complexity **must be** better than O(n log n), where n is the array's size.
- It's guaranteed that the answer is unique, in other words the set of the top k frequent elements is unique.
- You can return the answer in any order.

______________________  

# solution
time complexity : O(n)  
space complexity : O(n)  

	class Solution {
	public:
	    vector<int> topKFrequent(vector<int>& nums, int k) {
	        // {num, freq}
	        unordered_map<int, int> freqCnt;
	        int maxFreq = 1;
	        for (int i: nums)
	            maxFreq = max(maxFreq, ++freqCnt[i]);
	        
	        // {freq, {nums}}
	        unordered_map<int, vector<int>> freqNums;
	        for (auto i: freqCnt)
	            freqNums[i.second].push_back(i.first);
	        
	        vector<int> ans;
	        for (int i=maxFreq; i>0; --i) {
	            auto it = freqNums.find(i);
	            if (it == freqNums.end()) continue;
	            ans.insert(ans.end(), it->second.begin(), it->second.end());
	            if (ans.size() == k) return ans;
	        }
	        
	        return ans;
	    }
	};

流程：計算每個數字的頻率→根據每個頻率蒐集相對應的數字→頻率由大到小依序塞入答案中，直到k個。  

因為可以假設k得出來的答案是獨一無二的，不會有這樣子的題目出現：  

	Input: nums = [1,2], k = 1
	Output: [1]? [2]?
	k must be 2, so that output = {1, 2}

所以給的k，一定是會把相同頻率數字全部蒐集起來。