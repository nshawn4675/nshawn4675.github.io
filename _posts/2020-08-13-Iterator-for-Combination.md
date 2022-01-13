---
layout: post
title:  "[LeetCode August Challange]Day13-Iterator for Combination"
date:   2020-08-13 00:00:00 +0800
categories: LeetCode
tags: [String, Backtracking, Design, Iterator, C++]
---
Design an Iterator class, which has:

- A constructor that takes a string **<font color="red">characters</font>** of **sorted distinct** lowercase English letters and a number **<font color="red">combinationLength</font>** as arguments.
- A function *next()* that returns the next combination of length **<font color="red">combinationLength</font>** in **lexicographical order**.
- A function *hasNext()* that returns **<font color="red">True</font>** if and only if there exists a next combination.

# Example:
	CombinationIterator iterator = new CombinationIterator("abc", 2); // creates the iterator.

	iterator.next(); // returns "ab"
	iterator.hasNext(); // returns true
	iterator.next(); // returns "ac"
	iterator.hasNext(); // returns true
	iterator.next(); // returns "bc"
	iterator.hasNext(); // returns false

# Constraints:  
- **<font color="red">1 <= combinationLength <= characters.length <= 15</font>**
- There will be at most **<font color="red">10^4</font>** function calls per test.
- It's guaranteed that all calls of the function **<font color="red">next</font>** are valid.

______________________  

# solution

	class CombinationIterator {
	public:
	    CombinationIterator(string characters, int combinationLength) {
	        src = characters;
	        len_ = src.length();
	        resLen_ = combinationLength;
	        backtracking("", 0);
	        len_ = combinations.size();
	        cur_ = 0;
	    }
	    
	    string next() {
	        return cur_ < len_ ? combinations[cur_++] : "";
	    }
	    
	    bool hasNext() {
	        return cur_ < len_;
	    }
	private:
	    string src;
	    vector<string> combinations;
	    int len_, cur_, resLen_;
	    
	    void backtracking(string s, int idx) {
	        if (s.length() == resLen_)
	            combinations.push_back(s);
	        else {
	            for (int i=idx; i<len_; ++i)
	                backtracking(s+src[i], i+1);
	        }
	    }
	};

	/**
	 * Your CombinationIterator object will be instantiated and called as such:
	 * CombinationIterator* obj = new CombinationIterator(characters, combinationLength);
	 * string param_1 = obj->next();
	 * bool param_2 = obj->hasNext();
	 */

利用backtracking，加上長度限制，一一將結果組合加入容器中。  
因constructor只做一次，後面會call很多次其它的function，因此能做的儘量在constructor中做完，減少其它function的時間。  
hasNext()的部份，用計數變數判斷容器是否還有東西。  
next()的部份，先利用hasNext()判斷容器是否還有東西，有的話就回傳該物，且計數+1，沒有的話回傳空物件。