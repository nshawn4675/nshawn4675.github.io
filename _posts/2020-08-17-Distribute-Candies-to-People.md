---
layout: post
title:  "[LeetCode August Challange]Day17-Distribute Candies to People"
date:   2020-08-17 00:00:00 +0800
categories: LeetCode
tags: [Math, Simulation, C++]
---
We distribute some number of **<font color="red">candies</font>**, to a row of **<font color="red">n = num_people</font>** people in the following way:  

We then give 1 candy to the first person, 2 candies to the second person, and so on until we give **<font color="red">n</font>** candies to the last person.  

Then, we go back to the start of the row, giving **<font color="red">n + 1</font>** candies to the first person, **<font color="red">n + 2</font>** candies to the second person, and so on until we give **<font color="red">2 * n</font>** candies to the last person.  

This process repeats (with us giving one more candy each time, and moving to the start of the row after we reach the end) until we run out of candies.  The last person will receive all of our remaining candies (not necessarily one more than the previous gift).  

Return an array (of length **<font color="red">num_people</font>** and sum **<font color="red">candies</font>**) that represents the final distribution of candies.  

# Example 1:  
	Input: candies = 7, num_people = 4
	Output: [1,2,3,1]
	Explanation:
	On the first turn, ans[0] += 1, and the array is [1,0,0,0].
	On the second turn, ans[1] += 2, and the array is [1,2,0,0].
	On the third turn, ans[2] += 3, and the array is [1,2,3,0].
	On the fourth turn, ans[3] += 1 (because there is only one candy left), and the final array is [1,2,3,1].

# Example 2:  
	Input: candies = 10, num_people = 3
	Output: [5,2,3]
	Explanation: 
	On the first turn, ans[0] += 1, and the array is [1,0,0].
	On the second turn, ans[1] += 2, and the array is [1,2,0].
	On the third turn, ans[2] += 3, and the array is [1,2,3].
	On the fourth turn, ans[0] += 4, and the final array is [5,2,3].

# Constraints:  
- 1 <= candies <= 10^9
- 1 <= num_people <= 1000

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(n)

	class Solution {
	public:
	    vector<int> distributeCandies(int candies, int num_people) {
	        vector<int> res(num_people, 0);
	        
	        for (int cnt=1; 0<candies; candies-=cnt, ++cnt) {
	            res[(cnt-1)%num_people] += min(cnt, candies);
	        }
	            
	        return res;
	    }
	};