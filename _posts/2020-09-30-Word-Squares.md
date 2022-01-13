---
layout: post
title:  "Word Squares"
date:   2020-09-30 00:00:00 +0800
categories: LeetCode
tags: [Hard, Backtracking, Trie, Bloomberg, C++]
---
Given a set of words **(without duplicates)**, find all [word squares](https://en.wikipedia.org/wiki/Word_square) you can build from them.  

A sequence of words forms a valid word square if the *k*-th row and column read the exact same string, where 0 ≤ *k* < max(numRows, numColumns).  

For example, the word sequence <font color="red">["ball","area","lead","lady"]</font> forms a word square because each word reads the same both horizontally and vertically.  

	b a l l
	a r e a
	l e a d
	l a d y

# Note:  
1. There are at least 1 and at most 1000 words.
2. All words will have the exact same length.
3. Word length is at least 1 and at most 5.
4. Each word contains only lowercase English alphabet <font color="red">a-z</font>.

# Example 1:  
	Input:
	["area","lead","wall","lady","ball"]

	Output:
	[
	  [ "wall",
	    "area",
	    "lead",
	    "lady"
	  ],
	  [ "ball",
	    "area",
	    "lead",
	    "lady"
	  ]
	]

	Explanation:
	The output consists of two word squares. The order of output does not matter (just the order of words in each word square matters).

# Example 2:  
	Input:
	["abat","baba","atan","atal"]

	Output:
	[
	  [ "baba",
	    "abat",
	    "baba",
	    "atan"
	  ],
	  [ "baba",
	    "abat",
	    "baba",
	    "atal"
	  ]
	]

	Explanation:
	The output consists of two word squares. The order of output does not matter (just the order of words in each word square matters).

______________________  

# Solution

Time complexity : O(n^26l)  
Space complexity : O(nl)  

	class Solution {
	public:
	    vector<vector<string>> wordSquares(vector<string>& words) {
	        len = words[0].length();
	        for (string s: words)
	            build_prefix_tb(s);
	        for (string s: words) {
	            backtracking(1, {s});
	        }
	        return ans;
	    }
	private:
	    vector<vector<string>> ans;
	    unordered_map<string, vector<string>> prefix_words;
	    int len;
	    void build_prefix_tb(string& s) {
	        for (int i=1; i<=s.length(); ++i) {
	            string prefix = s.substr(0, i);
	            if (prefix_words.count(prefix) == 0) {
	                vector<string> words = {s};
	                prefix_words[prefix] = words;
	            } else {
	                prefix_words[prefix].push_back(s);
	            }
	        }
	    }
	    void backtracking(int step, vector<string> wordSquares) {
	        if (step == len) {
	            ans.push_back(wordSquares);
	            return;
	        }
	        
	        string prefix;
	        for (string s: wordSquares)
	            prefix += s[step];
	        
	        vector<string> candidates = prefix_words[prefix];
	        for (string s: candidates) {
	            wordSquares.push_back(s);
	            backtracking(step+1, wordSquares);
	            wordSquares.pop_back();
	        }
	    }
	};

先用給的words，做出prefix hash table。  
例：ball-> {"b": ["ball"], "ba": ["ball"], "bal": ["ball"], "ball":["ball"]}  

建出的hash table，相當於：f(prefix) → 符合該prefix的words。  

接著用backtracking的方式，找出word squares。