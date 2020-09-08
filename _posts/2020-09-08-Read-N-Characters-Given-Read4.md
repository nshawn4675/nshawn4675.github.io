---
layout: post
title:  "157. Read N Characters Given Read4"
date:   2020-09-08 00:00:00 +0800
categories: jekyll update
tags: LeetCode string
---
Given a file and assume that you can only read the file using a given method **<font color="red">read4</font>**, implement a method to read *n* characters.  

# Method read4:  

The API **<font color="red">read4</font>** reads 4 consecutive characters from the file, then writes those characters into the buffer array **<font color="red">buf</font>**.  

The return value is the number of actual characters read.  

Note that **<font color="red">read4()</font>** has its own file pointer, much like **<font color="red">FILE *fp</font>** in C.  

# Definition of read4:  
	Parameter:  char[] buf4
	Returns:    int

	Note: buf4[] is destination not source, the results from read4 will be copied to buf4[]

Below is a high level example of how **<font color="red">read4</font>** works:

![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/ReadNCharsGivenRead4_ex.png?raw=true)  

	File file("abcde"); // File is "abcde", initially file pointer (fp) points to 'a'
	char[] buf4 = new char[4]; // Create buffer with enough space to store characters
	read4(buf4); // read4 returns 4. Now buf = "abcd", fp points to 'e'
	read4(buf4); // read4 returns 1. Now buf = "e", fp points to end of file
	read4(buf4); // read4 returns 0. Now buf = "", fp points to end of file

# Method read:  
By using the **<font color="red">read4</font>** method, implement the method **<font color="red">read</font>** that reads *n* characters from the file and store it in the buffer array **<font color="red">buf</font>**. Consider that you **cannot** manipulate the file directly.  

The return value is the number of actual characters read.  

# Definition of read:  

	Parameters:	char[] buf, int n
	Returns:	int

	Note: buf[] is destination not source, you will need to write the results to buf[]

# Example 1:  
	Input: file = "abc", n = 4
	Output: 3
	Explanation: After calling your read method, buf should contain "abc". We read a total of 3 characters from the file, so return 3. Note that "abc" is the file's content, not buf. buf is the destination buffer that you will have to write the results to.

# Example 2:  
	Input: file = "abcde", n = 5
	Output: 5
	Explanation: After calling your read method, buf should contain "abcde". We read a total of 5 characters from the file, so return 5.

# Example 3:  
	Input: file = "abcdABCD1234", n = 12
	Output: 12
	Explanation: After calling your read method, buf should contain "abcdABCD1234". We read a total of 12 characters from the file, so return 12.

# Example 4:  
	Input: file = "leetcode", n = 5
	Output: 5
	Explanation: After calling your read method, buf should contain "leetc". We read a total of 5 characters from the file, so return 5.
 
# Note:  
- Consider that you **cannot** manipulate the file directly, the file is only accesible for **<font color="red">read4</font>** but **not** for **<font color="red">read</font>**.
- The **<font color="red">read</font>** function will only be called once for each test case.
- You may assume the destination buffer array, **<font color="red">buf</font>**, is guaranteed to have enough space for storing *n* characters.

______________________  

# Solution

Time complexity : O(N)  
Space complexity : O(1)

	/**
	 * The read4 API is defined in the parent class Reader4.
	 *     int read4(char *buf4);
	 */

	class Solution {
	public:
	    /**
	     * @param buf Destination buffer
	     * @param n   Number of characters to read
	     * @return    The number of actual characters read
	     */
	    int read(char *buf, int n) {
	        char buf4[4];
	        int copiedChar = 0, charRead = 4;
	        
	        while (copiedChar < n && charRead == 4) {
	            charRead = read4(buf4);
	            
	            for (int i=0; i<charRead; ++i) {
	                if (copiedChar == n)
	                    return copiedChar;
	                buf[copiedChar++] = buf4[i];
	            }
	        }
	        
	        return copiedChar;
	    }
	};

此方法是：File -> buf4 -> buf。  

若要加速，則使用下面的方法：File -> buf。  
直接將read4讀取的資料append到buf後。  

Time complexity : O(n)  
Space complexity : O(1)

	/**
	 * The read4 API is defined in the parent class Reader4.
	 *     int read4(char *buf4);
	 */

	class Solution {
	public:
	    /**
	     * @param buf Destination buffer
	     * @param n   Number of characters to read
	     * @return    The number of actual characters read
	     */
	    int read(char *buf, int n) {
	        int copiedChar = 0, charRead = 4;
	        
	        while (copiedChar < n && charRead == 4) {
	            charRead = read4(buf+copiedChar);
	            copiedChar += charRead;
	        }
	        
	        return min(n, copiedChar);
	    }
	};