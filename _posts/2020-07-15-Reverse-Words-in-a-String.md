---
layout: post
title:  "[LeetCode July Challange]Day15-Reverse Words in a String"
date:   2020-07-15 00:00:00 +0800
categories: LeetCode
tags: [Two Pointers, String, C++]
---
Given an input string, reverse the string word by word.  

# Example 1:  
	Input: "the sky is blue"
	Output: "blue is sky the"

# Example 2:  
	Input: "  hello world!  "
	Output: "world! hello"
	Explanation: Your reversed string should not contain leading or trailing spaces.

# Example 3:  
	Input: "a good   example"
	Output: "example good a"
	Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.

# Note:  
- A word is defined as a sequence of non-space characters.
- Input string may contain leading or trailing spaces. However, your reversed string should not contain leading or trailing spaces.
- You need to reduce multiple spaces between two words to a single space in the reversed string.

______________________  

# solution
time complexity : O(n)  
space complexity : O(1)  

	class Solution {
	public:
	    string reverseWords(string s) {
	        int len = s.length();
	        if (len == 0) return "";
	        
	        int scout = 0, wordCnt = 0, writeIdx = 0, wStartIdx = 0;
	        while (scout < len) {
	            // skip front & back spaces
	            while (scout < len && s[scout] == ' ') ++scout;
	            if (scout >= len) break;
	            
	            // record start point
	            if (wordCnt) s[writeIdx++] = ' ';
	            wStartIdx = writeIdx;
	            
	            // writing
	            while (scout < len && s[scout] != ' ') {
	                s[writeIdx++] = s[scout++];
	            }
	            
	            reverseWord(s, wStartIdx, writeIdx-1);
	            ++wordCnt;
	        }
	        
	        s.resize(writeIdx);
	        reverseWord(s, 0, writeIdx-1);
	        return s;
	    }
	private:
	    void reverseWord(string& s, int start, int end) {
	        for (int i=start, j=end; i<j; ++i,--j) {
	            s[i] ^= s[j];
	            s[j] ^= s[i];
	            s[i] ^= s[j];
	        }
	    }
	};

舉個例子：  

	"  a good   example   "  

經過scout跑一遍後，變成  

	"a doog elpmaxemple   "  

經過resize後，變成  

	"a doog elpmaxe"  

最後再reverse整個字串後  

	"example good a"  
	
即為答案。