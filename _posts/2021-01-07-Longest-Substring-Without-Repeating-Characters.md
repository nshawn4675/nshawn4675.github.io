---
layout: post
title:  "[LeetCode January Challange] Day 7 - Longest Substring Without Repeating Characters"
date:   2021-01-07 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Hash Table, Two Pointers, String, Sliding Window, Amazon, Bloomberg, Microsoft, Facebook, Apple, Google, Adobe, Goldman Sachs, ByteDance, Oracle, Alation, Yahoo, Uber, VMWare, Morgan Stanley, eBay, Expedia, SAP, Splunk, Spotify]
---
Given a string <font color="red">s</font>, find the length of the **longest substring** without repeating characters.

# Example 1:

	Input: s = "abcabcbb"
	Output: 3
	Explanation: The answer is "abc", with the length of 3.

# Example 2:

	Input: s = "bbbbb"
	Output: 1
	Explanation: The answer is "b", with the length of 1.

# Example 3:

	Input: s = "pwwkew"
	Output: 3
	Explanation: The answer is "wke", with the length of 3.
	Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

# Example 4:

	Input: s = ""
	Output: 0

# Constraints:

- <font color="red">0 <= s.length <= 5 * 10^4</font>
- **<font color="red">s</font>** consists of English letters, digits, symbols and spaces.

______________________  

# Solution  

# Brute Force (Time Limit Exceeded)

Time complexity : O(n^3)  
Space complexity : O(m) m = # char set  

	class Solution {
	public:
	    int lengthOfLongestSubstring(string s) {
	        int ans = 0;
	        for (int i=0; i<s.size(); ++i) {
	            for (int j=i; j<s.size(); ++j) {
	                int len = j - i + 1;
	                if (!isRepeat(s.substr(i, len)))
	                    ans = max(ans, len);
	            }
	        }
	        return ans;
	    }
	    
	    bool isRepeat(string s) {
	        bitset<256> m;
	        for (char c: s) {
	            if (m.test(c)) return true;
	            m.flip(c);
	        }
	        return false;
	    }
	};

以各字為首，列舉所有子字串。  
例："abcabcbb"  
"a"、"ab"、...、"abcabcbb"  
"b"、"bc"、...、"bcabcbb"
...
以此類推。  

再以每個子字串去檢查是否有重覆字。  


# Two Pointer + Sliding Window

Time complexity : O(n)  
Space complexity : O(m)  

	class Solution {
	public:
	    int lengthOfLongestSubstring(string s) {
	        vector<int> occur(256, 0);
	        int l = 0, r = 0;
	        int ans = 0;
	        while (r < s.size()) {
	            // new char
	            char r_c = s[r];
	            ++occur[r_c];
	            
	            // exist before, contract window
	            while (1 < occur[r_c]) {
	                char l_c = s[l];
	                --occur[l_c];
	                ++l;
	            }
	            
	            // update ans & expand to next one
	            ans = max(ans, r-l+1);
	            ++r;
	        }
	        return ans;
	    }
	};

l ~ r 之間為不重覆的子字串，window size 的移動是由 l 用來contract、 r 用來 expand。  

用 occur 記錄各個字出現了幾次。  

有新的字進來，增加 occur 的出現次數，若之前有出現過，l 就一步一步往右走，邊走邊更新 occur ，直到之前出現過的只剩一次。  

最後更新 ans、 expand window。  


# Two Pointer + Sliding Window (optimized)  

time complexity : O(n)  
space complexity : O(m)  

	class Solution {
	public:
	    int lengthOfLongestSubstring(string s) {
	        vector<int> idxs(256, -1);
	        int l = 0, r = 0;
	        int ans = 0;
	        while (r < s.size()) {
	            // new char
	            char r_c = s[r];
	            
	            // update l if it exist before & l is in the right range
	            if (-1 < idxs[r_c] && l <= idxs[r_c])
	                l = idxs[r_c] + 1;
	            
	            // update idxs and ans then expand window.
	            idxs[r_c] = r;
	            ans = max(ans, r-l+1);
	            ++r;
	        }
	        return ans;
	    }
	};

改良後的版本的差別：  
1. l 更新的方式不是一步一步走，而是直接過去。
2. 記錄最新出現過的位置，而非出現次數。
