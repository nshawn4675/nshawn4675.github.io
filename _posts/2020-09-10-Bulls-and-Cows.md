---
layout: post
title:  "[LeetCode September Challange]Day10-Bulls and Cows"
date:   2020-09-10 00:00:00 +0800
categories: LeetCode
tags: [Hash Table, String, Counting, C++]
---
You are playing the following [Bulls and Cows](https://en.wikipedia.org/wiki/Bulls_and_Cows) game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your friend will use successive guesses and hints to eventually derive the secret number.  

Write a function to return a hint according to the secret number and friend's guess, use **<font color="red">A</font>** to indicate the bulls and **<font color="red">B</font>** to indicate the cows.  

Please note that both secret number and friend's guess may contain duplicate digits.  

# Example 1:  
	Input: secret = "1807", guess = "7810"

	Output: "1A3B"

	Explanation: 1 bull and 3 cows. The bull is 8, the cows are 0, 1 and 7.

# Example 2:  
	Input: secret = "1123", guess = "0111"

	Output: "1A1B"

	Explanation: The 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow.

**Note:** You may assume that the secret number and your friend's guess only contain digits, and their lengths are always equal.

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)

	class Solution {
	public:
	    string getHint(string secret, string guess) {
	        int A=0, B=0;
	        vector<int> cnt(10, 0);
	        for (int i=0; i<secret.length(); ++i) {
	            int s = secret[i] - '0';
	            int g = guess[i] - '0';
	            if (s == g)
	                ++A;
	            else {
	                if (cnt[s] < 0)
	                    ++B;
	                if (cnt[g] > 0)
	                    ++B;
	                ++cnt[s];
	                --cnt[g];
	            }
	        }
	        return to_string(A) + "A" + to_string(B) + "B";
	    }
	};

cnt記錄secret及guess中，0~9數字出現的次數。  
其中若出現在secret，則計數+1，若出現在guess，則計數-1。  

若兩數字相同，bull+1。  
若兩數字不同，個別判斷其數字過往的出現情形：
- s需判斷說，其數字是否之前guess有出現過(cnt[s]<0)。
- g需判斷說，其數字是否之前secret有出現過(cnt[g]>0)。

若上述情況成立，cow+1。  
更新cnt現況。  
最後輸出結果。