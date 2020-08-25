---
layout: post
title:  "[LeetCode August Challange]Day25-Minimum Cost For Tickets"
date:   2020-08-25 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
In a country popular for train travel, you have planned some train travelling one year in advance.  The days of the year that you will travel is given as an array **<font color="red">days</font>**.  Each day is an integer from **<font color="red">1</font>** to **<font color="red">365</font>**.  

Train tickets are sold in 3 different ways:  
- a 1-day pass is sold for **<font color="red">costs[0]</font>** dollars;
- a 7-day pass is sold for **<font color="red">costs[1]</font>** dollars;
- a 30-day pass is sold for **<font color="red">costs[2]</font>** dollars.
The passes allow that many days of consecutive travel.  For example, if we get a 7-day pass on day 2, then we can travel for 7 days: day 2, 3, 4, 5, 6, 7, and 8.  

Return the minimum number of dollars you need to travel every day in the given list of **<font color="red">days</font>**.


# Example 1:  
	Input: days = [1,4,6,7,8,20], costs = [2,7,15]
	Output: 11
	Explanation: 
	For example, here is one way to buy passes that lets you travel your travel plan:
	On day 1, you bought a 1-day pass for costs[0] = $2, which covered day 1.
	On day 3, you bought a 7-day pass for costs[1] = $7, which covered days 3, 4, ..., 9.
	On day 20, you bought a 1-day pass for costs[0] = $2, which covered day 20.
	In total you spent $11 and covered all the days of your travel.

# Example 2:  
	Input: days = [1,2,3,4,5,6,7,8,9,10,30,31], costs = [2,7,15]
	Output: 17
	Explanation: 
	For example, here is one way to buy passes that lets you travel your travel plan:
	On day 1, you bought a 30-day pass for costs[2] = $15 which covered days 1, 2, ..., 30.
	On day 31, you bought a 1-day pass for costs[0] = $2 which covered day 31.
	In total you spent $17 and covered all the days of your travel.

# Note:  
1. **<font color="red">1 <= days.length <= 365</font>**
2. **<font color="red">1 <= days[i] <= 365</font>**
3. **<font color="red">days</font>** is in strictly increasing order.
4. **<font color="red">costs.length == 3</font>**
5. **<font color="red">1 <= costs[i] <= 1000</font>**

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(n)

	class Solution {
	public:
	    int mincostTickets(vector<int>& days, vector<int>& costs) {
	        int last_day = days.back();
	        vector<bool> activate(last_day+1);
	        vector<int> dp(last_day+1);
	        for (int day: days) activate[day]=true;
	        dp[0] = 0;
	        
	        for (int i=1; i<=last_day; ++i) {
	            if (!activate[i]) {
	                dp[i] = dp[i-1];
	                continue;
	            }
	            dp[i] = dp[i-1]+costs[0];
	            dp[i] = min(dp[i], dp[max(0, i-7)]+costs[1]);
	            dp[i] = min(dp[i], dp[max(0, i-30)]+costs[2]);
	        }
	        
	        return dp.back();
	    }
	};

dp[i]代表到第i天為止，可以花的最少的錢。  
用activate記錄哪些天要用到票。  
若第i天要用到票，則  
dp[i] = min(dp[i-1]+cost[0], dp[i-7]+cost[1], dp[i-30]+cost[2])  
買一天的票，買七天的票，買三十天的票，三者取最小。  
最後回傳dp.back()，到最後一天為止，可以花的最少的錢。