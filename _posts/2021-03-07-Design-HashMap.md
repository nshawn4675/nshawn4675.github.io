---
layout: post
title: "[LeetCode March Challange] Day 07 - Design HashMap"
date: 2021-03-07 00:00:00 +0800
categories: LeetCode
tags: [Easy, Array, Hash Table, Linked List, Design, Hash Function, Goldman Sachs, Apple, Amazon, Oracle, Twitter, LinkedIn, Google, eBay, Microsoft, ServiceNow, VMware, ByteDance, C++]
---
Design a HashMap without using any built-in hash table libraries.

Implement the <font color="red">MyHashMap</font> class:

- **<font color="red">MyHashMap()</font>** initializes the object with an empty map.
- **<font color="red">void put(int key, int value)</font>** inserts a <font color="red">(key, value)</font> pair into the HashMap. If the <font color="red">key</font> already exists in the map, update the corresponding <font color="red">value</font>.
- **<font color="red">int get(int key)</font>** returns the <font color="red">value</font> to which the specified <font color="red">key</font> is mapped, or <font color="red">-1</font> if this map contains no mapping for the <font color="red">key</font>.
- **<font color="red">void remove(key)</font>** removes the <font color="red">key</font> and its corresponding <font color="red">value</font> if the map contains the mapping for the <font color="red">key</font>.

# Example 1:

	Input
	["MyHashMap", "put", "put", "get", "get", "put", "get", "remove", "get"]
	[[], [1, 1], [2, 2], [1], [3], [2, 1], [2], [2], [2]]
	Output
	[null, null, null, 1, -1, null, 1, null, -1]

	Explanation
	MyHashMap myHashMap = new MyHashMap();
	myHashMap.put(1, 1); // The map is now [[1,1]]
	myHashMap.put(2, 2); // The map is now [[1,1], [2,2]]
	myHashMap.get(1);    // return 1, The map is now [[1,1], [2,2]]
	myHashMap.get(3);    // return -1 (i.e., not found), The map is now [[1,1], [2,2]]
	myHashMap.put(2, 1); // The map is now [[1,1], [2,1]] (i.e., update the existing value)
	myHashMap.get(2);    // return 1, The map is now [[1,1], [2,1]]
	myHashMap.remove(2); // remove the mapping for 2, The map is now [[1,1]]
	myHashMap.get(2);    // return -1 (i.e., not found), The map is now [[1,1]]

# Constraints:

- <font color="red">0 <= key, value <= 10^6</font>
- At most <font color="red">10^4</font> calls will be made to <font color="red">put</font>, <font color="red">get</font>, and <font color="red">remove</font>.

**Follow up:** Please do not use the built-in HashMap library.

______________________  

# Solution  

	class HTListNode {
	public:
	    int key, val;
	    HTListNode *next;
	    HTListNode(int key_, int val_): key(key_), val(val_), next(nullptr) {}
	    ~HTListNode() {}
	};

	class MyHashMap {
	public:
	    /** Initialize your data structure here. */
	    MyHashMap() {
	        for (int i=0; i<1000; ++i)
	            m_[i] = new HTListNode(-1, -1);
	    }
	    
	    /** value will always be non-negative. */
	    void put(int key, int value) {
	        int idx = mod_f(key);
	        HTListNode *prev = m_[idx];
	        HTListNode *cur = prev->next;
	        while (cur && cur->key != key) {
	            prev = cur;
	            cur = cur->next;
	        }
	        
	        if (cur != nullptr) {
	            cur->val = value;
	        } else {
	            prev->next = new HTListNode(key, value);
	        }
	    }
	    
	    /** Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key */
	    int get(int key) {
	        int idx = mod_f(key);
	        HTListNode *cur = m_[idx];
	        while (cur && cur->key != key) cur = cur->next;
	        if (cur != nullptr) return cur->val;
	        else return -1;
	    }
	    
	    /** Removes the mapping of the specified value key if this map contains a mapping for the key */
	    void remove(int key) {
	        int idx = mod_f(key);
	        HTListNode *prev = m_[idx];
	        HTListNode *cur = prev->next;
	        while (cur && cur->key != key) {
	            prev = cur;
	            cur = cur->next;
	        }
	        
	        if (cur != nullptr) {
	            prev->next = cur->next;
	            delete cur;
	        }
	    }
	    
	    int mod_f(int key) {
	        return key % 1000;
	    }
	private:
	    HTListNode *m_[1000];
	};

	/**
	 * Your MyHashMap object will be instantiated and called as such:
	 * MyHashMap* obj = new MyHashMap();
	 * obj->put(key,value);
	 * int param_2 = obj->get(key);
	 * obj->remove(key);
	 */

概念：
key -> hashing function -> idx -> linked list.  

此處 hashing function 用 mode。  
範圍鎖定在給的容器大小，這邊是 1000。  
得到 hashing 後的 idx 後，若有 collision，則用 linked list 串起來。  

初始化時的 linked list 是 dummy head。  
put, get, remove，就是 linked list 的新增、尋訪和刪除。