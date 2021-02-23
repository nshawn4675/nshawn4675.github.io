---
layout: post
title:  "[LeetCode February Challange] Day 16 - Letter Case Permutation"
date:   2021-02-16 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Backtracking, Bit Manipulation, Microsoft, Bloomberg, Amazon, Spotify]
---
Given a string S, we can transform every letter individually to be lowercase or uppercase to create another string.

Return *a list of all possible strings we could create*. You can return the output in **any order**.

# Example 1:

	Input: S = "a1b2"
	Output: ["a1b2","a1B2","A1b2","A1B2"]

# Example 2:

	Input: S = "3z4"
	Output: ["3z4","3Z4"]

# Example 3:

	Input: S = "12345"
	Output: ["12345"]

# Example 4:

	Input: S = "0"
	Output: ["0"]

# Constraints:

- **<font color="red">S</font>** will be a string with length between <font color="red">1</font> and <font color="red">12</font>.
- **<font color="red">S</font>** will consist only of letters or digits.

______________________  

# Solution  

Time complexity : O(2^l)  
Space complexity : O(n) + O(2^l)  

	class Solution {
	public:
	    vector<string> letterCasePermutation(string S) {
	        vector<string> ans;
	        dfs(S, 0, ans);
	        return ans;
	    }
	private:
	    void dfs(string& S, int s, vector<string>& ans) {
	        if (s == S.size()) {
	            ans.push_back(S);
	            return;
	        }
	        
	        dfs(S, s+1, ans);
	        if (!isalpha(S[s])) return;
	        S[s] ^= 1 << 5;
	        dfs(S, s+1, ans);
	        S[s] ^= 1 << 5;
	    }
	};