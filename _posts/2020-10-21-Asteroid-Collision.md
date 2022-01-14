---
layout: post
title:  "[LeetCode October Challange] Day 21 - Asteroid Collision"
date:   2020-10-21 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Stack, Amazon, Lyft, ByteDance, Google, C++]
---
We are given an array <font color="red">asteroids</font> of integers representing asteroids in a row.  

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.  

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.  

# Example 1:  
	Input: asteroids = [5,10,-5]
	Output: [5,10]
	Explanation: The 10 and -5 collide resulting in 10.  The 5 and 10 never collide.

# Example 2:  
	Input: asteroids = [8,-8]
	Output: []
	Explanation: The 8 and -8 collide exploding each other.

# Example 3:  
	Input: asteroids = [10,2,-5]
	Output: [10]
	Explanation: The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.

# Example 4:  
	Input: asteroids = [-2,-1,1,2]
	Output: [-2,-1,1,2]
	Explanation: The -2 and -1 are moving left, while the 1 and 2 are moving right. Asteroids moving the same direction never meet, so no asteroids will meet each other.

# Constraints:  
- <font color="red">1 <= asteroids <= 10^4</font>
- <font color="red">-1000 <= asteroids[i] <= 1000</font>
- <font color="red">asteroids[i] != 0</font>

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    vector<int> asteroidCollision(vector<int>& asteroids) {
	        vector<int> ans = {};
	        for (int i=0; i<asteroids.size(); ++i) {
	            int incoming = asteroids[i];
	            if (0 < incoming || ans.empty() || ans.back() < 0)
	                ans.push_back(incoming);
	            else if (abs(ans.back()) <= abs(incoming)) {
	                if (abs(ans.back()) < abs(incoming)) --i;
	                ans.pop_back();
	            }
	        }
	        return ans;
	    }
	};

這題輸出的性質：[-, ... , -, +, ... , +]，左部份會是往左飛，右部份會是往右飛。  

每有新的挑戰者出現時，符合下面條件其一，不會有碰撞，可直接塞入：  
1. 新的挑戰者向右飛。
2. 目前都沒有其它星球。
3. 目前的最後一個是向左飛。

不符合以上情況者，都是會碰撞的，即目前最後一個往右飛，新的挑戰者往左飛。  

若目前最後一個的size比新的挑戰者大，則新的挑戰者會爆炸。即不做任何處理，新的迴圈指向下一個新一挑戰者。  

若目前最後一個的size比新的挑戰者小，則新的挑戰者存活，舊的爆炸。即i=i-1，因為迴圈結束後會++i，為了保持處理目前新的挑戰者才做i=i-1。  

若目前最後一個的size與新的挑戰者相等，則兩者爆炸。即只pop目前最後一者，下一個迴圈時會指到下一個新的挑戰者。  

最後回傳結果。  