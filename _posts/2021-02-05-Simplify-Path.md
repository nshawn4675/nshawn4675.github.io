---
layout: post
title:  "[LeetCode February Challange] Day 5 - Simplify Path"
date:   2021-02-05 00:00:00 +0800
categories: jekyll update
tags: [LeetCode, Medium, String, Stack, Facebok, Amazon, Microsoft]
---
Given a string <font color="red">path</font>, which is an **absolute path** (starting with a slash <font color="red">'/'</font>) to a file or directory in a Unix-style file system, convert it to the simplified **canonical path**.

In a Unix-style file system, a period <font color="red">'.'</font> refers to the current directory, a double period <font color="red">'..'</font> refers to the directory up a level, and any multiple consecutive slashes (i.e. <font color="red">'//'</font>) are treated as a single slash <font color="red">'/'</font>. For this problem, any other format of periods such as <font color="red">'...'</font> are treated as file/directory names.

The **canonical path** should have the following format:

- The path starts with a single slash <font color="red">'/'</font>.
- Any two directories are separated by a single slash <font color="red">'/'</font>.
- The path does not end with a trailing <font color="red">'/'</font>.
- The path only contains the directories on the path from the root directory to the target file or directory (i.e., no period <font color="red">'.'</font> or double period <font color="red">'..'</font>)
- Return *the simplified **canonical path***.

# Example 1:

	Input: path = "/home/"
	Output: "/home"
	Explanation: Note that there is no trailing slash after the last directory name.

# Example 2:

	Input: path = "/../"
	Output: "/"
	Explanation: Going one level up from the root directory is a no-op, as the root level is the highest level you can go.

# Example 3:

	Input: path = "/home//foo/"
	Output: "/home/foo"
	Explanation: In the canonical path, multiple consecutive slashes are replaced by a single one.

# Example 4:

	Input: path = "/a/./b/../../c/"
	Output: "/c"
 

# Constraints:

- <font color="red">1 <= path.length <= 3000</font>
- **<font color="red">path</font>** consists of English letters, digits, period <font color="red">'.'</font>, slash <font color="red">'/'</font> or <font color="red">'_'</font>.
- **<font color="red">path</font>** is a valid absolute Unix path.

______________________  

# Solution  

Time complexity : O(n)  
Space complexity : O(n)  

	class Solution {
	public:
	    string simplifyPath(string path) {
	        stringstream ss(path);
	        string ans, token;
	        stack<string> stk;
	        
	        while (getline(ss, token, '/')) {
	            if (token == "" || token == ".") continue;
	            else if (token == "..") {
	                if (!stk.empty())stk.pop();
	            }
	            else stk.push(token);
	        }
	        
	        while (!stk.empty()) {
	            ans = "/" + stk.top() + ans;
	            stk.pop();
	        }
	        
	        return ans == "" ? "/" : ans;
	    }
	};

利用 stack 記錄拜訪過程。