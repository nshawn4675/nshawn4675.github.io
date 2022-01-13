---
layout: post
title:  "[LeetCode September Challange]Day9-Compare Version Numbers"
date:   2020-09-09 00:00:00 +0800
categories: LeetCode
tags: [Two Pointers, String, C++]
---
Compare two version numbers *version1* and *version2*.  
If **<font color="red">version1 > version2</font>** return **<font color="red">1</font>**; if **<font color="red">version1 < version2</font>** return **<font color="red">-1</font>**;otherwise return **<font color="red">0</font>**.  

You may assume that the version strings are non-empty and contain only digits and the **<font color="red">.</font>** character.  

The **<font color="red">.</font>** character does not represent a decimal point and is used to separate number sequences.   

For instance, **<font color="red">2.5</font>** is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.  

You may assume the default revision number for each level of a version number to be **<font color="red">0</font>**. For example, version number **<font color="red">3.4</font>** has a revision number of **<font color="red">3</font>** and **<font color="red">4</font>** for its first and second level revision number. Its third and fourth level revision number are both **<font color="red">0</font>**.  

# Example 1:  
	Input: version1 = "0.1", version2 = "1.1"
	Output: -1

# Example 2:  
	Input: version1 = "1.0.1", version2 = "1"
	Output: 1

# Example 3:  
	Input: version1 = "7.5.2.4", version2 = "7.5.3"
	Output: -1

# Example 4:  
	Input: version1 = "1.01", version2 = "1.001"
	Output: 0
	Explanation: Ignoring leading zeroes, both “01” and “001" represent the same number “1”

# Example 5:  
	Input: version1 = "1.0", version2 = "1.0.0"
	Output: 0
	Explanation: The first version number does not have a third level revision number, which means its third level revision number is default to "0"

# Note:  
1. Version strings are composed of numeric strings separated by dots **<font color="red">.</font>** and this numeric strings **may** have leading zeroes.
2. Version strings do not start or end with dots, and they will not be two consecutive dots.

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(n)

	class Solution {
	public:
	    int compareVersion(string version1, string version2) {
	        vector<int> v1 = parseVer(version1);
	        vector<int> v2 = parseVer(version2);
	        
	        int idx = 0;
	        int size1 = v1.size();
	        int size2 = v2.size();
	        while (idx < max(size1, size2)) {
	            int n1 = idx < size1 ? v1[idx] : 0;
	            int n2 = idx < size2 ? v2[idx] : 0;
	            ++idx;
	            if (n1 < n2) return -1;
	            else if (n1 > n2) return 1;
	        }
	        return 0;
	    }
	private:
	    vector<int> parseVer(string& str) {
	        vector<int> res;
	        int sum = 0;
	        for(char c: str) {
	            if (c == '.') {
	                res.push_back(sum);
	                sum = 0;
	            } else {
	                sum = 10*sum + (c-'0');
	            }
	        }
	        res.push_back(sum);
	        return res;
	    }
	};

先個別用vector存放version1、version2，以「.」隔開的版本號。  
再從頭一個一個比較，超過的用0代替，照題目所述輸出。