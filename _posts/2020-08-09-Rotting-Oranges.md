---
layout: post
title:  "[LeetCode August Challange]Day9-Rotting Oranges"
date:   2020-08-09 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
In a given grid, each cell can have one of three values:  

- the value **<font color="red">0</font>** representing an empty cell;
- the value **<font color="red">1</font>** representing a fresh orange;
- the value **<font color="red">2</font>** representing a rotten orange.

Every minute, any fresh orange that is adjacent (4-directionally) to a rotten orange becomes rotten.  

Return the minimum number of minutes that must elapse until no cell has a fresh orange.  If this is impossible, return **<font color="red">-1</font>** instead.

# Example 1:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/rottingOranges.png?raw=true)

	Input: [[2,1,1],[1,1,0],[0,1,1]]
	Output: 4

# Example 2:  
	Input: [[2,1,1],[0,1,1],[1,0,1]]
	Output: -1
	Explanation:  The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.

# Example 3:  
	Input: [[0,2]]
	Output: 0
	Explanation:  Since there are already no fresh oranges at minute 0, the answer is just 0.

# Note:  
- **<font color="red" >1 <= grid.length <= 10</font>**
- **<font color="red" >1 <= grid[0].length <= 10</font>**
- grid[i][j] is only 0, 1, or 2.

______________________  

# solution

Time complexity : O(wh)  
Space complexity : O(wh)  

	class Solution {
	public:
	    int orangesRotting(vector<vector<int>>& grid) {
	        int h = grid.size();
	        int w = grid[0].size();
	        queue<pair<int, int>> rotten_pos;
	        int freshCnt = 0;
	        unordered_map<int, pair<int, int>> direction = {
	            {0, {1, 0}},    // (x, y+1) down
	            {1, {0, 1}},    // (x+1, y) right
	            {2, {-1, 0}},   // (x, y-1) up
	            {3, {0, -1}}    // (x-1, y) left
	        };
	        
	        // observation of input state.
	        for (int y=0; y<h; ++y) {
	            for (int x=0; x<w; ++x) {
	                switch (grid[y][x]) {
	                    case 1:
	                        ++freshCnt;
	                        break;
	                    case 2:
	                        rotten_pos.emplace(y, x);
	                        break;
	                }
	            }
	        }
	        
	        // rotten process
	        int min = 0;
	        while(!rotten_pos.empty() && freshCnt) {
	            // one min rotten volume
	            int size = rotten_pos.size();
	            while(size--) {
	                // for each rotten orange
	                pair<int, int> curPos = rotten_pos.front();
	                rotten_pos.pop();
	                for (int i=0; i<4; ++i) {
	                    // 4 direction process
	                    int target_x = curPos.second + direction[i].second;
	                    int target_y = curPos.first + direction[i].first;
	                    if (target_x < 0 || target_x >= w ||
	                        target_y < 0 || target_y >= h ||
	                        grid[target_y][target_x] != 1) continue;
	                    // rot
	                    grid[target_y][target_x] = 2;
	                    --freshCnt;
	                    rotten_pos.emplace(target_y, target_x);
	                }
	            }
	            
	            ++min;
	        }
	        
	        return freshCnt ? -1 : min;
	    }
	};

首先記錄題目輸入的狀態，包含「多少個fresh」、「哪些位置rotten」。  
利用queue，記錄該min要rot的所有pos。  
個別對每個要rot的pos做處理，往上下左右四個方向rot，若目標位置超出範圍或是該位置不是fresh，則跳過。反之則rot它，並加入queue中。  
最後該處理的都處理完了，判斷是否還存有fresh，返回答案。