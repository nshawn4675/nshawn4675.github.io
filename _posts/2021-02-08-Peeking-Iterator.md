---
layout: post
title: "[LeetCode February Challange] Day 8 - Peeking Iterator"
date: 2021-02-08 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Design, Iterator, Google, Apple, C++]
---
Design an iterator that supports the <font color="red">peek</font> operation on a list in addition to the <font color="red">hasNext</font> and the <font color="red">next</font> operations.

Implement the <font color="red">PeekingIterator</font> class:

- **<font color="red">PeekingIterator(int[] nums)</font>** Initializes the object with the given integer array <font color="red">nums</font>.
- **<font color="red">int next()</font>** Returns the next element in the array and moves the pointer to the next element.
- **<font color="red">bool hasNext()</font>** Returns <font color="red">true</font> if there are still elements in the array.
- **<font color="red">int peek()</font>** Returns the next element in the array **without** moving the pointer.

# Example 1:

	Input
	["PeekingIterator", "next", "peek", "next", "next", "hasNext"]
	[[[1, 2, 3]], [], [], [], [], []]
	Output
	[null, 1, 2, 2, 3, false]

	Explanation
	PeekingIterator peekingIterator = new PeekingIterator([1, 2, 3]); // [1,2,3]
	peekingIterator.next();    // return 1, the pointer moves to the next element [1,2,3].
	peekingIterator.peek();    // return 2, the pointer does not move [1,2,3].
	peekingIterator.next();    // return 2, the pointer moves to the next element [1,2,3]
	peekingIterator.next();    // return 3, the pointer moves to the next element [1,2,3]
	peekingIterator.hasNext(); // return False

# Constraints:

- <font color="red">1 <= nums.length <= 1000</font>
- <font color="red">1 <= nums[i] <= 1000</font>
- All the calls to <font color="red">next</font> and <font color="red">peek</font> are valid.
- At most <font color="red">1000</font> calls will be made to <font color="red">next</font>, <font color="red">hasNext</font>, and <font color="red">peek</font>.

**Follow up:** How would you extend your design to be generic and work with all types, not just integer?

______________________  

# Solution  

Time complexity : O(1)  
Space complexity : O(1)  

	/*
	 * Below is the interface for Iterator, which is already defined for you.
	 * **DO NOT** modify the interface for Iterator.
	 *
	 *  class Iterator {
	 *      struct Data;
	 *      Data* data;
	 *  public:
	 *      Iterator(const vector<int>& nums);
	 *      Iterator(const Iterator& iter);
	 *
	 *      // Returns the next element in the iteration.
	 *      int next();
	 *
	 *      // Returns true if the iteration has more elements.
	 *      bool hasNext() const;
	 *  };
	 */

	class PeekingIterator : public Iterator {
	private:
	    int peeked;
	public:
	    PeekingIterator(const vector<int>& nums) : Iterator(nums) {
	        // Initialize any member here.
	        // **DO NOT** save a copy of nums and manipulate it directly.
	        // You should only use the Iterator interface methods.
	        peeked = -1;
	    }
	    
	    // Returns the next element in the iteration without advancing the iterator.
	    int peek() {
	        if (peeked == -1 && Iterator::hasNext())
	            peeked = Iterator::next();
	        return peeked;
	    }
	    
	    // hasNext() and next() should behave the same as in the Iterator interface.
	    // Override them if needed.
	    int next() {
	        int res = peeked == -1 ? Iterator::next() : peeked;
	        peeked = -1;
	        return res;
	    }
	    
	    bool hasNext() const {
	        return peeked != -1 || Iterator::hasNext();
	    }
	};