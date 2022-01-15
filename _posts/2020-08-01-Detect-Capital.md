---
layout: post
title:  "[LeetCode August Challange]Day1-Detect Capital"
date:   2020-08-01 00:00:00 +0800
categories: LeetCode
tags: [String, C++]
---
Given a word, you need to judge whether the usage of capitals in it is right or not.  

We define the usage of capitals in a word to be right when one of the following cases holds:  

1. All letters in this word are capitals, like "USA".
2. All letters in this word are not capitals, like "leetcode".
3. Only the first letter in this word is capital, like "Google".

Otherwise, we define that this word doesn't use capitals in a right way.  

# Example 1:  
	Input: "USA"
	Output: True

# Example 2:  
	Input: "FlaG"
	Output: False

**Note**: The input will be a non-empty word consisting of uppercase and lowercase latin letters.

______________________  

# solution
time complexity : O(n)  
space complexity : O(1)

	class Solution {
	public:
	    bool detectCapitalUse(string word) {
	        int n = count_if(word.begin(), word.end(), ::isupper);
	        return n==0 || (n==1 && isupper(word[0])) || n==word.length();
	    }
	};

利用count_if、isupper，計算word中大寫字母的數量n。  
若n==0：全部都小寫。  
若n==1 && isupper(word[0])：只有第一個字母為大寫。  
若n==word.length()：全部都大寫。