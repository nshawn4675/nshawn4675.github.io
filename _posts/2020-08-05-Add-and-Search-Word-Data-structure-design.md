---
layout: post
title:  "[LeetCode August Challange]Day5-Add and Search Word - Data structure design"
date:   2020-08-05 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Design a data structure that supports the following two operations:  

	void addWord(word)
	bool search(word)

search(word) can search a literal word or a regular expression string containing only letters **a-z** or **.**. A **.** means it can represent any one letter.  

# Example:  
	addWord("bad")
	addWord("dad")
	addWord("mad")
	search("pad") -> false
	search("bad") -> true
	search(".ad") -> true
	search("b..") -> true

# Note:  
- You may assume that all words are consist of lowercase letters **a-z**.

______________________  

# solution

Time complexity : O(n^26)  
Space complexity : O(26^n)  

	class WordDictionary {
	public:
	    /** Initialize your data structure here. */
	    WordDictionary(): root_(new Node()) {}
	    
	    /** Adds a word into the data structure. */
	    void addWord(string word) {
	        Node *cur = root_.get();
	        for (char c: word) {
	            if (!cur->next[c-'a'])
	                cur->next[c-'a'] = new Node();
	            cur = cur->next[c-'a'];
	        }
	        cur->isWord = true;
	    }
	    
	    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
	    bool search(string word) {
	        return find(root_.get(), word, 0);
	    }
	private:
	    struct Node {
	        vector<Node*> next;
	        bool isWord;
	        Node(): next(26, nullptr), isWord(false) {}
	        ~Node() {
	            for (Node* node: next)
	                if (node) delete node;
	        }
	    };
	    unique_ptr<Node> root_;
	    
	    bool find(Node* node, string& word, int idx) {
	        if (idx == word.length()) return node->isWord;
	        if (word[idx] == '.') {
	            bool res = false;
	            for (Node *next: node->next) {
	                if (next) res |= find(next, word, idx+1);
	            }
	            return res;
	        }
	        if (node->next[word[idx]-'a'])
	            return find(node->next[word[idx]-'a'], word, idx+1);
	        
	        return false;
	    }
	};

	/**
	 * Your WordDictionary object will be instantiated and called as such:
	 * WordDictionary* obj = new WordDictionary();
	 * obj->addWord(word);
	 * bool param_2 = obj->search(word);
	 */

用到了**Trie**，是存放word的樹，從root開始往子樹走，相當於word從頭走到尾，其中每個Node包含：  
1. 下一個char的node。
2. 從root到目前這個node，是否為存入的word？

因題目需求，存入的word只包含'a'-'z'，因此每個node有26個下一個char的node，初始為nullptr，根據需求而創建子node。  

在search的過程中，若目前找的字母是'.'，就將所有存在的下一個字母的search結果or起來。