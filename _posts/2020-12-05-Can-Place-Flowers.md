---
layout: post
title: "[LeetCode December Challange] Day 5 - Can Place Flowers"
date: 2020-12-05 00:00:00 +0800
categories: LeetCode
tags: [Easy, Array, Greedy, Facebook, LinkedIn, C++]
---

You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in **adjacent** plots.

Given an integer array <font color="red">flowerbed</font> containing <font color="red">0</font>'s and <font color="red">1</font>'s, where <font color="red">0</font> means empty and <font color="red">1</font> means not empty, and an integer <font color="red">n</font>, return if <font color="red">n</font> new flowers can be planted in the <font color="red">flowerbed</font> without violating the no-adjacent-flowers rule.

# Example 1:

    Input: flowerbed = [1,0,0,0,1], n = 1
    Output: true

# Example 2:

    Input: flowerbed = [1,0,0,0,1], n = 2
    Output: false

# Constraints:

- <font color="red">1 <= flowerbed.length <= 2 \* 10^4</font>
- **<font color="red">flowerbed[i]</font>** is <font color="red">0</font> or <font color="red">1</font>.
- There are no two adjacent flowers in <font color="red">flowerbed</font>.
- <font color="red">0 <= n <= flowerbed.length</font>

---

# Solution

Time complexity : O(n)  
Space complexity : O(1)

    class Solution {
    public:
        bool canPlaceFlowers(vector<int>& flowerbed, int n) {
            int size = flowerbed.size();
            for (int i=0; i<size; ++i) {
                if ((0<i && flowerbed[i-1] == 1) ||
                    (i<size-1 && flowerbed[i+1] == 1) ||
                    flowerbed[i] == 1)
                {
                    continue;
                }
                flowerbed[i] = 1;
                --n;
            }
            return n <= 0;
        }
    };

從左至右，檢查下面幾點，若其一符合，則不種，跳過：

1. 左邊是否有種。
2. 右邊是否有種。
3. 自身是否有種。

其餘情況則種花，需求花數-1。  
最後檢查種植數量是否大於需求花數(即需求為負)。
