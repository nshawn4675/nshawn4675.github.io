---
layout: post
title:  "[LeetCode July Challange]Day28-Task Scheduler"
date:   2020-07-28 00:00:00 +0800
categories: LeetCode
tags: [Array, Hash Table, Greedy, Sorting, Heap (Priority Queue), Counting, C++]
---
You are given a char array representing tasks CPU need to do. It contains capital letters A to Z where each letter represents a different task. Tasks could be done without the original order of the array. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle.  

However, there is a non-negative integer *n* that represents the cooldown period between two **same tasks** (the same letter in the array), that is that there must be at least *n* units of time between any two same tasks.  

You need to return the **least** number of units of times that the CPU will take to finish all the given tasks.  

# Example 1:  
	Input: tasks = ["A","A","A","B","B","B"], n = 2
	Output: 8
	Explanation: 
	A -> B -> idle -> A -> B -> idle -> A -> B
	There is at least 2 units of time between any two same tasks.

# Example 2:  
	Input: tasks = ["A","A","A","B","B","B"], n = 0
	Output: 6
	Explanation: On this case any permutation of size 6 would work since n = 0.
	["A","A","A","B","B","B"]
	["A","B","A","B","A","B"]
	["B","B","B","A","A","A"]
	...
	And so on.

# Example 3:  
	Input: tasks = ["A","A","A","A","A","A","B","C","D","E","F","G"], n = 2
	Output: 16
	Explanation: 
	One possible solution is
	A -> B -> C -> A -> D -> E -> A -> F -> G -> A -> idle -> idle -> A -> idle -> idle -> A

# Constraints:  
- The number of tasks is in the range **[1, 10000]**.
- The integer **n** is in the range **[0, 100]**.

______________________  

# solution
time complexity : O(n)  
space complexity : O(1)

	class Solution {
	public:
	    int leastInterval(vector<char>& tasks, int n) {
	        vector<int> taskFreq(26, 0);
	        for (char c: tasks) ++taskFreq[c-'A'];
	        
	        int maxFreq = *max_element(taskFreq.begin(), taskFreq.end());
	        
	        size_t ans = (maxFreq-1)*(n+1);
	        ans += count_if(taskFreq.begin(), taskFreq.end(),
	                       [&](int freq) { return freq == maxFreq; });
	        
	        return max(tasks.size(), ans);
	    }
	};

令freq(A) = **k** >= freq(B) >= ... >= freq(z)  
**p** = # tasks have the freq k.  

	ABCD... ABC□... AB□□... ... A....
	└ n+1 ┘ └ n+1 ┘ └ n+1 ┘ ... └ p ┘
	└────────── k-1 ──────────┘

確保每個工作之間的間隔皆為n，如此一來ans = (k-1)\*(n+1)+p  
ans為lower bound，為何是lower bound？  

	AAAABBBCCDDFFG	n=2, freq(A)=k=4
	ans = (4-1)*(2+1)+1 = 10
	長像為		：A__ A__ A__ A
	將B插入後 	：AB_ AB_ AB_ A
	將C插入後	：ABC ABC AB_ A
	將D插入後	：ABC ABC ABD AD       (為其中一個插入結果)
	將F插入後	：ABCDF ABCDF ABD AD   (為其中一個插入結果)
	將G插入後	：ABCDFG ABCDF ABFG AD (為其中一個插入結果)

即算出來的答案若小於task數量，代表無需idle(□)即可將task排好，ans就是task數量。  

又或者可以解譯為：  

	A___A___A___A___ A
	  n   n   n   n

k-1個長度為n的gap，之後次高freq的字母再找gap插，以B為例，  
若freq(B) == freq(A)，則k-1個B依序插入gap，最後一個B加在最後，所以總長度會再+1。

	AB__AB__AB__AB__ AB

若freq(B) < freq(A)，則在A後依序插入gap  

	AB__AB__AB__A___ A

以此類推，從freq高的字母往freq低的字母，依序找gap插入。  
若gap不夠了，也就是不需要idle即可完成排程，最少排程數就是總工作數量。  

	ABCDABCDABCDABCDABCD		若此時我們有2個E要插入
	ABCD_ABCD_ABCDABCDABCD		新增2gaps，給E插入即可
	ABCDEABCDEABCDABCDABCD

	若E的數量與A相同，則新增k個gaps再插入E即可
	ABCD_ABCD_ABCD_ABCD_ABCD_
	ABCDEABCDEABCDEABCDEABCDE

也就是不管怎麼樣，在gap不夠的情況下，都能找到無需額外idle將剩餘工作插入的方法。