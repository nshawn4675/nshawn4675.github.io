---
layout: post
title:  "161. One Edit Distance"
date:   2021-01-28 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, String, Facebook, Amazon, Yandex]
---
Given two strings <font color="red">s</font> and <font color="red">t</font>, return <font color="red">true</font> if they are both one edit distance apart, otherwise return <font color="red">false</font>.

A string <font color="red">s</font> is said to be one distance apart from a string <font color="red">t</font> if you can:

- Insert **exactly one** character into <font color="red">s</font> to get <font color="red">t</font>.
- Delete **exactly one** character from <font color="red">s</font> to get <font color="red">t</font>.
- Replace **exactly one** character of <font color="red">s</font> with **a different character** to get <font color="red">t</font>.

# Example 1:

	Input: s = "ab", t = "acb"
	Output: true
	Explanation: We can insert 'c' into s to get t.

# Example 2:

	Input: s = "", t = ""
	Output: false
	Explanation: We cannot get t from s by only one step.

# Example 3:

	Input: s = "a", t = ""
	Output: true

# Example 4:

	Input: s = "", t = "A"
	Output: true

# Constraints:

- <font color="red">0 <= s.length <= 10^4</font>
- <font color="red">0 <= t.length <= 10^4</font>
- **<font color="red">s</font>** and <font color="red">t</font> consist of lower-case letters, upper-case letters <font color="red">and/or</font> digits.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

class Solution {
public:
    bool isOneEditDistance(string s, string t) {
        const int sn = s.size(), tn = t.size();
        if (tn < sn) return isOneEditDistance(t, s);
        if (1 < tn - sn) return false;
        
        for (int i=0; i<sn; ++i) {
            if (s[i] != t[i]) {
                if (sn == tn)
                    return s.substr(i+1)==t.substr(i+1);
                else
                    return s.substr(i)==t.substr(i+1);
            }
        }
        return sn + 1 == tn;
    }
};