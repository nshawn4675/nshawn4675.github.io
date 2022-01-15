---
layout: post
title: "[LeetCode February Challange] Day 12 - Number of Steps to Reduce a Number to Zero"
date: 2021-02-12 00:00:00 +0800
categories: LeetCode
tags: [Easy, Math, Bit Manipulation, Amazon, Google, Microsoft, C++]
---
Given a non-negative integer <font color="red">num</font>, return the number of steps to reduce it to zero. If the current number is even, you have to divide it by 2, otherwise, you have to subtract 1 from it.

# Example 1:

	Input: num = 14
	Output: 6
	Explanation: 
	Step 1) 14 is even; divide by 2 and obtain 7. 
	Step 2) 7 is odd; subtract 1 and obtain 6.
	Step 3) 6 is even; divide by 2 and obtain 3. 
	Step 4) 3 is odd; subtract 1 and obtain 2. 
	Step 5) 2 is even; divide by 2 and obtain 1. 
	Step 6) 1 is odd; subtract 1 and obtain 0.

# Example 2:

	Input: num = 8
	Output: 4
	Explanation: 
	Step 1) 8 is even; divide by 2 and obtain 4. 
	Step 2) 4 is even; divide by 2 and obtain 2. 
	Step 3) 2 is even; divide by 2 and obtain 1. 
	Step 4) 1 is odd; subtract 1 and obtain 0.

# Example 3:

	Input: num = 123
	Output: 12

# Constraints:

- <font color="red">0 <= num <= 10^6</font>

______________________  

# Solution  

### Simulation

Time complexity : O(nlong)  
Space complexity : O(1)  

	class Solution {
	public:
	    int numberOfSteps (int num) {
	        int ans = 0;
	        while (0 < num) {
	            ++ans;
	            num = num % 2 ? num-1 : num / 2;
	        }
	        return ans;
	    }
	};


### Bit Manipulation

Time complexity : O(nlong)  
Space complexity : O(1)  

	class Solution {
	public:
	    int numberOfSteps (int num) {
	        string b_str = "";
	        while (0 < num) {
	            b_str = to_string(num%2) + b_str;
	            num /= 2;
	        }
	        printf("%s", b_str.c_str());
	        
	        int ans = 0;
	        for (char c: b_str) {
	            if (c == '1') ans += 2;
	            else ans += 1;
	        }
	        return max(0, ans-1);
	    }
	};

將一 int 轉為 binary string，一一將位元消掉。

若最小位元為 "1"，則需要「減1」、「右移(除2)」，需 2 步。  
若最小位元為 "0", 則需要「右移(除2)」，需 1 步。  

最後的答案需少一步的原因是：最後一個 "1" 只需要1步就到 0，而非 2 步。