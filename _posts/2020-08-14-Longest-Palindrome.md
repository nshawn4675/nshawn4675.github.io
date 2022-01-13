---
layout: post
title:  "[LeetCode August Challange]Day14-Longest Palindrome"
date:   2020-08-14 00:00:00 +0800
categories: LeetCode
tags: [Hash Table, String, Greedy, C++]
---
Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.  

This is case sensitive, for example **<font color="red">"Aa"</font>** is not considered a palindrome here.  

# Note:  
Assume the length of given string will not exceed 1,010.  

# Example:  

	Input:
	"abccccdd"

	Output:
	7

	Explanation:
	One longest palindrome that can be built is "dccaccd", whose length is 7.

______________________  

# solution

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int longestPalindrome(string s) {
	        vector<int> alphaCnt(128, 0);
	        for (char c: s) ++alphaCnt[c];

	        int oddCnt=0, evenCnt=0;
	        for (int i: alphaCnt) {
	            evenCnt += i/2;
	            oddCnt += i%2;
	        }
	        
	        return evenCnt*2+(oddCnt>0);
	    }
	};

首先計數各個字母出現的次數，  
再來計數字母出現奇偶頻率的次數，  
最後可以組成的palindrome長度，就是「偶數量\*2 + 有奇數量的話拿一個」。