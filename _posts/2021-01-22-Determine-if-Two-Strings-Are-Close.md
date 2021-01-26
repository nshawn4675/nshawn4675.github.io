---
layout: post
title:  "[LeetCode January Challange] Day 22 - Determine if Two Strings Are Close"
date:   2021-01-22 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Greedy, Postmates]
---
Two strings are considered **close** if you can attain one from the other using the following operations:

- Operation 1: Swap any two **existing** characters.
	- For example, <font color="red">abcde -> aecdb</font>
- Operation 2: Transform **every** occurrence of one **existing** character into another **existing** character, and do the same with the other character.
	- For example, <font color="red">aacabb -> bbcbaa</font> (all <font color="red">a</font>'s turn into <font color="red">b</font>'s, and all <font color="red">b</font>'s turn into <font color="red">a</font>'s)
You can use the operations on either string as many times as necessary.

Given two strings, <font color="red">word1</font> and <font color="red">word2</font>, return <font color="red">true</font> *if <font color="red">word1</font> and <font color="red">word2</font> are **close**, and <font color="red">false</font> otherwise.*

# Example 1:

	Input: word1 = "abc", word2 = "bca"
	Output: true
	Explanation: You can attain word2 from word1 in 2 operations.
	Apply Operation 1: "abc" -> "acb"
	Apply Operation 1: "acb" -> "bca"

# Example 2:

	Input: word1 = "a", word2 = "aa"
	Output: false
	Explanation: It is impossible to attain word2 from word1, or vice versa, in any number of operations.

# Example 3:

	Input: word1 = "cabbba", word2 = "abbccc"
	Output: true
	Explanation: You can attain word2 from word1 in 3 operations.
	Apply Operation 1: "cabbba" -> "caabbb"
	Apply Operation 2: "caabbb" -> "baaccc"
	Apply Operation 2: "baaccc" -> "abbccc"

# Example 4:

	Input: word1 = "cabbba", word2 = "aabbss"
	Output: false
	Explanation: It is impossible to attain word2 from word1, or vice versa, in any amount of operations.

# Constraints:

- <font color="red">1 <= word1.length, word2.length <= 10^5</font>
- **<font color="red">word1</font>** and <font color="red">word2</font> contain only lowercase English letters.

______________________  

# Solution  

# Hash Table

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    bool closeStrings(string word1, string word2) {
	        if (word1.size() != word2.size()) return false;
	        
	        unordered_map<char, int> ht1, ht2;
	        for (char c: word1) ++ht1[c];
	        for (char c: word2) ++ht2[c];
	        
	        vector<int> set1, w_cnt1, set2, w_cnt2;
	        for (auto pair: ht1) {
	            set1.push_back(pair.first);
	            w_cnt1.push_back(pair.second);
	        }
	        for (auto pair: ht2) {
	            set2.push_back(pair.first);
	            w_cnt2.push_back(pair.second);
	        }
	        
	        sort(set1.begin(), set1.end());
	        sort(set2.begin(), set2.end());
	        if (set1 != set2) return false;
	        
	        sort(w_cnt1.begin(), w_cnt1.end());
	        sort(w_cnt2.begin(), w_cnt2.end());
	        return w_cnt1 == w_cnt2;
	    }
	};

word1 和 word2 為 close，代表可由某一方做數次下列 2 運算得到另一方：
1. 該字中某兩字調換位置。(即可以任意換位)
2. 該字中某兩字母出現頻率對調。(即可以變換字母)

因此可推得若下列兩條件其一成立，word1 與 word2 不為close：
1. 某一方出現另一方沒出現過的字母。
2. 整體上各個字母出現頻率不一樣。

此方法利用 hash table 記錄 word1 和 word2 出現了哪些字母，出現了多少次。  
再用 vector 做條件一、二的判別。

# Frequency Array Map

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    bool closeStrings(string word1, string word2) {
	        if (word1.size() != word2.size()) return false;
	        
	        vector<int> w_cnt1(26, 0), w_cnt2(26, 0);
	        for (char c: word1) ++w_cnt1[c-'a'];
	        for (char c: word2) ++w_cnt2[c-'a'];
	        
	        for (int i=0; i<26; ++i) {
	            if ((w_cnt1[i] == 0 && w_cnt2[i] != 0) ||
	                (w_cnt1[i] != 0 && w_cnt2[i] == 0))
	            {
	                return false;
	            }
	        }
	        sort(w_cnt1.begin(), w_cnt1.end());
	        sort(w_cnt2.begin(), w_cnt2.end());
	        return w_cnt1 == w_cnt2;
	    }
	};

利用長為 26 的 vector，從頭開始分別存放 a 出現了幾次？ b 出現了幾次？ ... 以此類推。  
再利用此 vector 做條件一、條件二的判別。

# Bitwise Operation & Frequency Array Map

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    bool closeStrings(string word1, string word2) {
	        if (word1.size() != word2.size()) return false;
	        
	        vector<int> w_cnt1(26, 0), w_cnt2(26, 0);
	        int bitmap1 = 0, bitmap2 = 0;
	        for (char c: word1) {
	            ++w_cnt1[c-'a'];
	            bitmap1 |= 1 << c-'a';
	        }
	        for (char c: word2) {
	            ++w_cnt2[c-'a'];
	            bitmap2 |= 1 << c-'a';
	        }
	        
	        if (bitmap1 != bitmap2) return false;
	        
	        sort(w_cnt1.begin(), w_cnt1.end());
	        sort(w_cnt2.begin(), w_cnt2.end());
	        return w_cnt1 == w_cnt2;
	    }
	};

與上者雷同，差在用 bitmap 來檢查條件一。  
由右至左，第一個 bit 代表 a 有無出現過，第二個 bit 代表 b 有無出現過，... 以此類推。  
