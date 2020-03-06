---
layout: post
title: The Linux Kernel Introduction
date: 2020-03-06 09:20
---
### Linux Features
* UNIX-like operating syste.
* Features:
    * Preemptive multitasking.
    * Virtual memory.
    * Shared libraries.
    * Demand loading, dynamic kernel modules.
    * Shared copy-on-write executables.
    * TCP/IP networking.
    * SMP(Symmetrical Multi-Processing) support.
    * Open source.

### Two Modes within Linux
* User mode
    * Application software
    * libraries
* Kernel mode
    * System calls
    * **Linux Kernel**(device drives, process-scheduler, networking stack, file systems)
    * Linux Security Modules
    * Hardware

### Linux Source Tree
* bin - Commands needed during booting up that might be needed by normal users
* sbin - Like bin but commands are not intended for nomal users. Commands run by LINUX
* proc
    * A directory with info about process number
    * Each process has a directory below proc.
* usr - Contains all commands, libraries, man pages, games and static files for normal operation
* boot - Files used by the bootstrap loader. Kernel images are often kept here.
* lib - Shared libraries needed by the programs on the root filesystem.
* etc - Configuration files specific to the machine
* var - Contains files that change for mail, news, printers log files, man pages, temp files

### Summary
* Linux is a modular, UNIX-like monolithic kernel.
* Kernel is the heart of the OS that executes with special hardware permission(kernel mode)
* "Core kernel" provides framework, data structures, support for drivers, modules, subsystems.
* Architecture dependent source sub-trees live in /arch.

### 操作系统启动过程
1. BIOS读入操作系统的第一个扇区bootsect.s文件,然后执行bootsect.s文件<br>
2. bootsect.s继续读入操作系统的setup.s文件,将来交给setup.s执行,在其中会完成一些操作系统摄制工作<br>
3. 接下来 bootsect.s读入操作系统的主体模块system, setup.s执行完成后会执行system