---
layout: post
title: "Enlarge swap space"
date: 2022-01-20 19:00:00 +0800
categories: note
tags: [Linux, Ubuntu]
---

## Enlarge swap space to 16GB

```console
$ sudo swapoff /swapfile
$ sudo rm /swapfile
$ sudo dd if=/dev/zero of=/swapfile bs=1M count=16384
$ sudo chmod 600 /swapfile
$ sudo mkswap /swapfile
$ sudo swapon /swapfile

// check swap
$ cat /proc/swaps
```