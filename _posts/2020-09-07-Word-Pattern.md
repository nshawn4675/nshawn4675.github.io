---
layout: post
title:  "[LeetCode September Challange]Day7-Word Pattern"
date:   2020-09-07 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given a **<font color="red">pattern</font>** and a string **<font color="red">str</font>**, find if **<font color="red">str</font>** follows the same pattern.

Here **follow** means a full match, such that there is a bijection between a letter in **<font color="red">pattern</font>** and a **non-empty** word in **<font color="red">str</font>**.

# Example 1:  
	Input: pattern = "abba", str = "dog cat cat dog"
	Output: true

# Example 2:  
	Input:pattern = "abba", str = "dog cat cat fish"
	Output: false

# Example 3:  
	Input: pattern = "aaaa", str = "dog cat cat dog"
	Output: false

# Example 4:  
	Input: pattern = "abba", str = "dog dog dog dog"
	Output: false

# Notes:  
You may assume **<font color="red">pattern</font>** contains only lowercase letters, and **<font color="red">str</font>** contains lowercase letters that may be separated by a single space.

______________________  

# Solution

Time complexity : O(N) (size of pattern or str)  
Space complexity : O(M) (unique strings in pattern and str)

	class Solution {
	public:
	    bool wordPattern(string pattern, string str) {
	        vector<string> vec_str;
	        istringstream iss(str);
	        for (string s; iss >> s;)
	            vec_str.push_back(s);
	        if (vec_str.size() != pattern.length())
	            return false;
	        
	        // use hash table to store first occurrence index.
	        unordered_map<string, int> ht;
	        for (int i=0; i<vec_str.size(); ++i) {
	            string ptn_str = to_string(pattern[i]);
	            if (ht.count(ptn_str) == 0)
	                ht[ptn_str] = i;
	            if (ht.count(vec_str[i]) == 0)
	                ht[vec_str[i]] = i;
	            if (ht[ptn_str] != ht[vec_str[i]])
	                return false;
	        }
	        
	        return true;
	    }
	};

首先將str切割成strings，裝入vector中。
判斷pattern長度與strings數量，若不相同，返回false。  

使用一個hash table記錄第一次出現的pattern及string位置。  
若沒有記錄過，就記錄上去。  
若都有記錄過了，檢查第一次出現的位置是否相同，若不相同，則代表它們是不同的符號，返回false。  

都檢查完畢，沒有問題，返回true。