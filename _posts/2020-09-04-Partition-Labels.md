---
layout: post
title:  "[LeetCode September Challange]Day4-Partition Labels"
date:   2020-09-04 00:00:00 +0800
categories: LeetCode
tags: [Hash Table, Two Pointers, String, Greedy, C++]
---
A string **<font color="red">S</font>** of lowercase English letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.  

# Example 1:  
	Input: S = "ababcbacadefegdehijhklij"
	Output: [9,7,8]
	Explanation:
	The partition is "ababcbaca", "defegde", "hijhklij".
	This is a partition so that each letter appears in at most one part.
	A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.

# Note:  
- **<font color="red">S</font>** will have length in range **<font color="red">[1, 500]</font>**.
- **<font color="red">S</font>** will consist of lowercase English letters (**<font color="red">'a'</font>** to **<font color="red">'z'</font>**) only.

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)

	class Solution {
	public:
	    vector<int> partitionLabels(string S) {
	        vector<int> last(26, 0);
	        for (int i=0; i<S.length(); ++i)
	            last[S[i]-'a'] = i;
	        
	        vector<int> res;
	        int start = 0, end = 0;
	        for (int i=0; i<S.length(); ++i) {
	            end = max(end, last[S[i]-'a']);
	            if (i == end) {
	                res.push_back(end-start+1);
	                start = i+1;
	            }
	        }
	        return res;
	    }
	};

先記錄下各字母最後的位置，  
再利用start、end，算出各區間的長度。  