---
layout: post
title: "[LeetCode April Challange] Day 04 - Design Circular Queue"
date: 2021-04-04 00:00:00 +0800
categories: LeetCode
tags: [Medium, Array, Linked List, Design, Queue, Facebook, Amazon, Microsoft, Rubrik, Oracle, C++]
---
Design your implementation of the circular queue. The circular queue is a linear data structure in which the operations are performed based on FIFO (First In First Out) principle and the last position is connected back to the first position to make a circle. It is also called "Ring Buffer".

One of the benefits of the circular queue is that we can make use of the spaces in front of the queue. In a normal queue, once the queue becomes full, we cannot insert the next element even if there is a space in front of the queue. But using the circular queue, we can use the space to store new values.

Implementation the <font color="red">MyCircularQueue</font> class:

- **<font color="red">MyCircularQueue(k)</font>** Initializes the object with the size of the queue to be <font color="red">k</font>.
- **<font color="red">int Front()</font>** Gets the front item from the queue. If the queue is empty, return <font color="red">-1</font>.
- **<font color="red">int Rear()</font>** Gets the last item from the queue. If the queue is empty, return <font color="red">-1</font>.
- **<font color="red">boolean enQueue(int value)</font>** Inserts an element into the circular queue. Return <font color="red">true</font> if the operation is successful.
- **<font color="red">boolean deQueue()</font>** Deletes an element from the circular queue. Return <font color="red">true</font> if the operation is successful.
- **<font color="red">boolean isEmpty()</font>** Checks whether the circular queue is empty or not.
- **<font color="red">boolean isFull()</font>** Checks whether the circular queue is full or not.

# Example 1:

    Input
    ["MyCircularQueue", "enQueue", "enQueue", "enQueue", "enQueue", "Rear", "isFull", "deQueue", "enQueue", "Rear"]
    [[3], [1], [2], [3], [4], [], [], [], [4], []]
    Output
    [null, true, true, true, false, 3, true, true, true, 4]

    Explanation
    MyCircularQueue myCircularQueue = new MyCircularQueue(3);
    myCircularQueue.enQueue(1); // return True
    myCircularQueue.enQueue(2); // return True
    myCircularQueue.enQueue(3); // return True
    myCircularQueue.enQueue(4); // return False
    myCircularQueue.Rear();     // return 3
    myCircularQueue.isFull();   // return True
    myCircularQueue.deQueue();  // return True
    myCircularQueue.enQueue(4); // return True
    myCircularQueue.Rear();     // return 4

# Constraints:

- <font color="red">1 <= k <= 1000</font>
- <font color="red">0 <= value <= 1000</font>
- At most <font color="red">3000</font> calls will be made to <font color="red">enQueue, deQueue, Front, Rear, isEmpty</font>, and <font color="red">isFull</font>.

______________________  

# Solution  

# Array  

Time complexity : O(1)  
Space complexity : O(n)  

    class MyCircularQueue {
    private:
        int *q, front, cnt, capacity;
    public:
        MyCircularQueue(int k) {
            capacity = k;
            cnt = front = 0;
            q = new int[k];
        }
        
        bool enQueue(int value) {
            if (cnt == capacity) return false;
            q[(front+cnt++)%capacity] = value;
            return true;
        }
        
        bool deQueue() {
            if (cnt == 0) return false;
            front = (front+1) % capacity;
            --cnt;
            return true;
        }
        
        int Front() {
            return cnt == 0 ? -1 : q[front];
        }
        
        int Rear() {
            return cnt == 0 ? -1 : q[(front+cnt-1)%capacity];
        }
        
        bool isEmpty() {
            return cnt == 0;
        }
        
        bool isFull() {
            return cnt == capacity;
        }
    };

    /**
    * Your MyCircularQueue object will be instantiated and called as such:
    * MyCircularQueue* obj = new MyCircularQueue(k);
    * bool param_1 = obj->enQueue(value);
    * bool param_2 = obj->deQueue();
    * int param_3 = obj->Front();
    * int param_4 = obj->Rear();
    * bool param_5 = obj->isEmpty();
    * bool param_6 = obj->isFull();
    */

# Link List  

Time complexity : O(1)  
Space complexity : O(n)  

    class Node {
    public:
        int val;
        Node *next;
        Node(): val(0), next(nullptr) {}
        Node(int val_): val(val_), next(nullptr) {}
        ~Node() {}
    };

    class MyCircularQueue {
    private:
        Node *front, *rear;
        int cnt, capacity;
    public:
        MyCircularQueue(int k) {
            front = rear = nullptr;
            cnt = 0;
            capacity = k;
        }
        
        bool enQueue(int value) {
            if (cnt == capacity) return false;
            Node *curr = new Node(value);
            if (cnt == 0)
                front = rear = curr;
            else {
                rear->next = curr;
                rear = rear->next;
            }
            ++cnt;
            return true;
        }
        
        bool deQueue() {
            if (cnt == 0) return false;
            Node *curr = front;
            front = front->next;
            delete curr;
            --cnt;
            return true;
        }
        
        int Front() {
            return cnt == 0 ? -1 : front->val;
        }
        
        int Rear() {
            return cnt == 0 ? -1 : rear->val;
        }
        
        bool isEmpty() {
            return cnt == 0;
        }
        
        bool isFull() {
            return cnt == capacity;
        }
    };

    /**
    * Your MyCircularQueue object will be instantiated and called as such:
    * MyCircularQueue* obj = new MyCircularQueue(k);
    * bool param_1 = obj->enQueue(value);
    * bool param_2 = obj->deQueue();
    * int param_3 = obj->Front();
    * int param_4 = obj->Rear();
    * bool param_5 = obj->isEmpty();
    * bool param_6 = obj->isFull();
    */