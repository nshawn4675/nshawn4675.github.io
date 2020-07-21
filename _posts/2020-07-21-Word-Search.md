---
layout: post
title:  "[LeetCode July Challange]Day21-Word Search"
date:   2020-07-21 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Given a 2D board and a word, find if the word exists in the grid.  

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.  

# Example:  
	board =
	[
	  ['A','B','C','E'],
	  ['S','F','C','S'],
	  ['A','D','E','E']
	]

	Given word = "ABCCED", return true.
	Given word = "SEE", return true.
	Given word = "ABCB", return false.

# Constraints:  
- **board** and **word** consists only of lowercase and uppercase English letters.
- **1 <= board.length <= 200**
- **1 <= board[i].length <= 200**
- **1 <= word.length <= 10^3**

______________________  

# solution  
time complexity : O(m\*n\*4^l)  
space complexity : O(m\*n + l)  

	class Solution {
	public:
	    bool exist(vector<vector<char>>& board, string word) {
	        h = board.size();
	        if (h == 0) return false;
	        w = board[0].size();
	        
	        for (int i=0; i<h; ++i) {
	            for (int j=0; j<w; ++j) {
	                if (search(board, word, 0, j, i)) return true;
	            }
	        }
	        
	        return false;
	    }
	private:
	    int w, h;
	    bool search(vector<vector<char>>& board, string& word, int d, int x, int y) {
	        if (x<0 || x==w || y<0 || y==h || board[y][x]!=word[d]) return false;
	        if (d == word.length()-1) return true;
	        
	        char cur = board[y][x];
	        board[y][x] = 0;
	        bool res = search(board, word, d+1, x+1, y) ||
	                   search(board, word, d+1, x, y+1) ||
	                   search(board, word, d+1, x-1, y) ||
	                   search(board, word, d+1, x, y-1);
	        board[y][x] = cur;
	        return res;
	    }
	};

對board上所有字母都進行dfs的搜索。  
若發生：  
1. 超出board範圍(x<0 \|\| x==w \|\| y<0 \|\| y==h)。或是
2. 該格子與目前搜索的字母不相同(board[y][x]!=word[d])。

則返回false，若無返回，代表到目前這一格為止皆比對正確，接下來…   
如果目前比對是最後一個字，代表在這board上找到該word string，返回true。  
若還要繼續往下比，先保留目前字母，再把目前格子修改為一非正常值，代表此格已比對過，確保檢查下一個鄰居時回頭檢查到自己是false。  
接著對上下左右鄰居進行下一個字母的比對，比完後將原字母還原回正常值。  
最後返回檢查結果。