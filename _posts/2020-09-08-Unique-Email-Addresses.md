---
layout: post
title:  "929. Unique Email Addresses"
date:   2020-09-08 00:00:00 +0800
categories: LeetCode
tags: [Array, Hash Table, String, C++]
---
Every email consists of a local name and a domain name, separated by the @ sign.  

For example, in **<font color="red">alice@leetcode.com</font>**, **<font color="red">alice</font>** is the local name, and **<font color="red">leetcode.com</font>** is the domain name.  

Besides lowercase letters, these emails may contain **<font color="red">'.'</font>**s or **<font color="red">'+'</font>**s.  

If you add periods (**<font color="red">'.'</font>**) between some characters in the **local name** part of an email address, mail sent there will be forwarded to the same address without dots in the local name.  For example, **<font color="red">"alice.z@leetcode.com"</font>** and **<font color="red">"alicez@leetcode.com"</font>** forward to the same email address.  (Note that this rule does not apply for domain names.)  

If you add a plus (**<font color="red">'+'</font>**) in the **local name**, everything after the first plus sign will be **ignored**. This allows certain emails to be filtered, for example **<font color="red">m.y+name@email.com</font>** will be forwarded to **<font color="red">my@email.com</font>**.  (Again, this rule does not apply for domain names.)  

It is possible to use both of these rules at the same time.  

Given a list of **<font color="red">emails</font>**, we send one email to each address in the list.  How many different addresses actually receive mails?  

# Example 1:  
	Input: ["test.email+alex@leetcode.com","test.e.mail+bob.cathy@leetcode.com","testemail+david@lee.tcode.com"]
	Output: 2
	Explanation: "testemail@leetcode.com" and "testemail@lee.tcode.com" actually receive mails

# Note:  
- **<font color="red">1 <= emails[i].length <= 100</font>**
- **<font color="red">1 <= emails.length <= 100</font>**
- Each **<font color="red">emails[i]</font>** contains exactly one **<font color="red">'@'</font>** character.
- All local and domain names are non-empty.
- Local names do not start with a **<font color="red">'+'</font>** character.

______________________  

# Solution

Time complexity : O(n^2)  
Space complexity : O(n)

	public:
	    int numUniqueEmails(vector<string>& emails) {
	        unordered_set<string> st;
	        
	        for (string email: emails) {
	            string cleanEmail = "";
	            for (int i=0; i<email.size(); ++i) {
	                if (email[i] == '@' || email[i] == '+')
	                    break;
	                else if (email[i] != '.')
	                    cleanEmail += email[i];
	            }
	            cleanEmail += email.substr(email.find('@'));
	            st.insert(cleanEmail);
	        }
	        
	        return st.size();
	    }
	};

