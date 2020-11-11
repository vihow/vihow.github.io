---
layout: post
title: learn to use make
date: 2020-03-06 22:00
---
> * makefile 文件帮助我们记录了整个项目工程的所有需要编译的文件列表。 
> * makefile 文件反映了整个项目中各个模块的依赖关系。

## about makefile
### 🍎What is makefile?
makefile 就是一个简单的文本文件，它基本上就是由一条条的**规则**构成<br>
    
    target: prerequisites
    <tab> command1
    <tab> command2
    .....
    <tab> commandN

* target: 规则的目标，可以简单理解为这条规则存在的目的，通常是程序中间或最后需要生成的文件名。
* prerequisites: 规则的依赖列表，可以简单的理解为要达到本条规则的目标所需要的先决条件。可以是文件名，也可以是其他规则的目标。
* command: 规则的命令，当目标所需的先决条件满足后，需要执行的动作----shell命令。一条规则中可以有多行命令，以tab键开始。

### 📕How does it work?

make命令的基本使用范式：

    make [-f makefile] [options] ... [targets]

1. 不带任何参数，直接执行make,make就会在当前目录下依次查找名字GNUmakefile, makefile,和 Makefile的文件来作为其makefile文件

        make

2. 指定makefile文件：

        make -f <makefile_name>

3. 指定makefile目标: ( 以参数的形式指定终极目标，从而执行作为突破口的规则，如果我们不显式指定终极目标，make一般情况下将选择makefile的第一条规则的目标作为终极目标。)
    
        make <target>

4. 到指定目录下执行make:
    
        make -C <subdir> <target>
