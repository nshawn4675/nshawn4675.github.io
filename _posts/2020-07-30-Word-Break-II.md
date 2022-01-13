---
layout: post
title:  "[LeetCode July Challange]Day30-Word Break II"
date:   2020-07-30 00:00:00 +0800
categories: LeetCode
tags: [Hash Table, String, Dynamic Programming, Backtracking, Trie, Memoization, C++]
---
Given a **non-empty** string *s* and a dictionary *wordDict* containing a list of **non-empty** words, add spaces in s to construct a sentence where each word is a valid dictionary word. Return all such possible sentences.

# Note:  
- The same word in the dictionary may be reused multiple times in the segmentation.
- You may assume the dictionary does not contain duplicate words.

# Example 1:  
	Input:
	s = "catsanddog"
	wordDict = ["cat", "cats", "and", "sand", "dog"]
	Output:
	[
	  "cats and dog",
	  "cat sand dog"
	]

# Example 2:  
	Input:
	s = "pineapplepenapple"
	wordDict = ["apple", "pen", "applepen", "pine", "pineapple"]
	Output:
	[
	  "pine apple pen apple",
	  "pineapple pen apple",
	  "pine applepen apple"
	]
	Explanation: Note that you are allowed to reuse a dictionary word.

# Example 3:  
	Input:
	s = "catsandog"
	wordDict = ["cats", "dog", "sand", "and", "cat"]
	Output:
	[]

______________________  

# solution
time complexity : O(2^n)  
space complexity : O(2^n)

	class Solution {
	public:
	    vector<string> wordBreak(string s, vector<string>& wordDict) {
	        unordered_set<string> dict(wordDict.begin(), wordDict.end());
	        return wordBreak(s, dict);        
	    }
	private:
	    unordered_map<string, vector<string>> mem_;
	    vector<string> append(vector<string> prefixs, string word) {
	        for (int i=0; i<prefixs.size(); ++i) {
	            prefixs[i] += " " + word;
	        }
	        return prefixs;
	    }
	    
	    vector<string> wordBreak(string s, unordered_set<string> dict) {
	        if (mem_.count(s)) return mem_[s];
	        
	        vector<string> ans;
	        
	        if (dict.count(s)) ans.push_back(s);
	        
	        for (int i=0; i<s.length(); ++i) {
	            string right = s.substr(i);
	            if (!dict.count(right)) continue;
	            string left = s.substr(0, i);
	            vector<string> tmpAns = append(wordBreak(left, dict), right);
	            ans.insert(ans.end(), tmpAns.begin(), tmpAns.end());
	        }
	        
	        return mem_[s] = ans;
	    }
	};

利用計劃遞歸的方式完成，
遞歸的終止條件：若此字串s之前已有相對應的答案，則回傳答案。  
將此字串s，從左至右，切割成2字串，若右邊字串出現在題目給定的wordDict中的話，左邊的字串遞歸求解，與右字串接在一起。  
例："catsanddog", dict : {"cat", "cats", "sand", "and", "dog"}  
wordBreak("catsand")+" dog"  
{wordBreak("cat")+" sand", wordBreak("cats")+" and"}+" dog"  
{"cat sand", "cats and"}+" dog"  
{"cat sand dog", "cats and dog"}  