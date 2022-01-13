---
layout: post
title:  "[LeetCode September Challange]Day18-Best Time to Buy and Sell Stock"
date:   2020-09-18 00:00:00 +0800
categories: LeetCode
tags: [Easy, Array, Dynamic Programming, C++]
---
Say you have an array for which the *i-th* element is the price of a given stock on day *i*.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.  

Note that you cannot sell a stock before you buy one.  

# Example 1:  
	Input: [7,1,5,3,6,4]
	Output: 5
	Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
	             Not 7-1 = 6, as selling price needs to be larger than buying price.

# Example 2:  
	Input: [7,6,4,3,1]
	Output: 0
	Explanation: In this case, no transaction is done, i.e. max profit = 0.

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)

	class Solution {
	public:
	    int maxProfit(vector<int>& prices) {
	        int min_price_so_far = INT_MAX;
	        int max_profit_so_far = 0;
	        for (int n: prices) {
	            if (n < min_price_so_far)
	                min_price_so_far = n;
	            int profit = max(n - min_price_so_far, max_profit_so_far);
	            max_profit_so_far = profit;
	                
	        }
	        return max_profit_so_far;
	    }
	};

記錄到目前為止的最小值、和最大獲益。  

每過一天就計算當天獲利(過往最小值與當天價相減)，若大於過往最大獲益，則更新。  