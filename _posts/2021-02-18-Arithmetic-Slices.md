---
layout: post
title: "[LeetCode February Challange] Day 18 - Arithmetic Slices"
date: 2021-02-18 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Dynamic Programming, Amazon, C++]
---
A sequence of numbers is called arithmetic if it consists of at least three elements and if the difference between any two consecutive elements is the same.

For example, these are arithmetic sequences:

	1, 3, 5, 7, 9
	7, 7, 7, 7
	3, -1, -5, -9

The following sequence is not arithmetic.

	1, 1, 2, 5, 7
 
A zero-indexed array A consisting of N numbers is given. A slice of that array is any pair of integers (P, Q) such that 0 <= P < Q < N.  

A slice (P, Q) of the array A is called arithmetic if the sequence:  
A[P], A[P + 1], ..., A[Q - 1], A[Q] is arithmetic. In particular, this means that P + 1 < Q.  

The function should return the number of arithmetic slices in the array A.  

# Example:

	A = [1, 2, 3, 4]

	return: 3, for 3 arithmetic slices in A: [1, 2, 3], [2, 3, 4] and [1, 2, 3, 4] itself.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    int numberOfArithmeticSlices(vector<int>& A) {
	        const int n = A.size();
	        int ans = 0;
	        if (n < 2) return ans;
	        
	        vector<int> bp(n, 0);
	        for (int i=2; i<A.size(); ++i) {
	            if (A[i]-A[i-1] == A[i-1] - A[i-2]) {
	                bp[i] = 1 + bp[i-1];
	                ans += bp[i];
	            }
	        }
	        
	        return ans;
	    }
	};