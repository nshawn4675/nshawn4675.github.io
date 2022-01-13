---
layout: post
title:  "[LeetCode August Challange]Day22-Random Point in Non-overlapping Rectangles"
date:   2020-08-22 00:00:00 +0800
categories: LeetCode
tags: [Math, Binary Search, Reservoir Sampling, Prefix Sum, Ordered Set, Randomized, C++]
---
Given a list of **non-overlapping** axis-aligned rectangles **<font color="red">rects</font>**, write a function **<font color="red">pick</font>** which randomly and uniformily picks an **integer point** in the space covered by the rectangles.  

Note:  
1. An **integer point** is a point that has integer coordinates. 
2. A point on the perimeter of a rectangle is **included** in the space covered by the rectangles. 
3. **<font color="red">i-th</font>** rectangle = **<font color="red">rects[i]</font>** = **<font color="red">[x1,y1,x2,y2]</font>**, where **<font color="red">[x1, y1]</font>** are the integer coordinates of the bottom-left corner, and **<font color="red">[x2, y2]</font>** are the integer coordinates of the top-right corner.
4. length and width of each rectangle does not exceed **<font color="red">2000</font>**.
5. **<font color="red">1 <= rects.length <= 100</font>**
6. **<font color="red">pick</font>** return a point as an array of integer coordinates **<font color="red">[p_x, p_y]</font>**
7. **<font color="red">pick</font>** is called at most **<font color="red">10000</font>** times.  

# Example 1:  
	Input: 
	["Solution","pick","pick","pick"]
	[[[[1,1,5,5]]],[],[],[]]
	Output: 
	[null,[4,1],[4,1],[3,3]]

# Example 2:  
	Input: 
	["Solution","pick","pick","pick","pick","pick"]
	[[[[-2,-2,-1,-1],[1,0,3,0]]],[],[],[],[],[]]
	Output: 
	[null,[-1,-2],[2,0],[-2,-1],[3,0],[-2,-2]]

# Explanation of Input Syntax:  
The input is two lists: the subroutines called and their arguments. **<font color="red">Solution</font>**'s constructor has one argument, the array of rectangles **<font color="red">rects</font>**. **<font color="red">pick</font>** has no arguments. Arguments are always wrapped with a list, even if there aren't any.

______________________  

# solution

	class Solution {
	public:
	    Solution(vector<vector<int>> rects): rects_(move(rects)) {
	    	// Time : O(n) ; Space : O(n)
	        sum_ = vector<int>(rects_.size(), 0);
	        for (int i=0; i<rects_.size(); ++i) {
	            int area = (rects_[i][2]-rects_[i][0]+1) * (rects_[i][3]-rects_[i][1]+1);
	            sum_[i] = 0==i ? area : sum_[i-1] + area;
	        }
	    }
	    
	    vector<int> pick() {
	    	// Time : O(log(n)) ; Space : O(1)
	        int sample = 1 + (rand()%sum_.back());
	        int idx = lower_bound(sum_.begin(), sum_.end(), sample) - sum_.begin();
	        int x = rects_[idx][0] + rand()%(rects_[idx][2]-rects_[idx][0]+1);
	        int y = rects_[idx][1] + rand()%(rects_[idx][3]-rects_[idx][1]+1);
	        return {x, y};
	    }
	private:
	    vector<vector<int>> rects_;
	    vector<int> sum_;
	};

	/**
	 * Your Solution object will be instantiated and called as such:
	 * Solution* obj = new Solution(rects);
	 * vector<int> param_1 = obj->pick();
	 */

依序將rect的面積累加起來，形成**累積分布函數(CDF)**，再利用這個CDF隨機取相對應的rect，再從這個rect中隨機取x、y即可。