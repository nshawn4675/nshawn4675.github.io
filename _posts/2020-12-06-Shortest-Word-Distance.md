---
layout: post
title: "Shortest Word Distance"
date: 2020-12-06 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Array, Goldman Sachs]
---

Given a list of words and two words _word1_ and _word2_, return the shortest distance between these two words in the list.

# Example:

Assume that words = <font color="red">["practice", "makes", "perfect", "coding", "makes"]</font>.

    Input: word1 = "coding", word2 = "practice"
    Output: 3

<!--seperate code-->

    Input: word1 = "makes", word2 = "coding"
    Output: 1

# Note:

You may assume that _word1_ **does not equal to** _word2_, and _word1_ and _word2_ are both in the list.

---

# Solution

Time complexity : O(n)  
Space complexity : O(1)

    class Solution {
    public:
        int shortestDistance(vector<string>& words, string word1, string word2) {
            int min_dist = INT_MAX;
            int idx1 = -1, idx2 = -1;
            for (int i=0; i<words.size(); ++i) {
                if (words[i] == word1) idx1 = i;
                if (words[i] == word2) idx2 = i;
                if (0 <= idx1 && 0 <= idx2)
                    min_dist = min(min_dist, abs(idx1-idx2));
            }
            return min_dist;
        }
    };
