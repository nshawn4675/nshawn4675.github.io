---
layout: post
title: "[LeetCode April Challange] Day 06 - Minimum Operations to Make Array Equal"
date: 2021-04-06 00:00:00 +0800
categories: LeetCode
tags: [Medium, Math, Brillio, C++]
---
You have an array <font color="red">arr</font> of length <font color="red">n</font> where <font color="red">arr[i] = (2 * i) + 1</font> for all valid values of <font color="red">i</font> (i.e. <font color="red">0 <= i < n</font>).

In one operation, you can select two indices <font color="red">x</font> and <font color="red">y</font> where <font color="red">0 <= x, y < n</font> and subtract <font color="red">1</font> from <font color="red">arr[x]</font> and add <font color="red">1</font> to <font color="red">arr[y]</font> (i.e. perform <font color="red">arr[x] -=1</font> and <font color="red">arr[y] += 1</font>). The goal is to make all the elements of the array **equal**. It is **guaranteed** that all the elements of the array can be made equal using some operations.

Given an integer <font color="red">n</font>, the length of the array. Return *the minimum number of operations* needed to make all the elements of arr equal.

# Example 1:

    Input: n = 3
    Output: 2
    Explanation: arr = [1, 3, 5]
    First operation choose x = 2 and y = 0, this leads arr to be [2, 3, 4]
    In the second operation choose x = 2 and y = 0 again, thus arr = [3, 3, 3].

# Example 2:

    Input: n = 6
    Output: 9

# Constraints:

- <font color="red">1 <= n <= 10^4</font>

______________________  

# Solution  

Time complexity : O(1)  
Space complexity : O(1)  

    class Solution {
    public:
        int minOperations(int n) {
            return n*n/4;
        }
    };

target = sum([1, 3, 5, ..., 2n-1]/n) = \[(1+(2n-1))\*n/2\]/n = n  
可以用平衡的加減法當作一個動作，  
例：1, 3, 5, 7, target = n = 4  
則 1加1(7減1) 做 3 次，3加1(5減1) 做 1 次，即可達到平衡。

因此所需的動作次數，為 (4-1)+(4-3) = 4。  

一般化則為 (n-1)+(n-3)+...+1(or0)。

再利用等差級數和公式可得：1+3+...+(n-1) = (1+(n-1)) * n/2 / 2 = n^2 / 4;