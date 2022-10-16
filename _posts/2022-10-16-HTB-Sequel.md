---
layout: post
title: "[HTB - Starting Point] Sequel"
date: 2022-10-16 09:00:00 +0800
categories: note
tags: [HTB]
---

## Task 1  
Q : What does the acronym SQL stand for?  
A : Structured Query Language  

## Task 2  
Q : During our scan, which port running mysql do we find?  
``` text
[host] # nmap -sVC --open -oA Sequel_init_scan <target_ip>
```
A : 3306  

## Task 3  
Q : What community-developed MySQL version is the target running?  
A : MariaDB  

## Task 4  
Q : What switch do we need to use in order to specify a login username for the MySQL service?  
A : -u  

## Task 5  
Q : Which username allows us to log into MariaDB without providing a password?  
A : root  

## Task 6  
Q : What symbol can we use to specify within the query that we want to display everything inside a table?  
A : *  

## Task 7  
Q : What symbol do we need to end each query with?  
A : ;  

## SUBMIT FLAG  
Q : Submit root flag  
``` text
[host] # mariadb -u root -P 3306 -h <target_ip>
MariaDB [(none)]> SHOW DATABASES;
MariaDB [(none)]> USE htb;
MariaDB [htb]> SHOW TABLES;
MariaDB [htb]> SELECT * FROM config;
```
A : 7b4bec00d1a39e3dd4e021ec3d915da8
