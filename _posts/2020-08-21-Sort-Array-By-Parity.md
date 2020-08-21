---
layout: post
title:  "[LeetCode August Challange]Day21-Sort Array By Parity"
date:   2020-08-21 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given an array **<font color="red">A</font>** of non-negative integers, return an array consisting of all the even elements of **<font color="red">A</font>**, followed by all the odd elements of **<font color="red">A</font>**.  

You may return any answer array that satisfies this condition.  

# Example 1:  
	Input: [3,1,2,4]
	Output: [2,4,3,1]
	The outputs [4,2,3,1], [2,4,1,3], and [4,2,1,3] would also be accepted.

# Note:  
1. **<font color="red">1 <= A.length <= 5000</font>**
2. **<font color="red">0 <= A[i] <= 5000</font>**

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)

	class Solution {
	public:
	    vector<int> sortArrayByParity(vector<int>& A) {
	        for (int i=0, j=A.size()-1; i<j; ) {
	            while (0==(A[i]&1) && i<j) ++i;
	            while (1==(A[j]&1) && i<j) --j;
	            swap(A[i++], A[j--]);
	        }
	        return A;
	    }
	};

使用2-pointer的方式，從頭找到奇數，從尾找到偶數，兩者交換。