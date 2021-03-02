---
layout: post
title:  "[LeetCode February Challange] Day 24 - Score of Parentheses"
date:   2021-02-24 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, String, Stack, Amazon, Google]
---
Given a balanced parentheses string <font color="red">S</font>, compute the score of the string based on the following rule:

- **<font color="red">()</font>** has score 1
- **<font color="red">AB</font>** has score <font color="red">A + B</font>, where A and B are balanced parentheses strings.
- **<font color="red">(A)</font>** has score <font color="red">2 * A</font>, where A is a balanced parentheses string.

# Example 1:

	Input: "()"
	Output: 1

# Example 2:

	Input: "(())"
	Output: 2

# Example 3:

	Input: "()()"
	Output: 2

# Example 4:

	Input: "(()(()))"
	Output: 6

# Note:

1. **<font color="red">S</font>** is a balanced parentheses string, containing only <font color="red">(</font> and <font color="red">)</font>.
2. <font color="red">2 <= S.length <= 50</font>

______________________  

# Solution  

# Divide & Conquer

Time complexity : O(n^2)  
Space complexity : O(n)  

	class Solution {
	public:
	    int scoreOfParentheses(string S) {
	        return f(S, 0, S.size());
	    }
	private:
	    int f(string& s, int start, int end) {
	        int ans = 0;
	        int bal = 0;
	        for (int i=start; i<end; ++i) {
	            bal = s[i] == '(' ? ++bal : --bal;
	            if (bal == 0) {
	                if (i - start == 1) ++ans;
	                else ans += 2 * f(s, start+1, i);
	                start = i + 1;
	            }
	        }
	        return ans;
	    }
	};

bal 代表 balance，若 bal == 0 代表可形成 valid parentheses，開始計算分數：
1. 若 i - start == 1，代表是「()」，則 ans + 1。
2. 其它，則 ans 需加上這一段 valid parentheses 的分數，至於是多少，就要遞迴進去算。

ans 加完 start -> i 這一段的分數後，需更新 start 的位置至 i + 1。


# Stack

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    int scoreOfParentheses(string S) {
	        stack<int> stk;
	        stk.push(0);
	        for (char c: S) {
	            if (c == '(')
	                stk.push(0);
	            else {
	                int val = stk.top() == 0 ? 1 : 2 * stk.top();
	                stk.pop();
	                stk.top() += val;
	            }
	        }
	        return stk.top();
	    }
	};


# Count Cores

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int scoreOfParentheses(string S) {
	        int ans = 0;
	        int d = 0;
	        for (int i=0; i<S.size(); ++i) {
	            d = S[i] == '(' ? ++d : --d;
	            if (S[i] == ')' && S[i-1] == '(')
	                ans += 1 << d;
	        }
	        return ans;
	    }
	};

因有 () 才有 score，故只要判斷是多深的 ()，將其分數加總即可。