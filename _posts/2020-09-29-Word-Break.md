---
layout: post
title:  "[LeetCode September Challange]Day29-Word Break"
date:   2020-09-29 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Dynamic Programming, Facebook, Amazon, Apple, Microsoft, Google, Bloomberg, Qualtrics, ByteDance, Twitter, Adobe, eBay, GoDaddy]
---
Given a **non-empty** string s and a dictionary *wordDict* containing a list of **non-empty** words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.  

# Note:  
- The same word in the dictionary may be reused multiple times in the segmentation.
- You may assume the dictionary does not contain duplicate words.

# Example 1:  
	Input: s = "leetcode", wordDict = ["leet", "code"]
	Output: true
	Explanation: Return true because "leetcode" can be segmented as "leet code".

# Example 2:  
	Input: s = "applepenapple", wordDict = ["apple", "pen"]
	Output: true
	Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
	             Note that you are allowed to reuse a dictionary word.

# Example 3:  
	Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
	Output: false

______________________  

# Solution

Time complexity : O(n^2)  
Space complexity : O(n)  

	class Solution {
	public:
	    bool wordBreak(string s, vector<string>& wordDict) {
	        for (string word: wordDict) {
	            m_[word] = true;
	        }
	        return helper(s);
	    }
	private:
	    unordered_map<string, bool> m_;
	    bool helper(const string& s) {
	        if (m_.count(s)) return m_[s];
	        
	        // for each break point in s
	        for (int i=1; i<s.length(); ++i) {
	            auto it = m_.find(s.substr(i));
	            if (it != m_.end() && it->second && helper(s.substr(0, i)))
	                return m_[s] = true;
	        }
	        return m_[s] = false;
	    }
	};

memorized recursive.  
記憶已算過的答案，避免重覆計算，加快速度。  