---
layout: post
title:  "[LeetCode September Challange]Day16-Maximum XOR of Two Numbers in an Array"
date:   2020-09-16 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, Bit Manipulation, Trie]
---
Given an integer array **<font color="red">nums</font>**, return the *maximum result of* *<font color="red">nums[i] XOR nums[j]</font>*, where **<font color="red">0 ≤ i ≤ j < n</font>**.  

**Follow up:** Could you do this in **<font color="red">O(n)</font>** runtime?  

# Example 1:  
	Input: nums = [3,10,5,25,2,8]
	Output: 28
	Explanation: The maximum result is 5 XOR 25 = 28.

# Example 2:  
	Input: nums = [0]
	Output: 0

# Example 3:  
	Input: nums = [2,4]
	Output: 6

# Example 4:  
	Input: nums = [8,10,2]
	Output: 10

# Example 5:  
	Input: nums = [14,70,53,83,49,91,36,80,92,51,66,70]
	Output: 127

# Constraints:  
- **<font color="red">1 <= nums.length <= 2 * 104</font>**
- **<font color="red">0 <= nums[i] <= 231 - 1</font>**

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(2^32 - 1)

	class Solution {
	public:
	    int findMaximumXOR(vector<int>& nums) {
	        root = new TrieNode();
	        
	        // build trie tree
	        for (int n: nums) {
	            TrieNode* cur = root;
	            for (int i=31; 0<=i; --i) {
	                int bit = (n>>i) & 1;
	                if (!cur->children[bit])
	                    cur->children[bit] = new TrieNode();
	                cur = cur->children[bit];
	            }
	        }
	        
	        // find maximum xor
	        int ans = INT_MIN;
	        for (int n: nums) {
	            TrieNode* cur = root;
	            int tmp_ans = 0;
	            for (int i=31; 0<=i; --i) {
	                int bit = (n>>i) & 1;
	                if (cur->children[bit^1]) {
	                    tmp_ans += (1<<i);
	                    cur = cur->children[bit^1];
	                } else
	                    cur = cur->children[bit];
	            }
	            ans = max(ans, tmp_ans);
	        }
	        
	        return ans;
	    }
	private:
	    struct TrieNode {
	        vector<TrieNode*> children;
	        TrieNode(): children(2, nullptr) {}
	    };
	    TrieNode* root;
	};

利用各個數字的binary form建Trie，MSB最靠近root，leaf node為LSB。  

再遁一遍，這次朝xor的方向(1→0/0→1)，若沒有的話只能走原方向。  

各個num一路上的xor結果，取最大者，即為解。  