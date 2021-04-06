---
layout: post
title:  "[LeetCode April Challange] Day 03 - Longest Valid Parentheses"
date:   2021-04-03 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Hard, String, Dynamic Programming, Amazon, Facebook, Apple, ByteDance]
---
Given a string containing just the characters <font color="red">'('</font> and <font color="red">')'</font>, find the length of the longest valid (well-formed) parentheses substring.

# Example 1:

    Input: s = "(()"
    Output: 2
    Explanation: The longest valid parentheses substring is "()".

# Example 2:

    Input: s = ")()())"
    Output: 4
    Explanation: The longest valid parentheses substring is "()()".

# Example 3:

    Input: s = ""
    Output: 0

# Constraints:

- <font color="red">0 <= s.length <= 3 * 10^4</font>
- **<font color="red">s[i]</font>** is <font color="red">'('</font>, or <font color="red">')'</font>.

______________________  

# Solution  

# Brute Force  

Time complexity : O(n^3)  
Space complexity : O(n)  

    class Solution {
    public:
        int longestValidParentheses(string s) {
            int ans = 0;
            for (int i=0; i<s.length(); ++i) {
                for (int j=2; i+j<=s.length(); j+=2) {
                    if (isValidParentheses(s.substr(i, j)))
                        ans = max(ans, j);
                }
            }
            return ans;
        }
    private:
        bool isValidParentheses(string s) {
            stack<char> stk;
            for (char c: s) {
                if (c == '(') stk.push('(');
                else if (!stk.empty()) stk.pop();
                else return false;
            }
            return stk.empty();
        }
    };

檢查所有子字串的合理性，若合理，則更新最長值。


# DP

Time complexity : O(n)  
Space complexity : O(n)  

    class Solution {
    public:
        int longestValidParentheses(string s) {
            int ans = 0;
            vector<int> dp(s.length(), 0);
            for (int i=1; i<s.length(); ++i) {
                if (s[i] == ')') {
                    if (s[i-1] == '(')
                        dp[i] = (0 <= i-2 ? dp[i-2] : 0) + 2;
                    else if ((0 <= i-dp[i-1]-1) && s[i-dp[i-1]-1] == '(')
                        dp[i] = dp[i-1] + (0<=i-dp[i-1]-2 ? dp[i-dp[i-1]-2] : 0) + 2;
                    ans = max(ans, dp[i]);
                }
            }
            return ans;
        }
    };

建立一 dp array，其初始值為 0。  
因合理的 parentheses 只結尾於 ')'，故只有在看到s\[i\]為')'時，才做事情。  
1. case '...()'，則 dp\[i\] = dp\[i-2\](...) + 2，需做 0<=i-2 的防呆。
2. case '...(合理括號)'，則 dp\[i\] = dp\[i-1\](合理括號長) + dp\[i-dp\[i-1\]-2\](...) + 2，一樣需做防呆。

更新ans。


# stack

Time complexity : O(n)  
Space complexity : O(n)  

    class Solution {
    public:
        int longestValidParentheses(string s) {
            int ans = 0;
            stack<int> stk;
            stk.push(-1);
            for (int i=0; i<s.length(); ++i) {
                if (s[i] == '(') stk.push(i);
                else {
                    stk.pop();
                    if (stk.empty())stk.push(i);
                    else ans = max(ans, i-stk.top());
                }
            }
            return ans;
        }
    };

用 stack 記錄 '(' 的位置，若遇到 ')' 則 pop 掉最新的 '('，並計算長度。


# No Extra Space

Time complexity : O(n)  
Space complexity : O(1)  

    class Solution {
    public:
        int longestValidParentheses(string s) {
            int ans = 0;
            
            int cnt_l = 0, cnt_r = 0;
            for (int i=0; i<s.length(); ++i) {
                if (s[i] == '(') ++cnt_l;
                else ++cnt_r;
                
                if (cnt_l == cnt_r)
                    ans = max(ans, cnt_l + cnt_r);
                else if (cnt_l < cnt_r)
                    cnt_l = cnt_r = 0;
            }
            
            cnt_l = cnt_r = 0;
            for (int i=s.length()-1; 0<=i; --i) {
                if (s[i] == ')') ++cnt_r;
                else ++cnt_l;
                
                if (cnt_l == cnt_r)
                    ans = max(ans, cnt_l + cnt_r);
                else if (cnt_l > cnt_r)
                    cnt_l = cnt_r = 0;
            }
            
            return ans;
        }
    };

左到右掃一次，記錄 '(' 和 ')' 出現的次數。  
在 '(' > ')' 的條件下，若 '(' == ')'，則可形成合理的括號。  
若 '(' < ')'，則不可能形成合理的括號，將 '(' 、 ')' 計數歸 0。

類似的事情，由右到左再做一次。