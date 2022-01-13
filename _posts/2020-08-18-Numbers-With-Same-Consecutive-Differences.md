---
layout: post
title:  "[LeetCode August Challange]Day18-Numbers With Same Consecutive Differences"
date:   2020-08-18 00:00:00 +0800
categories: LeetCode
tags: [Backtracking, Breadth-First-Search, C++]
---
Return all **non-negative** integers of length **<font color="red">N</font>** such that the absolute difference between every two consecutive digits is **<font color="red">K</font>**.  

Note that **every** number in the answer **must not** have leading zeros **except** for the number **<font color="red">0</font>** itself. For example, **<font color="red">01</font>** has one leading zero and is invalid, but **<font color="red">0</font>** is valid.  

You may return the answer in any order.  

# Example 1:  
	Input: N = 3, K = 7
	Output: [181,292,707,818,929]
	Explanation: Note that 070 is not a valid number, because it has leading zeroes.

# Example 2:  
	Input: N = 2, K = 1
	Output: [10,12,21,23,32,34,43,45,54,56,65,67,76,78,87,89,98]

# Note:  
1. **<font color="red">1 <= N <= 9</font>**
2. **<font color="red">0 <= K <= 9</font>**

______________________  

# Solution

Time complexity : O(10^n)  
Space complexity : O(n)

	class Solution {
	public:
	    vector<int> numsSameConsecDiff(int N, int K) {
	        for (int i=N>1; i<10; ++i) {
	            genS(to_string(i), N, K);
	        }
	        return res_;
	    }
	private:
	    vector<int> res_;
	    void genS(string s, int N, int K) {
	        if (s.length() == N)
	        	res_.push_back(stoi(s));
	        else {
	            int num = s.back()-'0';
	            for (int i=0; i<10; ++i) {
	                if (abs(num - i) == K)
	                    genS(s+to_string(i), N, K);
	            }
	        }
	    }
	};

若N為1，則第一個字由0開始，若N>1，則第一個字由1開始，去掉了多位數0為開頭的問題。  

由0~9，與目前字串的最後一個字相對應的數字比較，若=k，則將此數加入字串尾巴，直到字串長度達N。