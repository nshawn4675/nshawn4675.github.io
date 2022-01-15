---
layout: post
title: "[LeetCode March Challange] Day 04 - Intersection of Two Linked Lists"
date: 2021-03-04 00:00:00 +0800
categories: LeetCode
tags: [Easy, Hash Table, Link List, Two Pointers, Microsoft, Amazon, Facebook, ByteDance, LinkedIn, Paypal, Apple, Bloomberg, Intuit, C++]
---
Given the heads of two singly linked-lists <font color="red">headA</font> and <font color="red">headB</font>, return *the node at which the two lists intersect*. If the two linked lists have no intersection at all, return <font color="red">null</font>.

For example, the following two linked lists begin to intersect at node <font color="red">c1</font>:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/160_ex.png?raw=true)

It is **guaranteed** that there are no cycles anywhere in the entire linked structure.

**Note** that the linked lists must **retain their original** structure after the function returns.

# Example 1:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/160_ex1.png?raw=true)

	Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3
	Output: Intersected at '8'
	Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect).
	From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,6,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.

# Example 2:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/160_ex2.png?raw=true)

	Input: intersectVal = 2, listA = [1,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
	Output: Intersected at '2'
	Explanation: The intersected node's value is 2 (note that this must not be 0 if the two lists intersect).
	From the head of A, it reads as [1,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.

# Example 3:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/160_ex3.png?raw=true)

	Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
	Output: No intersection
	Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
	Explanation: The two lists do not intersect, so return null.

# Constraints:

- The number of nodes of <font color="red">listA</font> is in the <font color="red">m</font>.
- The number of nodes of <font color="red">listB</font> is in the <font color="red">n</font>.
- <font color="red">1 <= m, n <= 3 * 10^4</font>
- <font color="red">1 <= Node.val <= 10^5</font>
- <font color="red">1 <= skipA <= m</font>
- <font color="red">1 <= skipB <= n</font>
- **<font color="red">intersectVal</font>** is <font color="red">0</font> if <font color="red">listA</font> and <font color="red">listB</font> do not intersect.
- **<font color="red">intersectVal == listA[skipA + 1] == listB[skipB + 1]</font>** if <font color="red">listA</font> and <font color="red">listB</font> intersect.

**Follow up:** Could you write a solution that runs in <font color="red">O(n)</font> time and use only <font color="red">O(1)</font> memory?

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(1)  

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     ListNode *next;
	 *     ListNode(int x) : val(x), next(NULL) {}
	 * };
	 */
	class Solution {
	public:
	    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
	        ListNode *A = headA, *B = headB;
	        while (A != B) {
	            A = A ? A->next : headB;
	            B = B ? B->next : headA;
	        }
	        return A;
	    }
	};

