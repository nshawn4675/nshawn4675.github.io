---
layout: post
title:  "170. Two Sum III - Data structure design"
date:   2020-10-14 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Easy, Hash Table, LinkedIn]
---
Design a data structure that accepts a stream of integers and checks if it has a pair of integers that sum up to a particular value.  

Implement the <font color="red">TwoSum class</font> :  
- **<font color="red">TwoSum()</font>** Initializes the <font color="red">TwoSum</font> object, with an empty array initially.
- **<font color="red">void add(int number)</font>** Adds <font color="red">number</font> to the data structure.
- **<font color="red">boolean find(int value)</font>** Returns <font color="red">true</font> if there exists any pair of numbers whose sum is equal to <font color="red">value</font>, otherwise, it returns <font color="red">false</font>.

# Example 1:  
	Input
	["TwoSum", "add", "add", "add", "find", "find"]
	[[], [1], [3], [5], [4], [7]]
	Output
	[null, null, null, null, true, false]

	Explanation
	TwoSum twoSum = new TwoSum();
	twoSum.add(1);   // [] --> [1]
	twoSum.add(3);   // [1] --> [1,3]
	twoSum.add(5);   // [1,3] --> [1,3,5]
	twoSum.find(4);  // 1 + 3 = 4, return true
	twoSum.find(7);  // No two integers sum up to 7, return false

# Constraints:  
- <font color="red">-105 <= number <= 105</font>
- <font color="red">-231 <= value <= 231 - 1</font>
- At most <font color="red">5 * 104</font> calls will be made to <font color="red">add</font> and <font color="red">find</font>.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	class TwoSum {
	public:
	    /** Initialize your data structure here. */
	    TwoSum() {
	        nums = {};
	    }
	    
	    /** Add the number to an internal data structure.. */
	    void add(int number) {
	        ++nums[number];
	    }
	    
	    /** Find if there exists any pair of numbers which sum is equal to the value. */
	    bool find(int value) {
	        for (const auto& it: nums) {
	            if (value == -2147483648 && 0 < it.first)
	                continue;
	            int diff = value - it.first;
	            if (diff == it.first) {
	                if (it.second > 1)
	                    return true;
	            } else {
	                if (nums.count(diff) > 0)
	                    return true;
	            }
	        }
	        return false;
	    }
	private:
	    unordered_map<int, int> nums;
	};

	/**
	 * Your TwoSum object will be instantiated and called as such:
	 * TwoSum* obj = new TwoSum();
	 * obj->add(number);
	 * bool param_2 = obj->find(value);
	 */

用hash table記錄每個add的數字的數量。  

因value = a + b，value - a = b。  
故可以用value-某數，確認另一數是否add過。  

先看看這個diff = value - a，是否與b相同，若相同，看b的數量是否有2以上，有的話則可以b+b=value。  
若不相同，則找diff在hash table中被add過的數量，若有1個以上，則可以a + b = value。