---
layout: post
title: "[LeetCode April Challange] Day 13 - Flatten Nested List Iterator"
date: 2021-04-13 00:00:00 +0800
categories: LeetCode
tags: [Medium, Stack, Tree, Depth-First Search, Design, Queue, Iterator, Facebook, Apple, Amazon, Airbnb, LinkedIn, Bloomberg, Oracle, C++]
---
You are given a nested list of integers <font color="red">nestedList</font>. Each element is either an integer or a list whose elements may also be integers or other lists. Implement an iterator to flatten it.

Implement the <font color="red">NestedIterator</font> class:

- **<font color="red">NestedIterator(List&lt;NestedInteger&gt; nestedList)</font>** Initializes the iterator with the nested list <font color="red">nestedList</font>.
- **<font color="red">int next()</font>** Returns the next integer in the nested list.
- **<font color="red">boolean hasNext()</font>** Returns <font color="red">true</font> if there are still some integers in the nested list and <font color="red">false</font> otherwise.

# Example 1:

    Input: nestedList = [[1,1],2,[1,1]]
    Output: [1,1,2,1,1]
    Explanation: By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,1,2,1,1].

# Example 2:

    Input: nestedList = [1,[4,[6]]]
    Output: [1,4,6]
    Explanation: By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,4,6].
 

# Constraints:

- <font color="red">1 <= nestedList.length <= 500</font>
- The values of the integers in the nested list is in the range <font color="red">[-10^6, 10^6]</font>.

______________________  

# Solution  

    /**
    * // This is the interface that allows for creating nested lists.
    * // You should not implement it, or speculate about its implementation
    * class NestedInteger {
    *   public:
    *     // Return true if this NestedInteger holds a single integer, rather than a nested list.
    *     bool isInteger() const;
    *
    *     // Return the single integer that this NestedInteger holds, if it holds a single integer
    *     // The result is undefined if this NestedInteger holds a nested list
    *     int getInteger() const;
    *
    *     // Return the nested list that this NestedInteger holds, if it holds a nested list
    *     // The result is undefined if this NestedInteger holds a single integer
    *     const vector<NestedInteger> &getList() const;
    * };
    */

    class NestedIterator {
    public:
        NestedIterator(vector<NestedInteger> &nestedList) {
            begin.push(nestedList.begin());
            end.push(nestedList.end());
        }
        
        int next() {
            return hasNext() ? (begin.top()++)->getInteger() : -1;
        }
        
        bool hasNext() {
            while (!begin.empty()) {
                if (begin.top() == end.top()) {
                    begin.pop();
                    end.pop();
                } else {
                    if (begin.top()->isInteger()) return true;
                    end.push(begin.top()->getList().end());
                    begin.push((begin.top()++)->getList().begin());
                }
            }
            return false;
        }
    private:
        stack<vector<NestedInteger>::iterator> begin, end;
    };

    /**
    * Your NestedIterator object will be instantiated and called as such:
    * NestedIterator i(nestedList);
    * while (i.hasNext()) cout << i.next();
    */

用 begin 和 end stack 來存放第 n level vector 的起終。  
呼叫 hasNext() 時，會將 begin.top() 指向下一個Integer。  