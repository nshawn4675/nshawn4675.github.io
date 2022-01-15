---
layout: post
title: "[LeetCode February Challange] Day 22 - Longest Word in Dictionary through Deleting"
date: 2021-02-22 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Two Pointers, String, Sorting, Goldman Sachs, C++]
---
Given a string <font color="red">s</font> and a string array <font color="red">dictionary</font>, return *the longest string in the dictionary that can be formed by deleting some of the given string characters*. If there is more than one possible result, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

# Example 1:

	Input: s = "abpcplea", dictionary = ["ale","apple","monkey","plea"]
	Output: "apple"

# Example 2:

	Input: s = "abpcplea", dictionary = ["a","b","c"]
	Output: "a"

# Constraints:

- <font color="red">1 <= s.length <= 1000</font>
- <font color="red">1 <= dictionary.length <= 1000</font>
- <font color="red">1 <= dictionary[i].length <= 1000</font>
- **<font color="red">s</font>** and <font color="red">dictionary[i]</font> consist of lowercase English letters.

______________________  

# Solution  

Time complexity : O(n \* l) (n : # words in dict, l : len of s)  
Space complexity : O(1)  

	class Solution {
	public:
	    string findLongestWord(string s, vector<string>& d) {
	        string ans = "";
	        for (string w: d) {
	            if (isSubsequence(s, w)) {
	                if ( ans.size() < w.size() ||
	                    (ans.size() == w.size() &&
	                     strcmp(w.c_str(), ans.c_str()) < 0))
	                    ans = w;
	            }
	        }
	        return ans;
	    }
	private:
	    bool isSubsequence(string& s, string& w) {
	        int end = 0;
	        for (int i=0; i<s.size(); ++i)
	            if (s[i] == w[end]) ++end;
	        return end == w.size();
	    }
	};

dict 內的 word 一個一個檢查是否為 s 的子字串。  
若是的話，再檢查 2 條件：
1. ans 字串長度 < w。
2. ans 與 w 長度相同，但字串比較起來 w 比 ans 小。
以上兩者其一成立的話，就將最新的 ans 更新為 w。