---
layout: post
title:  "[LeetCode July Challange]Day12-Reverse Bits"
date:   2020-07-12 00:00:00 +0800
categories: jekyll update
tags: LeetCode
---
Reverse bits of a given 32 bits unsigned integer.  

# Example 1:  
	Input: 00000010100101000001111010011100
	Output: 00111001011110000010100101000000
	Explanation: The input binary string 00000010100101000001111010011100 represents the unsigned integer 43261596, so return 964176192 which its binary representation is 00111001011110000010100101000000.

# Example 2:  
	Input: 11111111111111111111111111111101
	Output: 10111111111111111111111111111111
	Explanation: The input binary string 11111111111111111111111111111101 represents the unsigned integer 4294967293, so return 3221225471 which its binary representation is 10111111111111111111111111111111.

# Note:  
- Note that in some languages such as Java, there is no unsigned integer type. In this case, both input and output will be given as signed integer type and should not affect your implementation, as the internal binary representation of the integer is the same whether it is signed or unsigned.
- In Java, the compiler represents the signed integers using [2's complement](https://en.wikipedia.org/wiki/Two%27s_complement) notation. Therefore, in **Example 2** above the input represents the signed integer **-3** and the output represents the signed integer **-1073741825**.

______________________  

# solution
time complexity : O(1)  
space complexity : O(1)  

	class Solution {
	public:
	    uint32_t reverseBits(uint32_t n) {
	        uint32_t ans = 0;
	        for (int i=0; i<32; i++) {
	            ans = (ans << 1) | (n & 1);
	            n >>= 1;
	        }
	        return ans;
	    }
	};

將題目的最小位元右移，左移塞入ans。  
則題目的最小位元變成ans的最大位元，達到反轉的效果。  
例子如下所示：  

	題目(→)		答案(←)
	10100110	
	 1010011	       0
	  101001	      01
	   10100	     011
	    1010	    0110
	     101	   01100
	      10	  011001
	       1	 0110010
	       		01100101
