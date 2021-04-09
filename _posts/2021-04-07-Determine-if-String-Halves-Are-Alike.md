---
layout: post
title:  "[LeetCode April Challange] Day 07 - Determine if String Halves Are Alike"
date:   2021-04-07 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, String]
---
You are given a string <font color="red">s</font> of even length. Split this string into two halves of equal lengths, and let <font color="red">a</font> be the first half and <font color="red">b</font> be the second half.

Two strings are **alike** if they have the same number of vowels (<font color="red">'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'</font>). Notice that <font color="red">s</font> contains uppercase and lowercase letters.

Return <font color="red">true</font> *if <font color="red">a</font> and <font color="red">b</font> are **alike***. Otherwise, return <font color="red">false</font>.

# Example 1:

    Input: s = "book"
    Output: true
    Explanation: a = "bo" and b = "ok". a has 1 vowel and b has 1 vowel. Therefore, they are alike.

# Example 2:

    Input: s = "textbook"
    Output: false
    Explanation: a = "text" and b = "book". a has 1 vowel whereas b has 2. Therefore, they are not alike.
    Notice that the vowel o is counted twice.

# Example 3:

    Input: s = "MerryChristmas"
    Output: false

# Example 4:

    Input: s = "AbCdEfGh"
    Output: true

# Constraints:

- <font color="red">2 <= s.length <= 1000</font>
- **<font color="red">s.length</font>** is even.
- **<font color="red">s</font>** consists of **uppercase and lowercase** letters.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

    class Solution {
    public:
        bool halvesAreAlike(string s) {
            const int s_len = s.length();
            const string vowels = "aeiouAEIOU";
            int cnt1 = 0, cnt2 = 0;
            for (int i=0; i<s_len; ++i) {
                if (vowels.find(s[i]) != string::npos) {
                    if (i<s_len/2) ++cnt1;
                    else ++cnt2;
                }
            }
            return cnt1 == cnt2;
        }
    };