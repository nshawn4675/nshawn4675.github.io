---
layout: post
title:  "[LeetCode October Challange] Day 26 - Champagne Tower"
date:   2020-10-26 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Google]
---
We stack glasses in a pyramid, where the **first** row has <font color="red">1</font> glass, the **second** row has <font color="red">2</font> glasses, and so on until the 100-th row.  Each glass holds one cup of champagne.  

Then, some champagne is poured into the first glass at the top.  When the topmost glass is full, any excess liquid poured will fall equally to the glass immediately to the left and right of it.  When those glasses become full, any excess champagne will fall equally to the left and right of those glasses, and so on.  (A glass at the bottom row has its excess champagne fall on the floor.)  

For example, after one cup of champagne is poured, the top most glass is full.  After two cups of champagne are poured, the two glasses on the second row are half full.  After three cups of champagne are poured, those two cups become full - there are 3 full glasses total now.  After four cups of champagne are poured, the third row has the middle glass half full, and the two outside glasses are a quarter full, as pictured below.  

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/799_fig.png?raw=true)

Now after pouring some non-negative integer cups of champagne, return how full the <font color="red">j-th</font> glasses, glass in the <font color="red">i-th</font> row is (both <font color="red">i</font> and <font color="red">j</font> are 0-indexed.)  

# Example 1:  
	Input: poured = 1, query_row = 1, query_glass = 1
	Output: 0.00000
	Explanation: We poured 1 cup of champange to the top glass of the tower (which is indexed as (0, 0)). There will be no excess liquid so all the glasses under the top glass will remain empty.

# Example 2:  
	Input: poured = 2, query_row = 1, query_glass = 1
	Output: 0.50000
	Explanation: We poured 2 cups of champange to the top glass of the tower (which is indexed as (0, 0)). There is one cup of excess liquid. The glass indexed as (1, 0) and the glass indexed as (1, 1) will share the excess liquid equally, and each will get half cup of champange.

# Example 3:  
	Input: poured = 100000009, query_row = 33, query_glass = 17
	Output: 1.00000

# Constraints:  
- <font color="red">0 <= poured <= 10^9</font>
- <font color="red">0 <= query_glass <= query_row < 100</font>

______________________  

# Solution  

Time complexity : O(100\*100)  
Space complexity : O(100\*100)  

	class Solution {
	public:
	    double champagneTower(int poured, int query_row, int query_glass) {
	        const int MAX_NUM = 100;
	        double glasses[MAX_NUM][MAX_NUM] = {0};
	        glasses[0][0] = poured;
	        for (int row=0; row<MAX_NUM-1; ++row) {
	            for (int idx=0; idx<=row; ++idx) {
	                if (glasses[row][idx] > 1) {
	                    double overflow = max(0.0, (glasses[row][idx]-1)/2.0);
	                    glasses[row+1][idx] += overflow;
	                    glasses[row+1][idx+1] += overflow;
	                    glasses[row][idx] = 1;
	                }
	            }
	        }
	        return glasses[query_row][query_glass];
	    }
	};

由上而下，模擬滿出分配的方式進行。  