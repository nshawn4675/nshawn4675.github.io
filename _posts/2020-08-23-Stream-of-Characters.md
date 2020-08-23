---
layout: post
title:  "[LeetCode August Challange]Day23-Stream of Characters"
date:   2020-08-23 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Implement the **<font color="red">StreamChecker</font>** class as follows:  

- **<font color="red">StreamChecker(words)</font>**: Constructor, init the data structure with the given words.
- **<font color="red">query(letter)</font>**: returns true if and only if for some **<font color="red">k >= 1</font>**, the last **<font color="red">k</font>** characters queried (in order from oldest to newest, including this letter just queried) spell one of the words in the given list.  

# Example:  
	StreamChecker streamChecker = new StreamChecker(["cd","f","kl"]); // init the dictionary.
	streamChecker.query('a');          // return false
	streamChecker.query('b');          // return false
	streamChecker.query('c');          // return false
	streamChecker.query('d');          // return true, because 'cd' is in the wordlist
	streamChecker.query('e');          // return false
	streamChecker.query('f');          // return true, because 'f' is in the wordlist
	streamChecker.query('g');          // return false
	streamChecker.query('h');          // return false
	streamChecker.query('i');          // return false
	streamChecker.query('j');          // return false
	streamChecker.query('k');          // return false
	streamChecker.query('l');          // return true, because 'kl' is in the wordlist
 

# Note:  
- **<font color="red">1 <= words.length <= 2000</font>**
- **<font color="red">1 <= words[i].length <= 2000</font>**
- Words will only consist of lowercase English letters.
- Queries will only consist of lowercase English letters.
- The number of queries is at most 40000.

______________________  

# solution

	class StreamChecker {
	public:
	    StreamChecker(vector<string>& words) {
	        s_ = "";
	        root_ = new TrieNode();
	        
	        for (string word: words) {
	            TrieNode *cur = root_;
	            for (int i=word.length()-1; 0<=i; --i) {
	                int idx = word[i]-'a';
	                if (!cur->nexts[idx])
	                    cur->nexts[idx] = new TrieNode();
	                cur = cur->nexts[idx];
	            }
	            cur->flag = true;
	        }
	    }
	    
	    bool query(char letter) {
	        s_ += letter;
	        
	        TrieNode *cur = root_;
	        for (int i=s_.length()-1; 0<=i; --i) {
	            int idx = s_[i]-'a';
	            if (!cur->nexts[idx]) return false;
	            cur = cur->nexts[idx];
	            if (cur->flag) return true;
	        }
	        
	        return false;
	    }
	private:
	    struct TrieNode{
	        bool flag;
	        TrieNode* nexts[26];
	        TrieNode(): flag(false), nexts{nullptr} {};
	    };
	    TrieNode *root_;
	    string s_;
	};

	/**
	 * Your StreamChecker object will be instantiated and called as such:
	 * StreamChecker* obj = new StreamChecker(words);
	 * bool param_1 = obj->query(letter);
	 */

使用Trie建樹，為了在query時能達到題目所需的功能，每個字建樹時是將該字反過來看建出的，query時也用字串記錄下歷史query記錄，以尾至頭的方式查詢，若有找到當初建樹時出現的字，返回true，沒有則返回false。