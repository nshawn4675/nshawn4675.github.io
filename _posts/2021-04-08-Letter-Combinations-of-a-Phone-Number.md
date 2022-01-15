---
layout: post
title: "[LeetCode April Challange] Day 08 - Letter Combinations of a Phone Number"
date: 2021-04-08 00:00:00 +0800
categories: LeetCode
tags: [Medium, Hash Table, String, Backtracking, Amazon, Microsoft, Twilio, Facebook, Capital One, eBay, Google, Uber, Apple, Oracle, JPMorgan, Morgan Stanley, Tesla, Qualtrics, Samsung, C++]
---
Given a string containing digits from <font color="red">2-9</font> inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/17_ex.png?raw=true)

# Example 1:

    Input: digits = "23"
    Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]

# Example 2:

    Input: digits = ""
    Output: []

# Example 3:

    Input: digits = "2"
    Output: ["a","b","c"]

# Constraints:

- <font color="red">0 <= digits.length <= 4</font>
- **<font color="red">digits[i]</font>** is a digit in the range <font color="red">['2', '9']</font>.

______________________  

# Solution  

# DFS

Time complexity : O(4^n)  
Space complexity : O(n)  

    class Solution {
    public:
        vector<string> letterCombinations(string digits) {
            ans = {};
            if (digits == "") return ans;
            
            m[2] = "abc";
            m[3] = "def";
            m[4] = "ghi";
            m[5] = "jkl";
            m[6] = "mno";
            m[7] = "pqrs";
            m[8] = "tuv";
            m[9] = "wxyz";
            
            string cur = "";
            dfs(cur, digits);
            return ans;
        }
    private:
        string m[10];
        vector<string> ans;
        void dfs(string &cur, string &digits) {
            if (cur.length() == digits.length()) {
                ans.push_back(cur);
                return;
            }
            
            int i = cur.length();
            for (char c: m[digits[i]-'0']) {
                cur.push_back(c);
                dfs(cur, digits);
                cur.pop_back();
            }
        }
    };

使用 backtracking 的技巧，歷遍所有排列組合。

# BFS

Time complexity : O(4^n)  
Space complexity : O(4^n)  

    class Solution {
    public:
        vector<string> letterCombinations(string digits) {
            if (digits == "") return {};
            
            string m[10];
            m[2] = "abc";
            m[3] = "def";
            m[4] = "ghi";
            m[5] = "jkl";
            m[6] = "mno";
            m[7] = "pqrs";
            m[8] = "tuv";
            m[9] = "wxyz";
            
            vector<string> ans = {""};
            for (char d: digits) {
                vector<string> next;
                for (string s: ans) {
                    for (char c: m[d-'0'])
                        next.push_back(s+c);
                }
                ans.swap(next);
            }
            return ans;
        }
    };