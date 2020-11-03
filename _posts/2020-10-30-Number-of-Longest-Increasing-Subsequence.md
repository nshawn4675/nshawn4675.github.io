---
layout: post
title:  "[LeetCode October Challange] Day 30 - Number of Longest Increasing Subsequence"
date:   2020-10-30 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Dynamic Programming, Bloomberg]
---
Given an integer array <font color="red">nums</font>, return *the number of longest increasing subsequences*.

# Example 1:  
	Input: nums = [1,3,5,4,7]
	Output: 2
	Explanation: The two longest increasing subsequences are [1, 3, 4, 7] and [1, 3, 5, 7].

# Example 2:  
	Input: nums = [2,2,2,2,2]
	Output: 5
	Explanation: The length of longest continuous increasing subsequence is 1, and there are 5 subsequences' length is 1, so output 5.

# Constraints:  
- <font color="red">1 <= nums.length <= 2000</font>
- <font color="red">-10^6 <= nums[i] <= 10^6</font>

______________________  

# Solution  

Time complexity : O(n^2)  
Space complexity : O(n)  

	class Solution {
	public:
	    int findNumberOfLIS(vector<int>& nums) {
	        int n = nums.size();
	        vector<int> len(n, 1);
	        vector<int> cnt(n, 1);
	        
	        for (int end=0; end<n; ++end) {
	            for (int mid=0; mid<end; ++mid) {
	                if (nums[mid] < nums[end]) {
	                    if (len[mid] >= len[end]) {
	                        len[end] = len[mid] + 1;
	                        cnt[end] = cnt[mid];
	                    } else if (len[mid] + 1 == len[end])
	                        cnt[end] += cnt[mid];
	                }
	            }
	        }
	        
	        const int max_len = *max_element(len.begin(), len.end());
	        int ans = 0;
	        for (int i=0; i<n; ++i) {
	            if (len[i] == max_len)
	                ans += cnt[i];
	        }
	        return ans;
	    }
	};

定義len\[i\]代表在到i為最後一個元素，最大的遞增數組長度。  
定義cnt\[i\]代表在到i為最後一個元素，形成該最大遞增數組的組合數。  

因此對於每一個數，都要從頭開始計算，到它之前的最大遞增數組長度是多少，共有幾種組合方式。  
對於一個數組到mid，再考量end，若mid < end，一般情況下則可以將end加在最後面，使得最大遞增數組長度+1，但組合方式不變。  
但若到mid的長度剛好是end時長度-1，則代表mid那樣的方式也可以在尾部加上end形成end時的最大遞增數組，而且組合方式不重覆，所以end時的組合方式要加上mid時的組合方式。  

最後從頭掃到尾，若以該數為結尾的最大遞增數組長度是最大的，就加上它的組合方式數量。  