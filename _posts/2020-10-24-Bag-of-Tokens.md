---
layout: post
title:  "[LeetCode October Challange] Day 24 - Bag of Tokens"
date:   2020-10-24 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Greedy, Google]
---
You have an initial **power** of <font color="red">P</font>, an initial **score** of <font color="red">0</font>, and a bag of <font color="red">tokens</font> where <font color="red">tokens[i]</font> is the value of the <font color="red">i-th</font> token (0-indexed).  

Your goal is to maximize your total **score** by potentially playing each token in one of two ways:  
- If your current **power** is at least <font color="red">tokens[i]</font>, you may play the <font color="red">i-th</font> token face up, losing <font color="red">tokens[i]</font> **power** and gaining <font color="red">1</font> **score**.
- If your current **score** is at least <font color="red">1</font>, you may play the <font color="red">i-th</font> token face down, gaining <font color="red">tokens[i]</font> **power** and losing <font color="red">1</font> **score**.

Each token may be played **at most** once and **in any order**. You do **not** have to play all the tokens.  

Return *the largest possible **score** you can achieve after playing any number of tokens*.  

# Example 1:  
	Input: tokens = [100], P = 50
	Output: 0
	Explanation: Playing the only token in the bag is impossible because you either have too little power or too little score.

# Example 2:  
	Input: tokens = [100,200], P = 150
	Output: 1
	Explanation: Play the 0th token (100) face up, your power becomes 50 and score becomes 1.
	There is no need to play the 1st token since you cannot play it face up to add to your score.

# Example 3:  
	Input: tokens = [100,200,300,400], P = 200
	Output: 2
	Explanation: Play the tokens in this order to get a score of 2:
	1. Play the 0th token (100) face up, your power becomes 100 and score becomes 1.
	2. Play the 3rd token (400) face down, your power becomes 500 and score becomes 0.
	3. Play the 1st token (200) face up, your power becomes 300 and score becomes 1.
	4. Play the 2nd token (300) face up, your power becomes 0 and score becomes 2.

# Constraints:  
- <font color="red">0 <= tokens.length <= 1000</font>
- <font color="red">0 <= tokens[i], P < 10^4</font>

______________________  

# Solution  

Time complexity : O(nlog(n))  
Space complexity : O(1)  

	class Solution {
	public:
	    int bagOfTokensScore(vector<int>& tokens, int P) {
	        sort(tokens.begin(), tokens.end());
	        int l=0, r=tokens.size()-1;
	        int ans=0, cur_ans=0;
	        while (l <= r) {
	            if (tokens[l] <= P) {
	                ans = max(ans, ++cur_ans);
	                P -= tokens[l++];
	            } else if (0 < cur_ans) {
	                --cur_ans;
	                P += tokens[r--];
	            } else break;
	        }
	        return ans;
	    }
	};

由小至大排序，再用two-pointer，左邊買分數，右邊賣分數。  

要注意的是沒有分數時，是不能賣分數賺power的，故break的情況即是power不夠買最便宜的分數，又沒有分數可以換power。