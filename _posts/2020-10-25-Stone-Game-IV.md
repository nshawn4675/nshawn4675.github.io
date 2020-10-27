---
layout: post
title:  "[LeetCode October Challange] Day 25 - Stone Game IV"
date:   2020-10-25 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Hard, Dynamic Programming, Microsoft]
---
Alice and Bob take turns playing a game, with Alice starting first.  

Initially, there are <font color="red">n</font> stones in a pile.  On each player's turn, that player makes a move consisting of removing **any** non-zero **square number** of stones in the pile.  

Also, if a player cannot make a move, he/she loses the game.  

Given a positive integer <font color="red">n</font>. Return <font color="red">True</font> if and only if Alice wins the game otherwise return <font color="red">False</font>, assuming both players play optimally.

# Example 1:  
	Input: n = 1
	Output: true
	Explanation: Alice can remove 1 stone winning the game because Bob doesn't have any moves.

# Example 2: 
	Input: n = 2
	Output: false
	Explanation: Alice can only remove 1 stone, after that Bob removes the last one winning the game (2 -> 1 -> 0).

# Example 3:  
	Input: n = 4
	Output: true
	Explanation: n is already a perfect square, Alice can win with one move, removing 4 stones (4 -> 0).

# Example 4:  
	Input: n = 7
	Output: false
	Explanation: Alice can't win the game if Bob plays optimally.
	If Alice starts removing 4 stones, Bob will remove 1 stone then Alice should remove only 1 stone and finally Bob removes the last one (7 -> 3 -> 2 -> 1 -> 0). 
	If Alice starts removing 1 stone, Bob will remove 4 stones then Alice only can remove 1 stone and finally Bob removes the last one (7 -> 6 -> 2 -> 1 -> 0).

# Example 5:  
	Input: n = 17
	Output: false
	Explanation: Alice can't win the game if Bob plays optimally.

# Constraints:  
- <font color="red">1 <= n <= 10^5</font>

______________________  

# Solution  

Time complexity : O(n\*sqrt(n))  
Space complexity : O(n)  

	class Solution {
	public:
	    bool winnerSquareGame(int n) {
	        vector<int> mem(n+1, 0);
	        function<int(int)> win = [&](int n) -> int {
	            if (0 == n) return -1;
	            if (mem[n]) return mem[n];
	            for (int take=sqrt(n); 1<=take; --take) {
	                if (win(n-take*take) < 0) return mem[n] = 1;
	            }
	            return mem[n] = -1;
	        };
	        return win(n) > 0;
	    }
	};

若alice想要贏得遊戲，就思考如何做選擇讓Bob輸。  

以目前的石頭數，recursive考量可能的選擇，找出會讓Bob輸的去執行。  
若都找不到會讓Bob輸的路，就是Alice輸。  

用memoization記憶已做過的結果，避免重覆計算，增加效能。  