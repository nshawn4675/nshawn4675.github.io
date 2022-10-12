---
layout: post
title: "[HTB - Starting Point] Dancing"
date: 2022-10-12 09:00:00 +0800
categories: note
tags: [HTB]
---

## Task 1  
Q : What does the 3-letter acronym SMB stand for?  
A : Server Message Block  

## Task 2  
Q : What port does SMB use to operate at?  
A : 445  

## Task 3  
Q : What is the service name for port 445 that came up in our Nmap scan? 
``` text
[host] # nmap -sV --open <target_ip> -oA Dancing_init_scan
``` 
A : microsoft-ds  

## Task 4  
Q : What is the 'flag' or 'switch' we can use with the SMB tool to 'list' the contents of the share?  
A : -l  

## Task 5  
Q : How many shares are there on Dancing?  
``` text
[host] # smbclient -L <target_ip>
```  
A : 4

## Task 6  
Q : What is the name of the share we are able to access in the end with a blank password?  
A : WorkShares  

## Task 7  
Q : What is the command we can use within the SMB shell to download the files we find?  
A : get  

## SUBMIT FLAG
Q : Submit root flag  
``` text
[host] # smbclient \\\\<target_ip>\\WorkShares
smb: \> ls
smb: \> cd James.P
smb: \> get flag.txt
smb: \> exit
[host] # cat flag.txt
```
A : 5f61c10dffbc77a704d76016a22f1664

