---
layout: post
title: "[LeetCode December Challange] Day 13 - Burst Balloons"
date: 2020-12-13 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Hard, Divide and Conquer, Dynamic Programming]
---

Given <font color="red">n</font> balloons, indexed from <font color="red">0</font> to <font color="red">n-1</font>. Each balloon is painted with a number on it represented by array <font color="red">nums</font>. You are asked to burst all the balloons. If the you burst balloon <font color="red">i</font> you will get <font color="red">nums[left] * nums[i] * nums[right]</font> coins. Here <font color="red">left</font> and <font color="red">right</font> are adjacent indices of <font color="red">i</font>. After the burst, the <font color="red">left</font> and <font color="red">right</font> then becomes adjacent.

Find the maximum coins you can collect by bursting the balloons wisely.

# Note:

- You may imagine <font color="red">nums[-1] = nums[n] = 1</font>. They are not real therefore you can not burst them.
- 0 ≤ <font color="red">n</font> ≤ 500, 0 ≤ <font color="red">nums[i]</font> ≤ 100

# Example:

    Input: [3,1,5,8]
    Output: 167
    Explanation: nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
                coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167

---

# Solution

Time complexity : O(n^3)  
Space complexity : O(n^2)

    class Solution {
    public:
        int maxCoins(vector<int>& nums) {
            int N = nums.size();
            nums.insert(nums.begin(), 1);
            nums.push_back(1);

            vector<vector<int>> dp(N+2, vector<int>(N+2, 0));
            for (int len=1; len<=N; ++len) {
                for (int i=1; i+len-1<=N; ++i) {
                    int j = i+len-1;
                    for (int k=i; k<=j; ++j) {
                        dp[i][j] = max(dp[i][j], dp[i][k-1]+nums[i-1]*nums[k]*nums[j+1]+dp[k+1][j]);
                    }
                }
            }

            return dp[1][N];
        }
    };

定義 dp[i][j]為範圍 i~j 的氣球，可獲得的最大收益。

k 代表在 i~j 的範圍中，第 k 個氣球為最後引爆的。

故第 k 顆氣球的收益由以下組成：
1. dp[i][k-1] (範圍中，左邊爆光的最大收益)
2. nums[i-1]\*nums[k]\*nums[j+1] (中間k引爆的收益)
3. dp[k+1][j] (範圍中，右邊爆光的最大收益)

範圍長度由最少1個 ~ 最多N個(陣列長度)。

最後的答案為dp[1][N]，即範圍1~N可獲得的最大收益。