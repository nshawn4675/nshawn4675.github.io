---
layout: post
title:  "[LeetCode September Challange]Day22-Majority Element II"
date:   2020-09-22 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Hash Table, Sorting, Counting, C++]
---
Given an integer array of size *n*, find all elements that appear more than <font color="red">⌊ n/3 ⌋</font> times.  

**Note:** The algorithm should run in linear time and in O(1) space.  

# Example 1:  
	Input: [3,2,3]
	Output: [3]

# Example 2:  
	Input: [1,1,1,3,3,2,2,2]
	Output: [1,2]

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    vector<int> majorityElement(vector<int>& nums) {
	        vector<int> ans = {};
	        const int n = nums.size();
	        if (n == 0) return ans;
	        
	        int candi1, candi2, cnt1, cnt2;
	        candi1 = candi2 = -1;
	        cnt1 = cnt2 = 0;
	        
	        for (int num: nums) {
	            if (num == candi1)
	                ++cnt1;
	            else if (num == candi2)
	                ++cnt2;
	            else if (cnt1 == 0) {
	                candi1 = num;
	                cnt1 = 1;
	            } else if (cnt2 == 0) {
	                candi2 = num;
	                cnt2 = 1;
	            } else {
	                --cnt1;
	                --cnt2;
	            }
	        }
	        
	        cnt1 = cnt2 = 0;
	        for (int num: nums) {
	            if (num == candi1) ++cnt1;
	            else if (num == candi2) ++cnt2;
	        }
	        
	        if (cnt1 > n/3) ans.push_back(candi1);
	        if (cnt2 > n/3) ans.push_back(candi2);
	        
	        return ans;
	    }
	};

使用[Boyer-Moore Voting Algorithm](https://zh.wikipedia.org/wiki/多数投票算法)。  

在一系列輸入中：  
頂多會有1個元素符合其個數>⌊n/2⌋  
頂多會有2個元素符合其個數>⌊n/3⌋  
頂多會有3個元素符合其個數>⌊n/4⌋  
頂多會有4個元素符合其個數>⌊n/5⌋  
.  
.  
.  
頂多會有k-1個元素符合其個數>⌊n/k⌋  

在此題，我們頂多會有2個元素符合其個數>⌊n/3⌋。  

接著想像一個容器，裡面只裝目前輸入前2種最多的元素。  
手上拿著下一個輸入，與其中之一相符，則放入。  
若容器中有一種元素個數為0，則用新的輸入取代之。  
若都不相符，容器中兩種元素各取一個，含手上的，三個一起丟掉。  

最後容器中會裝著前2名，個數最多的元素種類。  

再判斷這2種元素，在原輸入中，是否個數>⌊n/3⌋。  