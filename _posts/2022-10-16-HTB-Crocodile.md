---
layout: post
title: "[HTB - Starting Point] Crocodile"
date: 2022-10-16 09:00:00 +0800
categories: note
tags: [HTB]
---

## Task 1  
Q : What nmap scanning switch employs the use of default scripts during a scan?  
A : -sC  

## Task 2  
Q : What service version is found to be running on port 21?  
``` text
[host] # nmap -sCV --open -oA Crocodile_init_scan <target_ip>
```
A : vsftpd 3.0.3  

## Task 3  
Q : What FTP code is returned to us for the "Anonymous FTP login allowed" message?  
``` text
[host] # ftp anonymous@<target_ip>
```
A : 230  

## Task 4  
Q : What command can we use to download the files we find on the FTP server?  
A : get  

## Task 5  
Q : What is one of the higher-privilege sounding usernames in the list we retrieved?  
``` text
ftp> ls
ftp> get allowed.userlist
ftp> get allowed.userlist.passwd
ftp> exit
[host] # cat allowed.userlist
```
A : admin  

## Task 6  
Q : What version of Apache HTTP Server is running on the target host?  
A : 2.4.41  

## Task 7  
Q : What is the name of a handy web site analysis plug-in we can install in our browser?  
A : wappalyzer  

## Task 8  
Q : What switch can we use with gobuster to specify we are looking for specific filetypes?  
A : -x  

## Task 9  
Q : What file have we found that can provide us a foothold on the target?  
``` text
[host] # gobuster dir -u 10.129.253.200 -w /usr/share/seclists/Discovery/Web-Content/common.txt -x php
```
A : login.php

## SUBMIT FLAG  
Q : Submit root flag  
``` text
1. go to <target_ip>/login.php
2. Enter admin account and password found in allowed.userlist and allowed.userlist.passwd.
```
A : c7110277ac44d78b6a9fff2232434d16
