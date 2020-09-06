---
layout: post
title:  "[LeetCode September Challange]Day6-Image Overlap"
date:   2020-09-06 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Two images **<font color="red">A</font>** and **<font color="red">B</font>** are given, represented as binary, square matrices of the same size.  (A binary matrix has only 0s and 1s as values.)  

We translate one image however we choose (sliding it left, right, up, or down any number of units), and place it on top of the other image.  After, the *overlap* of this translation is the number of positions that have a 1 in both images.  

(Note also that a translation does **not** include any kind of rotation.)  

What is the largest possible overlap?  

# Example 1:  
	Input: A = [[1,1,0],
	            [0,1,0],
	            [0,1,0]]
	       B = [[0,0,0],
	            [0,1,1],
	            [0,0,1]]
	Output: 3
	Explanation: We slide A to right by 1 unit and down by 1 unit.

# Notes:   
1. **<font color="red">1 <= A.length = A[0].length = B.length = B[0].length <= 30</font>**
2. **<font color="red">0 <= A[i][j], B[i][j] <= 1</font>**

______________________  

# Solution

Time complexity : O(n^4)  
Space complexity : O(1)

	class Solution {
	public:
	    int largestOverlap(vector<vector<int>>& A, vector<vector<int>>& B) {
	        int res = 0;
	        for (int yShift=0; yShift<A.size(); ++yShift) {
	            for (int xShift=0; xShift<A[0].size(); ++xShift) {
	                res = max(res, shiftCount(xShift, yShift, A, B));
	                res = max(res, shiftCount(xShift, yShift, B, A));
	            }
	        }
	        return res;
	    }
	private:
	    int shiftCount(int xShift, int yShift, vector<vector<int>>& A, vector<vector<int>>& B) {
	        int res = 0;
	        for (int y=yShift; y<A.size(); ++y) {
	            for (int x=xShift; x<A[0].size(); ++x) {
	                if (A[y][x] & B[y-yShift][x-xShift]) ++res;
	            }
	        }
	        return res;
	    }
	};

暴力法，將位移後的圖，疊到另一張上面，兩兩bit互and，若都是1，則代表重疊。  
因位移後是補0，所以位移多出來的位置就可以不用看。  