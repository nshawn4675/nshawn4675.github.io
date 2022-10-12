---
layout: post
title: "[HTB - Starting Point] Redeemer"
date: 2022-10-12 09:00:00 +0800
categories: note
tags: [HTB]
---

## Task 1  
Q : Which TCP port is open on the machine?  
``` text
[host] # nmap --open -p- -sV <target_ip> -oA Redeemer_full_scan
```
A : 6379  

## Task 2  
Q : Which service is running on the port that is open on the machine?  
A : redis  

## Task 3  
Q : What type of database is Redis? Choose from the following options: (i) In-memory Database, (ii) Traditional Database  
A :  In-memory Database  

## Task 4  
Q : Which command-line utility is used to interact with the Redis server? Enter the program name you would enter into the terminal without any arguments.  
A : redis-cli  

## Task 5  
Q : Which flag is used with the Redis command-line utility to specify the hostname?  
A : -h  

## Task 6  
Q : Once connected to a Redis server, which command is used to obtain the information and statistics about the Redis server?  
A : info  

## Task 7  
Q : What is the version of the Redis server being used on the target machine?  
A : 5.0.7  

## Task 8  
Q : Which command is used to select the desired database in Redis?  
A : select  

## Task 9  
Q : How many keys are present inside the database with index 0?  
``` text
[host] # redis-cli -h <target_ip>
<target_ip>:6379> info
```
A : 4

## Task 10  
Q : Which command is used to obtain all the keys in a database?  
A : keys *

## SUBMIT FLAG  
Q : Submit root flag  
``` text
<target_ip>:6379> keys *
<target_ip>:6379> get flag
```
A : 03e1d2b376c37ab3f5319922053953eb
