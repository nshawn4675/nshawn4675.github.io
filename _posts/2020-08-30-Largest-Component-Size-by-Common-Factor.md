---
layout: post
title:  "[LeetCode August Challange]Day30-Largest Component Size by Common Factor"
date:   2020-08-30 00:00:00 +0800
categories: LeetCode
tags: [Array, Math, Union Find, C++]
---
Given a non-empty array of unique positive integers **<font color="red">A</font>**, consider the following graph:  

- There are **<font color="red">A.length</font>** nodes, labelled **<font color="red">A[0]</font>** to **<font color="red">A[A.length - 1];</font>**
- There is an edge between **<font color="red">A[i]</font>** and **<font color="red">A[j]</font>** if and only if **<font color="red">A[i]</font>** and **<font color="red">A[j]</font>** share a common factor greater than 1.
Return the size of the largest connected component in the graph.

# Example 1:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/LargestComponentSizeByCommonFactor_ex1.png?raw=true)

	Input: [4,6,15,35]
	Output: 4

# Example 2:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/LargestComponentSizeByCommonFactor_ex2.png?raw=true)

	Input: [20,50,9,63]
	Output: 2

# Example 3:  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/LargestComponentSizeByCommonFactor_ex3.png?raw=true)

	Input: [2,3,6,7,4,12,21,39]
	Output: 8

# Note:  
1. **<font color="red">1 <= A.length <= 20000</font>**
2. **<font color="red">1 <= A[i] <= 100000</font>**

______________________  

# Solution

Time complexity : O(sum(sqrt(A[i])))  
Space complexity : O(max(A))

	class Solution {
	public:
	    int largestComponentSize(vector<int>& A) {
	        int max_num = *max_element(A.begin(), A.end());
	        DSU dsu(max_num+1);
	        
	        for (int num: A) {
	            for (int i=2; i<=sqrt(num); ++i) {
	                if (num%i == 0) {
	                    dsu.Union(num, i);
	                    dsu.Union(num, num/i);
	                }
	            }
	        }
	        
	        unordered_map<int, int> parent_cnt;
	        int ans = 1;
	        for (int num: A) {
	            ans = max(ans, ++parent_cnt[dsu.find(num)]);
	        }
	        return ans;
	    }
	private:
	    struct DSU {
	        vector<int> parent_;
	        DSU(int n) {
	            parent_ = vector<int>(n);
	            for(int i=0; i<n; ++i)
	                parent_[i] = i;
	        }
	        int find(int x) {
	            if (parent_[x] != x)
	                parent_[x] = find(parent_[x]);
	            return parent_[x];
	        }
	        void Union(int x, int y) {
	            parent_[find(x)] = parent_[find(y)];
	        }
	    };
	};

使用**[並查集](https://zh.wikipedia.org/wiki/%E5%B9%B6%E6%9F%A5%E9%9B%86)**資料結構。  
以 [4, 6, 15, 35] 為例，圖解一下操作。  

一開始初始化，各num的parent都為自己。 (其實有0~35，忽略沒用到的)  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/DSU0.png?raw=true)  

開始union。  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/DSU1.png?raw=true)
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/DSU2.png?raw=true)
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/DSU3.png?raw=true)
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/DSU4.png?raw=true)

最後對輸入陣列中所有數字進行find，會找到它的最根源，而這四個數字的最根源都是7，故7會被計數4次。