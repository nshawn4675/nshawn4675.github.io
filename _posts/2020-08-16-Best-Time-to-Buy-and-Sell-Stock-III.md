---
layout: post
title:  "[LeetCode August Challange]Day16-Best Time to Buy and Sell Stock III"
date:   2020-08-16 00:00:00 +0800
categories: LeetCode
tags: [Array, Dynamic Programming, C++]
---
Say you have an array for which the i-th element is the price of a given stock on day i.  

Design an algorithm to find the maximum profit. You may complete at most two transactions.  

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).  

# Example 1:  
	Input: [3,3,5,0,0,3,1,4]
	Output: 6
	Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
	             Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.

# Example 2:  
	Input: [1,2,3,4,5]
	Output: 4
	Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
	             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
	             engaging multiple transactions at the same time. You must sell before buying again.

# Example 3:  
	Input: [7,6,4,3,1]
	Output: 0
	Explanation: In this case, no transaction is done, i.e. max profit = 0.

______________________  

# solution

Time complexity : O(n)  
Space complexity : O(n)

	class Solution {
	public:
	    int maxProfit(vector<int>& prices) {
	        int n = prices.size();
	        int max_k = 2;
	        int dp[n+1][max_k+1][2];
	        
	        for (int i=0; i<=n; ++i) {
	            dp[i][0][0] = 0;
	            dp[i][0][1] = INT_MIN;
	            for (int k=max_k; 0<k; --k) {
	                dp[i][k][0] = i==0 ? 0 : max(dp[i-1][k][0], dp[i-1][k][1] + prices[i-1]);
	                dp[i][k][1] = i==0 ? INT_MIN : max(dp[i-1][k][1], dp[i-1][k-1][0] - prices[i-1]);
	            }
	        }
	        
	        return dp[n][max_k][0];
	    }
	};

定義dp\[n\]\[k\]\[s\]為最大獲利，其中：  
- n：天數。
- k：允許的交易數。
- s：s=1代表目前持有股票；s=0代表目前未持有股票

有關狀態轉換：  
- 未持有股票，可繼續等待或是買入轉換到已持有股票。
- 已持有股票，可繼續等待或是賣出轉換到未持有股票。

dp\[i\]\[k\]\[0\] = max\(dp\[i-1\]\[k\]\[0\], dp\[i-1\]\[k\]\[1\]+price\[i\]\)，可理解為：當天未持有股票的最大獲利 = max(昨天未持有股票的最大獲利, 昨天持有、今天賣出的最大獲利)  
dp\[i\]\[k\]\[1\] = max\(dp\[i-1\]\[k\]\[1\], dp\[i-1\]\[k\]\[0\]-price\[i\]\)，可理解為：當天持有股票的最大獲利 = max(昨天持有股票的最大獲利, 昨天未持有、今天買入的最大獲利)  

有關初始狀態：  
dp\[-1\]\[k\]\[0\] = dp\[i\]\[0\]\[0\] = 0，前者可理解為：尚未開始且尚未持有股票時的獲利；後者可理解為：我完全沒有買入的機會。  
dp\[-1\]\[k\]\[1\] = dp\[i\]\[0\]\[1\] = -∞，前者可理解為：尚未開始而我已持有股票時的獲利；後者可理解為：我完全沒有買入的機會而持有股票時的獲利，顯然兩者皆不可能成立，故設為-∞。  

此方法相當於窮舉，最後答案是取dp\[n\]\[k\]\[0\]而非dp\[n\]\[k\]\[1\]的原因是，都要結算了，未持有股票的獲利肯定\>持有股票的獲利。