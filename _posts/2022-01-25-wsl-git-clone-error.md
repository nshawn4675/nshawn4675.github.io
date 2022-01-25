---
layout: post
title: "WSL git clone error"
date: 2022-01-25 16:00:00 +0800
categories: note
tags: [WSL, git]
---

Git clone with Ubuntu WSL, and an error occured.  
``` console
error: chmod on /mnt/d/nshawn4675.github.io/.git/config.lock failed: Operation not permitted
```

Because **/mnt/d** is a NTFS partition so that **chmod** doesn't work.  

Steps to solve this problem:  
1. Launch Ubuntu WSL
2. Create / Modify WSL conf file

    ``` console
    $ sudo vi /etc/wsl.conf
    
    [automount]
    options = "metadata"
    ```
3. Shutdown WSL with PowerShell

    ``` PowerShell
    wsl --shutdown
    ```
4. Relaunch Ubuntu WSL

[Reference](https://alessandrococco.com/2021/01/wsl-how-to-resolve-operation-not-permitted-error-on-cloning-a-git-repository)