---
layout: post
title: "[LeetCode February Challange] Day 28 - Maximum Frequency Stack"
date: 2021-02-28 00:00:00 +0800
categories: LeetCode
tags: [Hard, Hash Table, Stack, Design, Ordered Set, Amazon, Microsoft, Bloomberg, C++]
---
Design a stack-like data structure to push elements to the stack and pop the most frequent element from the stack.

Implement the <font color="red">FreqStack</font> class:

- **<font color="red">FreqStack()</font>** constructs an empty frequency stack.
- **<font color="red">void push(int val)</font>** pushes an integer <font color="red">val</font> onto the top of the stack.
- **<font color="red">int pop()</font>** removes and returns the most frequent element in the stack.
	- If there is a tie for the most frequent element, the element closest to the stack's top is removed and returned.

# Example 1:

	Input
	["FreqStack", "push", "push", "push", "push", "push", "push", "pop", "pop", "pop", "pop"]
	[[], [5], [7], [5], [7], [4], [5], [], [], [], []]
	Output
	[null, null, null, null, null, null, null, 5, 7, 5, 4]

	Explanation
	FreqStack freqStack = new FreqStack();
	freqStack.push(5); // The stack is [5]
	freqStack.push(7); // The stack is [5,7]
	freqStack.push(5); // The stack is [5,7,5]
	freqStack.push(7); // The stack is [5,7,5,7]
	freqStack.push(4); // The stack is [5,7,5,7,4]
	freqStack.push(5); // The stack is [5,7,5,7,4,5]
	freqStack.pop();   // return 5, as 5 is the most frequent. The stack becomes [5,7,5,7,4].
	freqStack.pop();   // return 7, as 5 and 7 is the most frequent, but 7 is closest to the top. The stack becomes [5,7,5,4].
	freqStack.pop();   // return 5, as 5 is the most frequent. The stack becomes [5,7,4].
	freqStack.pop();   // return 4, as 4, 5 and 7 is the most frequent, but 4 is closest to the top. The stack becomes [5,7].

# Constraints:

- <font color="red">0 <= val <= 10^9</font>
- At most <font color="red">2 * 10^4</font> calls will be made to <font color="red">push</font> and <font color="red">pop</font>.
- It is guaranteed that there will be at least one element in the stack before calling <font color="red">pop</font>.

______________________  

# Solution  

Time complexity : O(1)  
Space complexity : O(n)  

	class FreqStack {
	public:
	    FreqStack() {
	        maxFreq = 0;
	        freqM = {};
	        freqRecentM = {};
	    }
	    
	    void push(int val) {
	        if (maxFreq < ++freqM[val])
	            maxFreq = freqM[val];
	        freqRecentM[freqM[val]].push(val);
	    }
	    
	    int pop() {
	        int res = freqRecentM[maxFreq].top();
	        freqRecentM[maxFreq].pop();
	        --freqM[res];
	        if (freqRecentM[maxFreq].empty())
	            --maxFreq;
	        return res;
	    }
	private:
	    int maxFreq;
	    unordered_map<int, int> freqM;
	    unordered_map<int, stack<int>> freqRecentM;
	};

	/**
	 * Your FreqStack object will be instantiated and called as such:
	 * FreqStack* obj = new FreqStack();
	 * obj->push(val);
	 * int param_2 = obj->pop();
	 */

當 push 時：
1. 更新該數的 freq 值。
2. 更新 maxFreq 值。
3. 在該 freq 出現的順序 stack 中加入該數。

當 pop 時：
1. 取出目前 maxFreq 順序中最新的那一個。
2. 該數的 freq -1。
3. 若 maxFreq 的 stack 為空，則 maxFreq 往下減少 1。