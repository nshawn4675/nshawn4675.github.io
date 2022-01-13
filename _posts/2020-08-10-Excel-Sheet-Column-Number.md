---
layout: post
title:  "[LeetCode August Challange]Day10-Excel Sheet Column Number"
date:   2020-08-10 00:00:00 +0800
categories: LeetCode
tags: [Math, String, C++]
---
Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:  

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...

# Example 1:  
	Input: "A"
	Output: 1

# Example 2:  
	Input: "AB"
	Output: 28

# Example 3:  
	Input: "ZY"
	Output: 701

# Constraints:  
- 1 <= s.length <= 7
- s consists only of uppercase English letters.
- s is between "A" and "FXSHRXW".

______________________  

# solution

Time complexity : O(n)  
Space complexity : O(1)  

	class Solution {
	public:
	    int titleToNumber(string s) {
	        unsigned int res = 0;
	        for (int i=0; i<s.length(); ++i) {
	            unsigned int base = pow(26, i);
	            unsigned int num = calNum(*(rbegin(s)+i));
	            res += base*num;
	        }
	        return res;
	    }
	private:
	    unsigned int calNum(char c) {
	        return c-'A'+1;
	    }
	};

從s的頭←尾處理，對於每一個字母：  
1. 計算目前的位數次方，26^i。
2. 計算該字母對應的數值。
3. 以上兩者相乘後加入結果。