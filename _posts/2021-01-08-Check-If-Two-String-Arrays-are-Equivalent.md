---
layout: post
title:  "[LeetCode January Challange] Day 8 - Check If Two String Arrays are Equivalent"
date:   2021-01-08 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, String, Facebook]
---
Given two string arrays <font color="red">word1</font> and <font color="red">word2</font>, return <font color="red">true</font> *if the two arrays **represent** the same string, and* <font color="red">false</font> *otherwise*.

A string is **represented** by an array if the array elements concatenated **in order** forms the string.

# Example 1:

	Input: word1 = ["ab", "c"], word2 = ["a", "bc"]
	Output: true
	Explanation:
	word1 represents string "ab" + "c" -> "abc"
	word2 represents string "a" + "bc" -> "abc"
	The strings are the same, so return true.

# Example 2:

	Input: word1 = ["a", "cb"], word2 = ["ab", "c"]
	Output: false

# Example 3:

	Input: word1  = ["abc", "d", "defg"], word2 = ["abcddefg"]
	Output: true

# Constraints:

- <font color="red">1 <= word1.length, word2.length <= 10^3</font>
- <font color="red">1 <= word1[i].length, word2[i].length <= 10^3</font>
- <font color="red">1 <= sum(word1[i].length), sum(word2[i].length) <= 10^3</font>
- <font color="red">word1[i] and word2[i] consist of lowercase letters.</font>

______________________  

# Solution  

# Brute Force  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    bool arrayStringsAreEqual(vector<string>& word1, vector<string>& word2) {
	        string s1, s2;
	        for (string s: word1) s1 += s;
	        for (string s: word2) s2 += s;
	        return s1 == s2;
	    }
	};


# Pointers  

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    bool arrayStringsAreEqual(vector<string>& word1, vector<string>& word2) {
	        int i1=0, j1=0;
	        int i2=0, j2=0;
	        
	        while (i1 < word1.size() || i2 < word2.size()) {
	            char c1 = i1 < word1.size() ? word1[i1][j1++] : '\0';
	            char c2 = i2 < word2.size() ? word2[i2][j2++] : '\0';
	            if (c1 != c2) return false;
	            if (j1 == word1[i1].size()) {
	                ++i1;
	                j1 = 0;
	            }
	            if (j2 == word2[i2].size()) {
	                ++i2;
	                j2 = 0;
	            }
	        }
	        
	        return true;
	    }
	};

兩個 string array 個別用指標，一個字一個字做比較。