---
layout: post
title:  "[LeetCode July Challange]Day14-Angle Between Hands of a Clock"
date:   2020-07-14 00:00:00 +0800
categories: LeetCode
tags: [Math, C++]
---
Given two numbers, **hour** and **minutes**. Return the smaller angle (in degrees) formed between the **hour** and the **minute** hand.

# Example 1:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/clock1230.png?raw=true)

	Input: hour = 12, minutes = 30
	Output: 165

# Example 2:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/clock0330.png?raw=true)

	Input: hour = 3, minutes = 30
	Output: 75

# Example 3:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/clock0315.png?raw=true)

	Input: hour = 3, minutes = 15
	Output: 7.5

# Example 4:  
	Input: hour = 4, minutes = 50
	Output: 155

# Example 5:  
	Input: hour = 12, minutes = 0
	Output: 0

# Constraints:  
- **1 <= hour <= 12**
- **0 <= minutes <= 59**
- Answers within **10^-5** of the actual value will be accepted as correct.

______________________  

# solution
time complexity : O(1)  
space complexity : O(1)  

	class Solution {
	public:
	    double angleClock(int hour, int minutes) {
	        // total angle = units * angle per unit
	        double minAngle = minutes * 360/60;
	        double hourAngle = (hour+minutes/60.0) * 360/12;
	        
	        double res = abs(minAngle-hourAngle);
	        return min(res, 360-res);
	    }
	};

計算每一分鐘，分針走的角度。  
計算每一分鐘、小時，時針走的角度。  
有了每單位走的角度，就可用總量來算出角度。  
相減即是夾角。  
因算出來的角度有可能會是大角，所以與小角取最小值。