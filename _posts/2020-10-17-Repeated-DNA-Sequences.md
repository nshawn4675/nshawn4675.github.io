---
layout: post
title:  "[LeetCode October Challange] Day 17 - Repeated DNA Sequences"
date:   2020-10-17 00:00:00 +0800
categories: LeetCode
tags: [Medium, Hash Table, String, Bit Manipulation, Sliding Window, Rolling Hash, Hash Function, Amazon, Apple, Microsoft, C++]
---
All DNA is composed of a series of nucleotides abbreviated as <font color="red">'A'</font>, <font color="red">'C'</font>, <font color="red">'G'</font>, and <font color="red">'T'</font>, for example: <font color="red">"ACGAATTCCG"</font>. When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.  

Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.  

# Example 1:  
	Input: s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
	Output: ["AAAAACCCCC","CCCCCAAAAA"]

# Example 2:  
	Input: s = "AAAAAAAAAAAAA"
	Output: ["AAAAAAAAAA"]

# Constraints:  
- <font color="red">0 <= s.length <= 105</font>
- <font color="red">s[i]</font> is <font color="red">'A'</font>, <font color="red">'C'</font>, <font color="red">'G'</font>, or <font color="red">'T'</font>.

______________________  

# Solution  

### Rabin-Karp  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    vector<string> findRepeatedDnaSequences(string s) {
	        const int len = s.length();
	        const int L = 10, base = 4;
	        if (len < L) return {};
	        
	        const int hi_w = pow(base, L);
	        unordered_map<char, int> to_int = { {'A', 0}, {'C', 1}, {'G', 2}, {'T', 3}};
	        unordered_map<int, int> seen = {};
	        vector<string> ans = {};
	        
	        int h = 0;
	        for (int i=0; i<len-L+1; ++i) {
	            if (i == 0) {
	                for (int j=0; j<L; ++j)
	                    h = h*base + to_int[s[j]];
	            } else {
	                h = h*base - to_int[s[i-1]]*hi_w + to_int[s[i+L-1]];
	            }
	            string hit_str = s.substr(i, L);
	            if (seen.count(h)) {
	                if (find(ans.begin(), ans.end(), hit_str) == ans.end())
	                    ans.push_back(hit_str);
	            } else ++seen[h];
	        }
	        
	        return ans;
	    }
	};

使用Rabin-Karp rolling hash的技巧。  

將字編碼，以數字呈現，其hash值為在相對應的位置乘上相對應的權重。  
例：2030 => 2\*4^3 + 0\*4^2 + 3\*4^1 + 0\*4^0  

根據算出來的hash值，判斷是否看過。  
若hash值已看過，且沒有在ans中，則將此substring加入ans中。  
若hash值沒看過，將hash值加入seen。  


### Bit Manipulation  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    vector<string> findRepeatedDnaSequences(string s) {
	        const int len = s.length();
	        const int L = 10, base = 4;
	        if (len < L) return {};
	        
	        const int hi_w = pow(base, L);
	        unordered_map<char, int> to_int = { {'A', 0}, {'C', 1}, {'G', 2}, {'T', 3}};
	        unordered_map<int, int> seen = {};
	        vector<string> ans = {};
	        
	        int h = 0;
	        for (int i=0; i<len-L+1; ++i) {
	            if (i == 0) {
	                for (int j=0; j<L; ++j)
	                    h = h<<2 | to_int[s[j]];
	            } else {
	                h = h<<2 | to_int[s[i+L-1]];
	                h &= ~(3<<2*L);
	            }
	            string hit_str = s.substr(i, L);
	            if (seen.count(h)) {
	                if (find(ans.begin(), ans.end(), hit_str) == ans.end())
	                    ans.push_back(hit_str);
	            } else ++seen[h];
	        }
	        
	        return ans;
	    }
	};

與上者的方法，只差在計算hash value的地方，  
上者是用4進制來計算hash值，這個是用bit的方式看待。  

定義，A=0=00，C=1=01，G=2=10，T=3=11。  

slice window：  
每次左移2bit => h = h<<2  
補上新bits => h = h | to_int[s[i+L-1]]  
去掉舊bits => h = h & \~(3<<2\*L)。  

\~(3<<2\*L)的意思是，將"11"左移L個位置(每個位置2bit)，會到要移除的舊2bit，反相代表那2bit是0(&後會不見)，其餘為1(&後會保留)。