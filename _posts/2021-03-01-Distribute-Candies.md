---
layout: post
title:  "[LeetCode March Challange] Day 01 - Distribute Candies"
date:   2021-03-01 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Hash Table, Microsoft, LiveRamp]
---
Alice has <font color="red">n</font> candies, where the <font color="red">ith</font> candy is of type <font color="red">candyType[i]</font>. Alice noticed that she started to gain weight, so she visited a doctor.

The doctor advised Alice to only eat <font color="red">n / 2</font> of the candies she has (<font color="red">n</font> is always even). Alice likes her candies very much, and she wants to eat the maximum number of different types of candies while still following the doctor's advice.

Given the integer array <font color="red">candyType</font> of length <font color="red">n</font>, return *the **maximum** number of different types of candies she can eat if she only eats <font color="red">n / 2</font> of them*.

# Example 1:

	Input: candyType = [1,1,2,2,3,3]
	Output: 3
	Explanation: Alice can only eat 6 / 2 = 3 candies. Since there are only 3 types, she can eat one of each type.

# Example 2:

	Input: candyType = [1,1,2,3]
	Output: 2
	Explanation: Alice can only eat 4 / 2 = 2 candies. Whether she eats types [1,2], [1,3], or [2,3], she still can only eat 2 different types.

# Example 3:

	Input: candyType = [6,6,6,6]
	Output: 1
	Explanation: Alice can only eat 4 / 2 = 2 candies. Even though she can eat 2 candies, she only has 1 type.

# Constraints:

- <font color="red">n == candyType.length</font>
- <font color="red">2 <= n <= 10^4</font>
- **<font color="red">n</font>** is even.
- <font color="red">-10^5 <= candyType[i] <= 10^5</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    int distributeCandies(vector<int>& c) {
	        const int TOT_C = c.size();
	        set<int> s(c.begin(), c.end());
	        int types = s.size();
	        return TOT_C / 2 < types ? TOT_C / 2 : types;
	    }
	};

1. 算出總共有幾顆 candy，才知道醫生規定最多能吃 candy / 2 顆。
2. 算出 candy 總共有多少種 types。
3. 貪心的在能吃的數量內，儘可能吃多一點 types 的 candy。

可縮寫成一行：

	class Solution {
	public:
	    int distributeCandies(vector<int>& c) {
	        return min(set<int>(c.begin(), c.end()).size(), c.size() / 2);
	    }
	};