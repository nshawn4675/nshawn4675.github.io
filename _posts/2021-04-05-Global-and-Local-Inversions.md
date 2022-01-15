---
layout: post
title: "[LeetCode April Challange] Day 05 - Global and Local Inversions"
date: 2021-04-05 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Math, Bloomberg, C++]
---
We have some permutation <font color="red">A</font> of <font color="red">[0, 1, ..., N - 1]</font>, where <font color="red">N</font> is the length of <font color="red">A</font>.

The number of (global) inversions is the number of <font color="red">i < j</font> with <font color="red">0 <= i < j < N</font> and <font color="red">A[i] > A[j]</font>.

The number of local inversions is the number of <font color="red">i</font> with <font color="red">0 <= i < N</font> and <font color="red">A[i] > A[i+1]</font>.

Return <font color="red">true</font> if and only if the number of global inversions is equal to the number of local inversions.

# Example 1:

    Input: A = [1,0,2]
    Output: true
    Explanation: There is 1 global inversion, and 1 local inversion.

# Example 2:

    Input: A = [1,2,0]
    Output: false
    Explanation: There are 2 global inversions, and 1 local inversion.

# Note:

- **<font color="red">A</font>** will be a permutation of <font color="red">[0, 1, ..., A.length - 1]</font>.
- **<font color="red">A</font>** will have length in range <font color="red">[1, 5000]</font>.
- The time limit for this problem has been reduced.

______________________  

# Solution  

# Brute Force (TLE)

Time complexity : O(n^2)  
Space complexity : O(1)  

    class Solution {
    public:
        bool isIdealPermutation(vector<int>& A) {
            int local = 0, global = 0;
            for (int i=0; i<A.size(); ++i) {
                for (int j=i+1; j<A.size(); ++j) {
                    if (A[i] > A[j])
                        ++global;
                }
            }
            for (int i=1; i<A.size(); ++i) {
                if (A[i-1] > A[i])
                    ++local;
            }
            return local == global;
        }
    };

# Remember Minimun  

Time complexity : O(n)  
Space complexity : O(1)  

    class Solution {
    public:
        bool isIdealPermutation(vector<int>& A) {
            const int N = size(A);
            int minimum = N;
            for (int i=N-1; 2 <= i; --i) {
                minimum = min(A[i], minimum);
                if (A[i-2] > minimum) return false;
            }
            return true;
        }
    };

文字遊戲：local inversion 為 global inversion 的一種。  
題目即是要我們找存不存在非 local inversion。

從右往左掃描，記錄到目前為止的最小值，若 A\[i-2\] \> minimum，則此為 global inversion。

也可以從左往右掃描，記錄最大值，與 A\[i+2\] 比較。


# Linear Scan  

Time complexity : O(n)  
Space complexity : O(1)  

    class Solution {
    public:
        bool isIdealPermutation(vector<int>& A) {
            for (int i=0; i<A.size(); ++i)
                if (2 <= abs(A[i]-i)) return false;
            return true;
        }
    };

在一個沒有 global inversion 的 permutation 中，各個元素的位置會在哪裡？  
若 0 出現在 A\[2\] 以上，則其為 global inversion.  
若 1 沒有出現在 A\[0~2\]，則其為 global inversion.  
...  
即，若該位置的數離開它本該存在的位置距離 2 以上，則為 global inversion.