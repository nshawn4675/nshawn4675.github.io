---
layout: post
title:  "[LeetCode July Challange]Day3-Prison Cells After N Days"
date:   2020-07-03 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
There are 8 prison cells in a row, and each cell is either occupied or vacant.  

Each day, whether the cell is occupied or vacant changes according to the following rules:  

- If a cell has two adjacent neighbors that are both occupied or both vacant, then the cell becomes occupied.  
- Otherwise, it becomes vacant.  
(Note that because the prison is a row, the first and the last cells in the row can't have two adjacent neighbors.)  

We describe the current state of the prison in the following way: **cells[i] == 1** if the **i**-th cell is occupied, else **cells[i] == 0**.  

Given the initial state of the prison, return the state of the prison after **N** days (and **N** such changes described above.)  

# Example 1:  

	Input: cells = [0,1,0,1,1,0,0,1], N = 7  
	Output: [0,0,1,1,0,0,0,0]  
	Explanation:  
	The following table summarizes the state of the prison on each day:  
	Day 0: [0, 1, 0, 1, 1, 0, 0, 1]  
	Day 1: [0, 1, 1, 0, 0, 0, 0, 0]  
	Day 2: [0, 0, 0, 0, 1, 1, 1, 0]  
	Day 3: [0, 1, 1, 0, 0, 1, 0, 0]  
	Day 4: [0, 0, 0, 0, 0, 1, 0, 0]  
	Day 5: [0, 1, 1, 1, 0, 1, 0, 0]  
	Day 6: [0, 0, 1, 0, 1, 1, 0, 0]  
	Day 7: [0, 0, 1, 1, 0, 0, 0, 0]  

# Example 2: 

	Input: cells = [1,0,0,1,0,0,1,0], N = 1000000000  
	Output: [0,0,1,1,1,1,1,0]  

______________________  
# solution
time complexity : O(mn)  
space complexity : O(n)  
(m:days, n:#cells)  

	class Solution {
	public:
	    vector<int> prisonAfterNDays(vector<int>& cells, int N) {
	        int size = cells.size();
	        vector<int> next_cells(size, 0), first_cycle_cells;
	        
	        for (int cycle=0; N-->0; cells = next_cells, ++cycle) {
	            for (int i=1; i<size-1; ++i)
	                next_cells[i] = cells[i-1] == cells[i+1];
	            
	            if (cycle == 0)
	                first_cycle_cells = next_cells;
	            else if (next_cells == first_cycle_cells)
	                N %= cycle;
	        }
	        
	        return cells;
	    }
	};

此題可用brute-force，但天數N太大會使得執行時間過長，導致Time Limit Exceeded，因此得想方法減少執行時間。  
因具有固定的變化，故可猜想應有某一cycle，又因最左、最右元素第一天變化後一定為0(但初始未知)，因此變化的cycle是從第一天變化後開始計算，往後執行若遇到與cycle一開始相同的pattern，就將剩餘的天數N與cycle取餘數，執行不滿cycle的剩餘天數即可，中間重覆的cycle只會得到一樣的結果，造成多餘的執行時間，故直接跳過。