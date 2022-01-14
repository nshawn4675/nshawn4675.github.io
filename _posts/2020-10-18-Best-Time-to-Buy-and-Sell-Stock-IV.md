---
layout: post
title:  "[LeetCode October Challange] Day 18 - Best Time to Buy and Sell Stock IV"
date:   2020-10-18 00:00:00 +0800
categories: LeetCode
tags: [Hard, Array, Dynamic Programming, Amazon, Bloomberg, Google, Citadel, C++]
---
You are given an integer array <font color="red">prices</font> where <font color="red">prices[i]</font> is the price of a given stock on the i-th day.  

Design an algorithm to find the maximum profit. You may complete at most <font color="red">k</font> transactions.  

**Notice** that you may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).  

# Example 1:  
	Input: k = 2, prices = [2,4,1]
	Output: 2
	Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.

# Example 2:  
	Input: k = 2, prices = [3,2,6,5,0,3]
	Output: 7
	Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4. Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.

# Constraints:  
- <font color="red">0 <= k <= 109</font>
- <font color="red">0 <= prices.length <= 104</font>
- <font color="red">0 <= prices[i] <= 1000</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    int maxProfit(int max_k, vector<int>& prices) {
	        int days = prices.size();
	        if (0 == days || 0 == max_k) return 0;
	        if (max_k > days/2) return maxProfit_inf(prices);
	        
	        int profit[days+1][max_k+1][2];
	        for (int day=0; day<=days; ++day) {
	            profit[day][0][0] = 0;
	            profit[day][0][1] = INT_MIN;
	            for (int k=1; k<=max_k; ++k) {
	                if (0 == day) {
	                    profit[day][k][0] = 0;
	                    profit[day][k][1] = INT_MIN;
	                    continue;
	                }
	                profit[day][k][0] = max(profit[day-1][k][0], profit[day-1][k][1]+prices[day-1]);
	                profit[day][k][1] = max(profit[day-1][k][1], profit[day-1][k-1][0]-prices[day-1]);
	            }
	        }
	        return profit[days][max_k][0];
	    }
	private:
	    int maxProfit_inf(vector<int>& prices) {
	        int days = prices.size();
	        int profit[days+1][2];
	        for (int day=0; day<=days; ++day) {
	            if (0 == day) {
	                profit[day][0] = 0;
	                profit[day][1] = INT_MIN;
	                continue;
	            }
	            profit[day][0] = max(profit[day-1][0], profit[day-1][1]+prices[day-1]);
	            profit[day][1] = max(profit[day-1][1], profit[day-1][0]-prices[day-1]);
	        }
	        return profit[days][0];
	    }
	};

dynamic programming就是有技巧性的窮舉。  
定義profit\[day\]\[k\]\[hold\]，day代表第幾天，k代表最大交易次數，hold代表是否持有股票(1有/0無)。  

初始狀態：  
profit\[-1\]\[k\]\[0\] = 0，還沒開始時，收益為0。  
profit\[-1\]\[k\]\[1\] = -∞，還沒開始時，不可能持有股票。  
profit\[day\]\[0\]\[0\] = 0，不管第幾天，沒有可用交易次數，收益為0。  
profit\[day\]\[0\]\[1\] = -∞，不管第幾天，沒有可用交易次數，不可能持有股票。  

接下來就窮舉所有狀態，  
profit\[day\]\[k\]\[0\]，表示到今天為止，可以有k次交易，目前手上無持有股票，的最大收益，為以下兩者取最大者：  
1. profit\[day-1\]\[k\]\[0\]，前一天手上無持有股票，不做動作。
2. profit\[day-1\]\[k\]\[1\]+prices\[day-1\]，前一天持有股票，今日賣出(此prices的day-1是今日，因days多1天做初始化)

profit\[day\]\[k\]\[1\]，表示到今天為止，可以有k次交易，目前手上持有股票，的最大收益，為以下兩者取最大者：  
1. profit\[day-1\]\[k\]\[1\]，前一天手上持有股票，不做動作。
2. profit\[day-1\]\[k-1\]\[0\]-prices\[day-1\]，前一天無持有股票，今日買入(此prices的day-1是今日，日days多1天做初始化)

特別情況：因買、賣需秏時2day，所以若max_k>days/2時，等同於沒有交易次數限制，就能用沒有交易限制的方式來計算。