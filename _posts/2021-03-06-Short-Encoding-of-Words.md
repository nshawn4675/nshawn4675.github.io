---
layout: post
title:  "[LeetCode March Challange] Day 06 - Short Encoding of Words"
date:   2021-03-06 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium]
---
A **valid encoding** of an array of <font color="red">words</font> is any reference string <font color="red">s</font> and array of indices <font color="red">indices</font> such that:

- <font color="red">words.length == indices.length</font>
- The reference string <font color="red">s</font> ends with the <font color="red">'#'</font> character.
- For each index <font color="red">indices[i]</font>, the **substring** of <font color="red">s</font> starting from <font color="red">indices[i]</font> and up to (but not including) the next <font color="red">'#'</font> character is equal to <font color="red">words[i]</font>.
Given an array of <font color="red">words</font>, return *the **length of the shortest reference string** <font color="red">s</font> possible of any **valid encoding** of <font color="red">words</font>*.

# Example 1:

	Input: words = ["time", "me", "bell"]
	Output: 10
	Explanation: A valid encoding would be s = "time#bell#" and indices = [0, 2, 5].
	words[0] = "time", the substring of s starting from indices[0] = 0 to the next '#' is underlined in "time#bell#"
	words[1] = "me", the substring of s starting from indices[1] = 2 to the next '#' is underlined in "time#bell#"
	words[2] = "bell", the substring of s starting from indices[2] = 5 to the next '#' is underlined in "time#bell#"

# Example 2:

	Input: words = ["t"]
	Output: 2
	Explanation: A valid encoding would be s = "t#" and indices = [0].

# Constraints:

- <font color="red">1 <= words.length <= 2000</font>
- <font color="red">1 <= words[i].length <= 7</font>
- **<font color="red">words[i]</font>** consists of only lowercase letters.

______________________  

# Solution  

# Remove suffix

Time complexity : O(n\*l^2) (n: # words, l: word len)  
Space complexity : O(n\*l)

	class Solution {
	public:
	    int minimumLengthEncoding(vector<string>& words) {
	        set<string> st(words.begin(), words.end());
	        for (string s: st) {
	            for (int i=s.length()-1; 0<i; --i) {
	                st.erase(s.substr(i));
	            }
	        }
	        
	        int ans = 0;
	        for (string s: st)
	            ans += s.length() + 1;
	        return ans;
	    }
	};

# Trie

Time complexity : O(n\*l)  
Space complexity :O(26^l)  

	class Node {
	public:
	    Node *children[26];
	    int len;
	    ~Node();
	    Node(int val) {
	        for (int i=0; i<26; ++i)
	            children[i] = nullptr;
	        len = val;
	    }
	};

	class Solution {
	public:
	    int minimumLengthEncoding(vector<string>& words) {
	        Node *root = new Node(0);
	        
	        for (string w: words) {
	            Node *cur = root;
	            for (int i=w.length()-1; 0<=i; --i) {
	                if (cur->children[w[i]-'a'] == nullptr)
	                    cur->children[w[i]-'a'] = new Node(cur->len+1);
	                cur = cur->children[w[i]-'a'];
	            }
	        }
	        
	        ans = 0;
	        dfs(root);
	        return ans;
	    }
	private:
	    int ans;
	    void dfs(Node *node) {
	        if (node == nullptr) return;
	        bool isLast = true;
	        for (Node *c: node->children) {
	            if (c != nullptr) {
	                isLast = false;
	                dfs(c);
	            }
	        }
	        
	        if (isLast) ans += node->len + 1;
	    }
	};

將每個字從尾到頭尋訪建樹。  
再 dfs 尋訪整棵樹，若其沒有 children，代表為完整的字，更新 ans。