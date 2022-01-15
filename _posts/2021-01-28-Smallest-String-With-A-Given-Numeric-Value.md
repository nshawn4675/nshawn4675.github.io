---
layout: post
title: "[LeetCode January Challange] Day 28 - Smallest String With A Given Numeric Value"
date: 2021-01-28 00:00:00 +0800
categories: LeetCode
tags: [Medium, String, Greedy, Lendingkart, C++]
---
The **numeric value** of a **lowercase character** is defined as its position <font color="red">(1-indexed)</font> in the alphabet, so the numeric value of <font color="red">a</font> is <font color="red">1</font>, the numeric value of <font color="red">b</font> is <font color="red">2</font>, the numeric value of <font color="red">c</font> is <font color="red">3</font>, and so on.

The **numeric value** of a **string** consisting of lowercase characters is defined as the sum of its characters' numeric values. For example, the numeric value of the string <font color="red">"abe"</font> is equal to <font color="red">1 + 2 + 5 = 8</font>.

You are given two integers <font color="red">n</font> and <font color="red">k</font>. Return *the **lexicographically smallest string** with **length** equal to <font color="red">n</font> and **numeric value** equal to <font color="red">k</font>*.

Note that a string <font color="red">x</font> is lexicographically smaller than string <font color="red">y</font> if <font color="red">x</font> comes before <font color="red">y</font> in dictionary order, that is, either <font color="red">x</font> is a prefix of <font color="red">y</font>, or if <font color="red">i</font> is the first position such that <font color="red">x[i] != y[i]</font>, then <font color="red">x[i]</font> comes before <font color="red">y[i]</font> in alphabetic order.

# Example 1:

	Input: n = 3, k = 27
	Output: "aay"
	Explanation: The numeric value of the string is 1 + 1 + 25 = 27, and it is the smallest string with such a value and length equal to 3.

# Example 2:

	Input: n = 5, k = 73
	Output: "aaszz"

# Constraints:

- <font color="red">1 <= n <= 10^5</font>
- <font color="red">n <= k <= 26 * n</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    string getSmallestString(int n, int k) {
	        string ans(n, 'a');
	        k -= n;
	        while (0 < k) {
	            int diff = min(k, 25);
	            ans[--n] += diff;
	            k -= diff;
	        }
	        return ans;
	    }
	};

先用 a 鋪地毯，再由後往前加至最大的字母。