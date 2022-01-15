---
layout: post
title: "[LeetCode April Challange] Day 09 - Verifying an Alien Dictionary"
date: 2021-04-09 00:00:00 +0800
categories: LeetCode
tags: [Easy, Array, Hash Table, String, Facebook, Walmart Labs, Amazon, C++]
---
In an alien language, surprisingly they also use english lowercase letters, but possibly in a different <font color="red">order</font>. The <font color="red">order</font> of the alphabet is some permutation of lowercase letters.

Given a sequence of <font color="red">words</font> written in the alien language, and the <font color="red">order</font> of the alphabet, return <font color="red">true</font> if and only if the given <font color="red">words</font> are sorted lexicographicaly in this alien language.

# Example 1:

    Input: words = ["hello","leetcode"], order = "hlabcdefgijkmnopqrstuvwxyz"
    Output: true
    Explanation: As 'h' comes before 'l' in this language, then the sequence is sorted.

# Example 2:

    Input: words = ["word","world","row"], order = "worldabcefghijkmnpqstuvxyz"
    Output: false
    Explanation: As 'd' comes after 'l' in this language, then words[0] > words[1], hence the sequence is unsorted.

# Example 3:

    Input: words = ["apple","app"], order = "abcdefghijklmnopqrstuvwxyz"
    Output: false
    Explanation: The first three characters "app" match, and the second string is shorter (in size.) According to lexicographical rules "apple" > "app", because 'l' > '∅', where '∅' is defined as the blank character which is less than any other character (More info).

# Constraints:

- <font color="red">1 <= words.length <= 100</font>
- <font color="red">1 <= words[i].length <= 20</font>
- <font color="red">order.length == 26</font>
- All characters in <font color="red">words[i]</font> and <font color="red">order</font> are English lowercase letters.

______________________  

# Solution  

Time complexity : O(sum(len(words)))  
Space complexity : O(26)  

    class Solution {
    public:
        bool isAlienSorted(vector<string>& words, string order) {
            char m[26];
            for (int i=0; i<26; ++i)
                m[order[i]-'a'] = 'a' + i;
            for (int i=0; i<size(words); ++i) {
                for (int j=0; j<words[i].length(); ++j)
                    words[i][j] = m[words[i][j]-'a'];
                if (0<i && words[i-1] > words[i]) return false;
            }
            return true;
        }
    };

建立一個還原表，從 alien order 換回 human order。  
再將各個 word 轉換回 human，再檢查是否有由小到大排序。  