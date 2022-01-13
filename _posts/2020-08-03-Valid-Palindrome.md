---
layout: post
title:  "[LeetCode August Challange]Day3-Valid Palindrome"
date:   2020-08-03 00:00:00 +0800
categories: LeetCode
tags: [Two Pointers, String, C++]
---
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.  

**Note**: For the purpose of this problem, we define empty string as valid palindrome.  

# Example 1:  
	Input: "A man, a plan, a canal: Panama"
	Output: true

# Example 2:  
	Input: "race a car"
	Output: false

# Constraints:  
- **s** consists only of printable ASCII characters.

______________________  

# solution

Time complexity : O(n)  
Space complexity : O(1)

	class Solution {
	public:
	    bool isPalindrome(string s) {
	        for (int i=0, j=s.length()-1; i<j; ++i,--j) {
	            while (i<j && !isalnum(s[i])) ++i;
	            while (i<j && !isalnum(s[j])) --j;
	            if (tolower(s[i]) != tolower(s[j]))
	                return false;
	        }
	        return true;
	    }
	};

使用2-pointer，從頭、從尾，一路往中間檢查。  
移動到是字母或是數字，統一轉換為小寫。  
若途中有不一致，即為invalid palindrome。  
直到 j < i (palindrome長度為偶)、或是 i == j (palindrome長度為奇，中間單獨一個字)，即結束。