---
layout: post
title:  "[LeetCode August Challange]Day2-Design HashSet"
date:   2020-08-02 00:00:00 +0800
categories: LeetCode
tags: [Array, Hash Table, Linked List, Design, Hash Function, C++]
---
Design a HashSet without using any built-in hash table libraries.  

To be specific, your design should include these functions:  

- **add(value)**: Insert a value into the HashSet. 
- **contains(value)**: Return whether the value exists in the HashSet or not.
- **remove(value)**: Remove a value in the HashSet. If the value does not exist in the HashSet, do nothing.

# Example:  
	MyHashSet hashSet = new MyHashSet();
	hashSet.add(1);         
	hashSet.add(2);         
	hashSet.contains(1);    // returns true
	hashSet.contains(3);    // returns false (not found)
	hashSet.add(2);          
	hashSet.contains(2);    // returns true
	hashSet.remove(2);          
	hashSet.contains(2);    // returns false (already removed)

# Note:  
- All values will be in the range of **[0, 1000000]**.
- The number of operations will be in the range of **[1, 10000]**.
- Please do not use the built-in HashSet library.

______________________  

# solution

	class MyHashSet {
	public:
	    /** Initialize your data structure here. */
	    MyHashSet() {
	        content = vector<bool>(1000001, false);
	    }
	    
	    void add(int key) {
	        content[key] = true;
	    }
	    
	    void remove(int key) {
	        content[key] = false;
	    }
	    
	    /** Returns true if this set contains the specified element */
	    bool contains(int key) {
	        return content[key];
	    }
	private:
	    vector<bool> content;
	};

	/**
	 * Your MyHashSet object will be instantiated and called as such:
	 * MyHashSet* obj = new MyHashSet();
	 * obj->add(key);
	 * obj->remove(key);
	 * bool param_3 = obj->contains(key);
	 */

Hash table的概念圖：  
![](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/hashset.png?raw=true)

理論上輸入(key, value)，key經過hash function之後，會去存取相對應index的內容。  
table得看需求設計大小，或是進階一點，動態大小。  
(index, content) pair 後面的content也可延伸為linked list。  

按照此題需求，index範圍是[0, 1000000]，也只需知道此數值是否有存起來，因此hash function f(x) = x，content 就存有沒有存入此數值即可。  