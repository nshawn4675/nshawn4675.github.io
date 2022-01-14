---
layout: post
title:  "[LeetCode October Challange] Day 12 - Buddy Strings"
date:   2020-10-12 00:00:00 +0800
categories: LeetCode
tags: [Easy, Hash Table, String, Facebook, C++]
---
Given two strings <font color="red">A</font> and <font color="red">B</font> of lowercase letters, return <font color="red">true</font> *if you can swap two letters in* <font color="red">A</font> *so the result is equal to* <font color="red">B</font>, *otherwise, return* <font color="red">false</font>.  

Swapping letters is defined as taking two indices <font color="red">i</font> and <font color="red">j</font> (0-indexed) such that <font color="red">i != j</font> and swapping the characters at <font color="red">A[i]</font> and <font color="red">A[j]</font>. For example, swapping at indices <font color="red">0</font> and <font color="red">2</font> in <font color="red">"abcd"</font> results in <font color="red">"cbad"</font>.

# Example 1:  
	Input: A = "ab", B = "ba"
	Output: true
	Explanation: You can swap A[0] = 'a' and A[1] = 'b' to get "ba", which is equal to B.

# Example 2:  
	Input: A = "ab", B = "ab"
	Output: false
	Explanation: The only letters you can swap are A[0] = 'a' and A[1] = 'b', which results in "ba" != B.

# Example 3:  
	Input: A = "aa", B = "aa"
	Output: true
	Explanation: You can swap A[0] = 'a' and A[1] = 'a' to get "aa", which is equal to B.

# Example 4:  
	Input: A = "aaaaaaabc", B = "aaaaaaacb"
	Output: true

# Example 5:  
	Input: A = "", B = "aa"
	Output: false

# Constraints:  
- <font color="red">0 <= A.length <= 20000</font>
- <font color="red">0 <= B.length <= 20000</font>
- **<font color="red">A</font>** and <font color="red">B</font> consist of lowercase letters.


______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    bool buddyStrings(string A, string B) {
	        if (A.size() != B.size()) return false;
	        int a_cnt[26] = {0}, b_cnt[26] = {0};
	        int diff = 0;
	        for (int i=0; i<A.size(); ++i) {
	            if (A[i]!=B[i] && ++diff>2) return false;
	            ++a_cnt[A[i]-'a'];
	            ++b_cnt[B[i]-'a'];
	        }
	        for (int i=0; i<26; ++i) {
	            if (0==diff && a_cnt[i]>1) return true;
	            if (a_cnt[i] != b_cnt[i]) return false;
	        }
	        return 2 == diff;
	    }
	};

根據題目表示，buddy string的性質為：
1. 長度相同。
2. 不相同之處為2，且各字母出現的頻率相同。
3. 不相同之處為0，有其中一字母出現的頻率為2以上。

先比較長度。  
統計不相同之處和各字母出現頻率。  
檢查各字母出現的頻率。  
檢查不相同之處。  