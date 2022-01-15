---
layout: post
title: "[LeetCode February Challange] Day 7 - Shortest Distance to a Character"
date: 2021-02-07 00:00:00 +0800
categories: LeetCode
tags: [Easy, Array, Two Pointers, String, Apple, C++]
---
Given a string <font color="red">s</font> and a character <font color="red">c</font> that occurs in <font color="red">s</font>, return *an array of integers* <font color="red">answer</font> *where* <font color="red">answer.length == s.length</font> *and* <font color="red">answer[i]</font> *is the **distance** from index* <font color="red">i</font> *to the **closest** occurrence of character* <font color="red">c</font> *in* <font color="red">s</font>.

The **distance** between two indices <font color="red">i</font> and <font color="red">j</font> is <font color="red">abs(i - j)</font>, where <font color="red">abs</font> is the absolute value function.

# Example 1:

	Input: s = "loveleetcode", c = "e"
	Output: [3,2,1,0,1,0,0,1,2,2,1,0]
	Explanation: The character 'e' appears at indices 3, 5, 6, and 11 (0-indexed).
	The closest occurrence of 'e' for index 0 is at index 3, so the distance is abs(0 - 3) = 3.
	The closest occurrence of 'e' for index 1 is at index 3, so the distance is abs(1 - 3) = 3.
	For index 4, there is a tie between the 'e' at index 3 and the 'e' at index 5, but the distance is still the same: abs(4 - 3) == abs(4 - 5) = 1.
	The closest occurrence of 'e' for index 8 is at index 6, so the distance is abs(8 - 6) = 2.

# Example 2:

	Input: s = "aaab", c = "b"
	Output: [3,2,1,0]

# Constraints:

- <font color="red">1 <= s.length <= 10^4</font>
- **<font color="red">s[i]</font>** and <font color="red">c</font> are lowercase English letters.
- It is guaranteed that <font color="red">c</font> occurs at least once in <font color="red">s</font>.

______________________  

# Solution  

Time complexity : O(n^2)  
Space complexity : O(n)  

	class Solution {
	public:
	    vector<int> shortestToChar(string s, char c) {
	        int n = s.size();
	        vector<int> ans(n, INT_MAX);
	        for (int i=0; i<n; ++i) {
	            if (s[i] != c) continue;
	            ans[i] = 0;
	            for (int j=0; j<n; ++j)
	                ans[j] = min(ans[j], abs(j-i));
	        }
	        return ans;
	    }
	};

用一 vector 記錄最短距離，遍歷元素，每遇到 c 時，就更新最小距離值。