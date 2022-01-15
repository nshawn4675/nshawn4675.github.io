---
layout: post
title: "Windows10 & VirtualBox Ubuntu20.04 - shared folder"
date: 2022-01-15 15:30:00 +0800
categories: note
tags: [Windows10, VirtualBox, Ubuntu]
---

## Add a shared folder on host side.

virtualbox &rarr; your machine (powered off) &rarr; settings &rarr; Shared Folders &rarr; Add new shared folder &rarr; select "Folder Path" on win10 &rarr; enter "Folder Name" = "win10_shared" &rarr; unchecked "Read-only" and "Auto-mount".

## Install VBoxLinuxAdditions on guest side.

Turn on machine &rarr; Devices &rarr; Insert Guest Addtions CD Image...
``` console
// Mount CD
$ sudo mkdir /media/cdrom
$ sudo mount -t iso9660 /dev/cdrom /media/cdrom

// Install prerequisites
$ sudo apt-get update
$ sudo apt-get install -y build-essential linux-headers-`uname -r`

// Run installation script
$ sudo /media/cdrom/./VBoxLinuxAdditions.run

// Reboot to take effect.
$ sudo shutdown -r now
```

## Mount shared folder manually

``` console
$ mkdir ~/ubuntu_shared
$ sudo mount -t vboxsf win10_shared ~/ubuntu_shared
$ cd ~/ubuntu_shared
$ ls
```

## Mount shared folder automatically

```console
$ sudo nano /etc/fstab
// add the following line. (seperated by "tab", replace <username> with yours)
win10_shared    /home/<username>/ubuntu_shared  defaults    0   0

$ sudo nano /etc/modules
// add the following line.
vboxsf

// Reboot to take effect
$ sudo shutdown -r now

// Check shared folder is mount after boot.
$ cd ~/ubuntu_shared
$ ls

```