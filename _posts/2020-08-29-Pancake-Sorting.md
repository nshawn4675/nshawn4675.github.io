---
layout: post
title:  "[LeetCode August Challange]Day29-Pancake Sorting"
date:   2020-08-29 00:00:00 +0800
categories: LeetCode
tags: [Array, Two Pointers, Greedy, Sorting, C++]
---
Given an array of integers **<font color="red">A</font>**, We need to sort the array performing a series of **pancake flips**.

In one pancake flip we do the following steps:
- Choose an integer **<font color="red">k</font>** where **<font color="red">0 <= k < A.length</font>**.
- Reverse the sub-array **<font color="red">A[0...k]</font>**.
For example, if **<font color="red">A = [3,2,1,4]</font>** and we performed a pancake flip choosing **<font color="red">k = </font>**2</font>**, we reverse the sub-array **<font color="red">[3,2,1], so **<font color="red">A = [1,2,3,4]</font>** after the pancake flip at **<font color="red">k = 2</font>**.

Return an array of the k-values of the pancake flips that should be performed in order to sort **<font color="red">A</font>**. Any valid answer that sorts the array within **<font color="red">10 * A.length</font>** flips will be judged as correct.

# Example 1:  
	Input: A = [3,2,4,1]
	Output: [4,2,4,3]
	Explanation: 
	We perform 4 pancake flips, with k values 4, 2, 4, and 3.
	Starting state: A = [3, 2, 4, 1]
	After 1st flip (k = 4): A = [1, 4, 2, 3]
	After 2nd flip (k = 2): A = [4, 1, 2, 3]
	After 3rd flip (k = 4): A = [3, 2, 1, 4]
	After 4th flip (k = 3): A = [1, 2, 3, 4], which is sorted.
	Notice that we return an array of the chosen k values of the pancake flips.

# Example 2:  
	Input: A = [1,2,3]
	Output: []
	Explanation: The input is already sorted, so there is no need to flip anything.
	Note that other answers, such as [3, 3], would also be accepted.

# Constraints:  
- **<font color="red">1 <= A.length <= 100</font>**
- **<font color="red">1 <= A[i] <= A.length</font>**
- All integers in **<font color="red">A</font>** are unique (i.e. **<font color="red">A</font>** is a permutation of the integers from **<font color="red">1</font>** to **<font color="red">A.length</font>**).

______________________  

# solution

Time complexity : O(n^2)
Space complexity : O(1)

	class Solution {
	public:
	    vector<int> pancakeSort(vector<int>& A) {
	        int n = A.size();
	        vector<int> res = {};
	        for (int i=0; i<n-1; ++i) {
	            int pos = max_element(A.begin(), A.end()-i) - A.begin();
	            res.push_back(pos+1);
	            reverse(A.begin(), A.begin()+(pos+1));
	            res.push_back(n-i);
	            reverse(A.begin(), A.begin()+(n-i));
	        }
	        return res;
	    }
	};

從右至左，數值大至小處理。  
每次處理一個數時，找到最大值，將它移到最左邊，再將它移到最右邊。