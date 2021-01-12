---
layout: post
title:  "[LeetCode January Challange] Day 9 - Word Ladder"
date:   2021-01-09 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Hard, Breadth-first Search, Amazon Lyft, Faceboook, Google, Qualtrics, Microsoft, Bloomberg, Zillow, Oracle, Uber, Yahoo, Apple, Citadel]
---
Given two words <font color="red">beginWord</font> and <font color="red">endWord</font>, and a dictionary <font color="red">wordList</font>, return *the length of the shortest transformation sequence from <font color="red">beginWord</font> to <font color="red">endWord</font>, such that:*

- Only one letter can be changed at a time.
- Each transformed word must exist in the word list.
Return <font color="red">0</font> if there is no such transformation sequence.

# Example 1:

	Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
	Output: 5
	Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog", return its length 5.

# Example 2:

	Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
	Output: 0
	Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.

# Constraints:

- <font color="red">1 <= beginWord.length <= 100</font>
- <font color="red">endWord.length == beginWord.length</font>
- <font color="red">1 <= wordList.length <= 5000</font>
- <font color="red">wordList[i].length == beginWord.length</font>
- **<font color="red">beginWord</font>**, <font color="red">endWord</font>, and wordList[i] consist of lowercase English letters.
- <font color="red">beginWord != endWord</font>
- All the strings in <font color="red">wordList</font> are **unique**.

______________________  

# Solution  

# BFS  

Time complexity : O(26^l \* n) l: word len, n: # wordlist  
Space complexity : O(n)  

	class Solution {
	public:
	    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
	        unordered_set<string> dict(wordList.begin(), wordList.end());
	        if (!dict.count(endWord)) return 0;
	        
	        int l = beginWord.size();
	        int step = 0;
	        queue<string> q;
	        q.push(beginWord);
	        while (!q.empty()) {
	            ++step;
	            queue<string> next_q;
	            while (!q.empty()) {
	                string cur_s = q.front(); q.pop();
	                for (int i=0; i<l; ++i) {
	                    char orig_c = cur_s[i];
	                    for (char next_c='a'; next_c<='z'; ++next_c) {
	                        if (next_c == orig_c) continue;
	                        cur_s[i] = next_c;
	                        if (cur_s == endWord) return step+1;
	                        if (!dict.count(cur_s)) continue;
	                        dict.erase(cur_s);
	                        next_q.push(cur_s);
	                    }
	                    cur_s[i] = orig_c;
	                }
	            }
	            q = next_q;
	        }
	        
	        return 0;
	    }
	};

可用 graph traversal 的觀點來看此題。  
start node 為 beginWord，將 node 中各個字母依序換成 a...z 可得到往外一圈的擴展。  
若擴展出來的字存在 wordList 中才留著，其它不保留。  
直到擴展到 endWord 為止，看擴了幾圈。  


# Bidirectional BFS  

	class Solution {
	public:
	    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
	        unordered_set<string> dict(wordList.begin(), wordList.end());
	        if (!dict.count(endWord)) return 0;
	        
	        unordered_set<string> q1({beginWord});
	        unordered_set<string> q2({endWord});
	        int step = 0;
	        int l = beginWord.size();
	        while (!q1.empty() && !q2.empty()) {
	            ++step;
	            
	            // always expand the small one first.
	            if (q1.size() > q2.size())
	                swap(q1, q2);
	            
	            unordered_set<string> next_q;
	            for (string s: q1) {
	                for (int i=0; i<l; ++i) {
	                    char orig_c = s[i];
	                    for (char c='a'; c<='z'; ++c) {
	                        if (c == orig_c) continue;
	                        s[i] = c;
	                        if (q2.count(s)) return step+1;
	                        if (!dict.count(s)) continue;
	                        next_q.insert(s);
	                        dict.erase(s);
	                    }
	                    s[i] = orig_c;
	                }
	            }
	            swap(q1, next_q);
	        }
	        return 0;
	    }
	};

減少計算量，start 與 end node 輪流跑 BFS，若其中一方跑到的字存在於另一方的 q 中，就結束了。