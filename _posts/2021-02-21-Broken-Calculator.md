---
layout: post
title: "[LeetCode February Challange] Day 21 - Broken Calculator"
date: 2021-02-21 00:00:00 +0800
categories: LeetCode
tags: [Medium, Math, Greedy, Nutanix, Bloomberg, C++]
---
On a broken calculator that has a number showing on its display, we can perform two operations:

- **Double**: Multiply the number on the display by 2, or;
- **Decrement**: Subtract 1 from the number on the display.

Initially, the calculator is displaying the number <font color="red">X</font>.

Return the minimum number of operations needed to display the number <font color="red">Y</font>.

# Example 1:

	Input: X = 2, Y = 3
	Output: 2
	Explanation: Use double operation and then decrement operation {2 -> 4 -> 3}.

# Example 2:

	Input: X = 5, Y = 8
	Output: 2
	Explanation: Use decrement and then double {5 -> 4 -> 8}.

# Example 3:

	Input: X = 3, Y = 10
	Output: 3
	Explanation:  Use double, decrement and double {3 -> 6 -> 5 -> 10}.

# Example 4:

	Input: X = 1024, Y = 1
	Output: 1023
	Explanation: Use decrement operations 1023 times.

# Note:

1. <font color="red">1 <= X <= 10^9</font>
2. <font color="red">1 <= Y <= 10^9</font>

______________________  

# Solution  

Time complexity : O(logY)  
Space complexity : O(1)  

	class Solution {
	public:
	    int brokenCalc(int X, int Y) {
	        int ans = 0;
	        while (X < Y) {
	            Y = Y % 2 ? Y + 1 : Y / 2;
	            ++ans;
	        }
	        return ans + (X - Y);
	    }
	};

X 至 Y 沒什麼線索可以思考，由 Y 至 X 的話…  
- 若 Y 是奇數的話，一定是 某階段的 X - 1 來的。
- 若 Y 是偶數的話，一定是 某階段的 X \* 2 來的。

若 Y < X，X 只能一直 -1 直到 Y。