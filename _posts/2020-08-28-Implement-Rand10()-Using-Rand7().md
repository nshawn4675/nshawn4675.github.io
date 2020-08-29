---
layout: post
title:  "[LeetCode August Challange]Day28-Implement Rand10() Using Rand7()"
date:   2020-08-28 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given the **API** **<font color="red">rand7</font>** which generates a uniform random integer in the range 1 to 7, write a function **<font color="red">rand10</font>** which generates a uniform random integer in the range 1 to 10. You can only call the API **<font color="red">rand7</font>** and you shouldn't call any other API. Please **don't** use the system's **<font color="red">Math.random()</font>**.  

**Notice that** Each test case has one argument **<font color="red">n</font>**, the number of times that your implemented function **<font color="red">rand10</font>** will be called while testing. 

# Follow up:  
1. What is the [expected value](https://en.wikipedia.org/wiki/Expected_value) for the number of calls to **<font color="red">rand7()</font>** function?
2. Could you minimize the number of calls to **<font color="red">rand7()</font>**?

# Example 1:  
	Input: n = 1
	Output: [2]

# Example 2:  
	Input: n = 2
	Output: [2,8]

# Example 3:  
	Input: n = 3
	Output: [3,8,10]

# Constraints:  
- **<font color="red">1 <= n <= 105</font>**

______________________  

# solution

Time complexity : O(1)
Space complexity : O(1)

	// The rand7() API is already defined for you.
	// int rand7();
	// @return a random integer in the range 1 to 7

	class Solution {
	public:
	    int rand10() {
	        int idx = INT_MAX;
	        while (idx >= 40)
	            idx = (rand7()-1)*7 + (rand7()-1);
	        return idx%10+1;
	    }
	};

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/rand7.png?raw=true)  

共有四個完整0~9的分佈，使用 (a-1)\*7 + (b-1) 作為索引值來sample，  
若不幸取到40~48，就再sample一次。