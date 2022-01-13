---
layout: post
title:  "[LeetCode August Challange]Day19-Goat Latin"
date:   2020-08-19 00:00:00 +0800
categories: LeetCode
tags: [String, C++]
---
A sentence **<font color="red">S</font>** is given, composed of words separated by spaces. Each word consists of lowercase and uppercase letters only.

We would like to convert the sentence to *"Goat Latin"* (a made-up language similar to Pig Latin.)

The rules of Goat Latin are as follows:

If a word begins with a vowel (a, e, i, o, or u), append **<font color="red">"ma"</font>** to the end of the word.
For example, the word 'apple' becomes 'applema'.
 
If a word begins with a consonant (i.e. not a vowel), remove the first letter and append it to the end, then add **<font color="red">"ma"</font>**.
For example, the word **<font color="red">"goat"</font>** becomes **<font color="red">"oatgma"</font>**.
 
Add one letter **<font color="red">'a'</font>** to the end of each word per its word index in the sentence, starting with 1.
For example, the first word gets **<font color="red">"a"</font>** added to the end, the second word gets **<font color="red">"aa"</font>** added to the end and so on.
Return the final sentence representing the conversion from **<font color="red">S</font>** to Goat Latin. 

# Example 1:  
	Input: "I speak Goat Latin"
	Output: "Imaa peaksmaaa oatGmaaaa atinLmaaaaa"

# Example 2:  
	Input: "The quick brown fox jumped over the lazy dog"
	Output: "heTmaa uickqmaaa rownbmaaaa oxfmaaaaa umpedjmaaaaaa overmaaaaaaa hetmaaaaaaaa azylmaaaaaaaaa ogdmaaaaaaaaaa"

Notes:  
- **<font color="red">S</font>** contains only uppercase, lowercase and spaces. Exactly one space between each word.
- **<font color="red">1 <= S.length <= 150</font>**.

______________________  

# Solution

Time complexity : O(n)  
Space complexity : O(n)

	class Solution {
	public:
	    string toGoatLatin(string S) {
	        const string vowels = "AEIOUaeiou";
	        int cnt = 0;
	        string word, ans;
	        istringstream iss(S);
	        while (iss >> word) {
	            if (vowels.find(word[0]) == string::npos)
	                word = word.substr(1) + word[0];
	            ans += " " + word + "ma" + string(++cnt, 'a');
	        }
	        return ans.substr(1);
	    }
	};

使用istringstream歷遍S中的每個word。  
npos指的是字串的尾巴，找不到時會跑到這邊。  
一個一個加到ans中，最後ans頭會多出一個空白，跳過它即可。  