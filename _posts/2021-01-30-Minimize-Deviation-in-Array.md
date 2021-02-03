---
layout: post
title:  "[LeetCode January Challange] Day 30 - Minimize Deviation in Array"
date:   2021-01-30 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Hard, Heap, Ordered Map, Samsung]
---
You are given an array <font color="red">nums</font> of n positive integers.

You can perform two types of operations on any element of the array any number of times:

- If the element is **even**, **divide** it by <font color="red">2</font>.
	- For example, if the array is <font color="red">[1,2,3,4]</font>, then you can do this operation on the last element, and the array will be <font color="red">[1,2,3,2]</font>.
- If the element is **odd**, **multiply** it by <font color="red">2</font>.
	- For example, if the array is <font color="red">[1,2,3,4]</font>, then you can do this operation on the first element, and the array will be <font color="red">[2,2,3,4]</font>.
The **deviation** of the array is the **maximum difference** between any two elements in the array.

Return *the **minimum deviation** the array can have after performing some number of operations*.

# Example 1:

	Input: nums = [1,2,3,4]
	Output: 1
	Explanation: You can transform the array to [1,2,3,2], then to [2,2,3,2], then the deviation will be 3 - 2 = 1.

# Example 2:

	Input: nums = [4,1,5,20,3]
	Output: 3
	Explanation: You can transform the array after two operations to [4,2,5,5,3], then the deviation will be 5 - 2 = 3.

# Example 3:

	Input: nums = [2,10,8]
	Output: 3

# Constraints:

- <font color="red">n == nums.length</font>
- <font color="red">2 <= n <= 10^5</font>
- <font color="red">1 <= nums[i] <= 10^9</font>

______________________  

# Solution  

# Max Heap

Time complexity : O(nlogn)  
Space complexity : O(n)  

	class Solution {
	public:
	    int minimumDeviation(vector<int>& nums) {
	        priority_queue<int> pq;
	        int min_num = INT_MAX;
	        for (int n: nums) {
	            int x = n & 1 ? n*2 : n;
	            pq.push(x);
	            min_num = min(min_num, x);
	        }
	        
	        int ans = pq.top() - min_num;
	        while (pq.top() % 2 == 0) {
	            int x = pq.top()/2; pq.pop();
	            pq.push(x);
	            min_num = min(min_num, x);
	            ans = min(ans, pq.top()-min_num);
	        }
	        return ans;
	    }
	};

先做前處理，將所有奇數乘 2，之後只要考慮偶數的除 2 即可。  
小數奇數已做乘 2 往上拉，接下來只考慮最大值且為偶數可以除 2。  
做到最大值為奇數為止，因奇數只能乘 2，max-min 只會更大。

# Ordered Set

Time complexity : O(nlogn)  
Space comlexity : O(n)  

	class Solution {
	public:
	    int minimumDeviation(vector<int>& nums) {
	        set<int> s;
	        for (int n: nums)
	            s.insert(n & 1 ? n*2 : n);
	        
	        int ans = *s.rbegin() - *s.begin();
	        while (*s.rbegin() % 2 == 0) {
	            s.insert(*s.rbegin()/2);
	            s.erase(*s.rbegin());
	            ans = min(ans, *s.rbegin() - *s.begin());
	        }
	        return ans;
	    }
	};

概念與上相同，只是用 set 來做。