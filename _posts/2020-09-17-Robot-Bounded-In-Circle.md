---
layout: post
title:  "[LeetCode September Challange]Day17-Robot Bounded In Circle"
date:   2020-09-17 00:00:00 +0800
categories: LeetCode
tags: [Medium, Math, String, Simulation, C++]
---
On an infinite plane, a robot initially stands at **<font color="red">(0, 0)</font>** and faces north.  The robot can receive one of three instructions:  

- **<font color="red">"G"</font>** : go straight 1 unit.  
- **<font color="red">"L"</font>** : turn 90 degrees to the left.  
- **<font color="red">"R"</font>** : turn 90 degress to the right.  

The robot performs the **<font color="red">instructions</font>** given in order, and repeats them forever.  

Return **<font color="red">true</font>** if and only if there exists a circle in the plane such that the robot never leaves the circle.  

# Example 1:  
	Input: "GGLLGG"
	Output: true
	Explanation: 
	The robot moves from (0,0) to (0,2), turns 180 degrees, and then returns to (0,0).
	When repeating these instructions, the robot remains in the circle of radius 2 centered at the origin.

# Example 2:  
	Input: "GG"
	Output: false
	Explanation: 
	The robot moves north indefinitely.

# Example 3:  
	Input: "GL"
	Output: true
	Explanation: 
	The robot moves from (0, 0) -> (0, 1) -> (-1, 1) -> (-1, 0) -> (0, 0) -> ...

# Note:  
1. **<font color="red">1 <= instructions.length <= 100</font>**
2. **<font color="red">instructions[i]</font>** is in **<font color="red">{'G', 'L', 'R'}</font>**

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(1)

	class Solution {
	public:
	    bool isRobotBounded(string instructions) {
	        int x = 0, y = 0, direction = 0;
	        vector<int> dx = {0, 1, 0, -1};
	        vector<int> dy = {1, 0, -1, 0};
	        for (char c: instructions) {
	            if (c == 'G') {
	                x += dx[direction];
	                y += dy[direction];
	            } else
	                direction = (direction + (c == 'L' ? 3 : 1)) % 4;
	        }
	        return (x==0 && y==0) || direction;
	    }
	};

根據數學推導，以這上下左右四個方位來說，跑四次，若是cycle，x、y座標會回到(0, 0)。  

但不用跑到4次，1次即可，也是根據數學推導，跑1次判斷是否為cycle的條件：  
1. x、 y座標會回到(0, 0)。
2. 非面向北方。

若跑一次之後位置不在(0, 0)，且面向北方(即初始狀態)，代表再跑下一輪，同樣的事情會發生，且離(0, 0)更遠，永遠回不了(0, 0)。