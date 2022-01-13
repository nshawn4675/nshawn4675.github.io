---
layout: post
title:  "[LeetCode July Challange]Day31-Climbing Stairs"
date:   2020-07-31 00:00:00 +0800
categories: LeetCode
tags: [Math, Dynamic Programming, Memoization, C++]
---
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

# Example 1:  
	Input: 2
	Output: 2
	Explanation: There are two ways to climb to the top.
	1. 1 step + 1 step
	2. 2 steps

# Example 2:  
	Input: 3
	Output: 3
	Explanation: There are three ways to climb to the top.
	1. 1 step + 1 step + 1 step
	2. 1 step + 2 steps
	3. 2 steps + 1 step

# Constraints:  
- **1 <= n <= 45**

______________________  

# solution
time complexity : O(n)  
space complexity : O(n)

	class Solution {
	public:
	    int climbStairs(int n) {
	        vector<int> sol(n+1, 0);
	        sol[0] = sol[1] = 1;
	        for (int i=2; i<=n; ++i) {
	            sol[i] = sol[i-1] + sol[i-2];
	        }
	        return sol[n];
	    }
	};

動態歸劃，初始狀態樓梯為0階及1階時的走法皆為1次。(0階：不走)  

n階樓梯的走法 = 走了1步後，剩下n-1階樓梯的走法 + 走了2步後，剩下n-2階樓梯的走法。  

空間複雜度經設計後可達O(1)，但可讀性較差。