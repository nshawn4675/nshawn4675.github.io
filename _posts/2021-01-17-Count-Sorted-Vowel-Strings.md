---
layout: post
title:  "[LeetCode January Challange] Day 17 - Count Sorted Vowel Strings"
date:   2021-01-17 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Math, Dynamic Programming, Backtracking, Nira Finance]
---
Given an integer <font color="red">n</font>, return *the number of strings of length <font color="red">n</font> that consist only of vowels (<font color="red">a, e, i, o, u</font>) and are **lexicographically sorted.***  

A string <font color="red">s</font> is **lexicographically sorted** if for all valid <font color="red">i, s[i]</font> is the same as or comes before <font color="red">s[i+1]</font> in the alphabet.  

# Example 1:

	Input: n = 1
	Output: 5
	Explanation: The 5 sorted strings that consist of vowels only are ["a","e","i","o","u"].

# Example 2:

	Input: n = 2
	Output: 15
	Explanation: The 15 sorted strings that consist of vowels only are
	["aa","ae","ai","ao","au","ee","ei","eo","eu","ii","io","iu","oo","ou","uu"].
	Note that "ea" is not a valid string since 'e' comes after 'a' in the alphabet.

# Example 3:

	Input: n = 33
	Output: 66045

# Constraints:

- <font color="red">1 <= n <= 50</font>

______________________  

# Solution  

# Backtracking

Time complexity : O(n^5)  
Space complexity : O(n)  

	class Solution {
	public:
	    int countVowelStrings(int n) {
	        return backtrack(n, 1);
	    }
	private:
	    int backtrack(int n, int vowel) {
	        if (n == 0) return 1;
	        int res = 0;
	        for (int i=vowel; i<=5; ++i)
	            res += backtrack(n-1, i);
	        return res;
	    }
	};

vowel 代表還有哪些字可以塞，n 代表還可以塞多少個字。  
由前往後 backtracking。

# Recusion

Time complexity : O(n^5)  
Space complexity : O(n)  

	class Solution {
	public:
	    int countVowelStrings(int n) {
	        return recursion(n, 5);
	    }
	private:
	    int recursion(int n, int vowel) {
	        // n = remain len, vowel = available vowels.
	        if (n == 1) return vowel;
	        if (vowel == 1) return 1;
	        return recursion(n, vowel-1) + recursion(n-1, vowel);
	    }
	};

用目前的 vowel 組成長度為 n 的字串。  
此答案可拆解為下面兩部份：  
1. 最後一個位置是最後一個字母：再用所有字母，求長度-1的解(因最後一個字母前面可以是任何字母)。
2. 最後一個位置是其它字母：長度不變，但不考慮最後一個字母的解。

# Recusion + Memoization (Top Down Dynamic Programming)

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    int countVowelStrings(int n) {
	        m_ = vector<vector<int>>(n+1, vector<int>(6, 0));
	        return recursion(n, 5);
	    }
	private:
	    int recursion(int n, int vowel) {
	        // n = remain len, vowel = available vowels.
	        if (n == 1) return vowel;
	        if (vowel == 1) return 1;
	        
	        if (0 < m_[n][vowel]) return m_[n][vowel];
	        else return m_[n][vowel] = recursion(n, vowel-1) + recursion(n-1, vowel);
	    }
	    vector<vector<int>> m_;
	};

# Bottom Up Dynamic Programming (Tabulation)

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    int countVowelStrings(int n) {
	        vector<vector<int>>dp = vector<vector<int>>(n+1, vector<int>(6, 0));
	        for (int v=1; v<=5; ++v)
	            dp[1][v] = v;
	        for (int i=1; i<=n; ++i)
	            dp[i][1] = 1;
	        for (int i=2; i<=n; ++i) {
	            for (int v=1; v<=5; ++v) {
	                dp[i][v] = dp[i-1][v] + dp[i][v-1];
	            }
	        }
	        return dp[n][5];
	    }
	};

# Math

Time complexity : O(1)  
Space complexity : O(1)

	class Solution {
	public:
	    int countVowelStrings(int n) {
	        return (n+4)*(n+3)*(n+2)*(n+1)/24;
	    }
	};

利用組合公式：c(k, n) = (k+n-1)!/(k-1)!n!  
c(5, n)  
= (5+n-1)!/(5-1)!n!  
= (n+4)!/4!n!  
= (n+4)(n+3)(n+2)(n+1)n!/4x3x2x1xn!  
= (n+4)(n+3)(n+2)(n+1)/24  