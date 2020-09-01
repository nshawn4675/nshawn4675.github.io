---
layout: post
title:  "[LeetCode September Challange]Day1-Largest Time for Given Digits"
date:   2020-09-01 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given an array of 4 digits, return the largest 24 hour time that can be made.  

The smallest 24 hour time is 00:00, and the largest is 23:59.  Starting from 00:00, a time is larger if more time has elapsed since midnight.  

Return the answer as a string of length 5.  If no valid time can be made, return an empty string.  

# Example 1:  
	Input: [1,2,3,4]
	Output: "23:41"

# Example 2:  
	Input: [5,5,5,5]
	Output: ""

# Note: 
1. **<font color="red">A.length == 4</font>**
2. **<font color="red">0 <= A[i] <= 9</font>**

______________________  

# Solution

Time complexity : O(1)  
Space complexity : O(1)

	class Solution {
	public:
	    string largestTimeFromDigits(vector<int>& A) {
	        int total_min = INT_MIN;
	        
	        sort(A.begin(), A.end());
	        do {
	            total_min = max(total_min, cal_total_min(A));
	        } while (next_permutation(A.begin(), A.end()));
	        
	        string res = "";
	        if (total_min != INT_MIN) {
	            string str_min = to_string(total_min%60);
	            if (str_min.length() < 2) str_min = "0" + str_min;
	            string str_hour = to_string(total_min/60);
	            if (str_hour.length() < 2) str_hour = "0" + str_hour;
	            res = str_hour + ":" + str_min;
	        }
	        
	        return res;
	    }
	private:
	    bool is_valid_time(vector<int> vec) {
	        if (vec[0]>2 ||
	            vec[0]==2 && vec[1]>3 ||
	            vec[2]>5) {
	            return false;
	        } else return true;
	    }
	    
	    int cal_total_min(vector<int> vec) {
	        if (!is_valid_time(vec)) return INT_MIN;
	        return (vec[0]*10+vec[1])*60+(vec[2]*10+vec[3]);
	    }
	};

思路很簡單，所有排列組合、合法的時間中，取最大者。  
有些麻煩的是要做時間合法性判斷、計算總時間量、還有字串處理。  