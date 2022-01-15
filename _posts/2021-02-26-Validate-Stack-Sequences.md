---
layout: post
title: "[LeetCode February Challange] Day 26 - Validate Stack Sequences"
date: 2021-02-26 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Stack, Simulation, Google, C++]
---
Given two sequences <font color="red">pushed</font> and <font color="red">popped</font> **with distinct values**, return <font color="red">true</font> if and only if this could have been the result of a sequence of push and pop operations on an initially empty stack.

# Example 1:

	Input: pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
	Output: true
	Explanation: We might do the following sequence:
	push(1), push(2), push(3), push(4), pop() -> 4,
	push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1

# Example 2:

	Input: pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
	Output: false
	Explanation: 1 cannot be popped before 2.

# Constraints:

- <font color="red">0 <= pushed.length == popped.length <= 1000</font>
- <font color="red">0 <= pushed[i], popped[i] < 1000</font>
- **<font color="red">pushed</font>** is a permutation of <font color="red">popped</font>.
- **<font color="red">pushed</font>** and <font color="red">popped</font> have distinct values.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
	        stack<int> stk;
	        int pop_idx = 0;
	        for (int x: pushed) {
	            stk.push(x);
	            while (!stk.empty() && stk.top() == popped[pop_idx]) {
	                ++pop_idx;
	                stk.pop();
	            }
	        }
	        return stk.empty();
	    }
	};

模擬依序 push，若可 pop 則 pop。  
最後檢查該 stack 是否全被 pop 掉，是的話表示該 pop 順序是合理的。