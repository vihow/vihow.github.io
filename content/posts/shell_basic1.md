---
title: "Shell_basic1"
date: 2020-11-16T22:24:13+08:00
draft: false
---

# 自动执行的一批命令（用户级别）
- 当bash最为注册shell被启动时：自动执行~/.bash_profile
- 当bash作为注册shell退出时：自动执行~/.bash_logout
- 当bash作为交互式shell启动时：自动执行~/.bashrc

# 脚本文件
```
bash -x <.sh>: 打印每一行命令

./xx.sh:  在子进程中执行
. xx.sh  =  source xx.sh：  在当前shell进程中执行
```

## 历史与别名
### 历史表
- 先前键入的命令存于历史表 编号递增，FIFO刷新
- 表大小由变量HISTSIZE设定，该配置位于~/.bashrc
- history：查看历史命令
- !! : 引用上一命令
- !str ： 以str开头的最近使用的命令

### 别名和别名替换
- alias
- alias rm = 'rm -i'


### 输入重定向 stdin 0号文件描述符
- < file: 从file中获取输入
- << STR: 从shell中获取输入，直到再次遇到字符串STR，同时会对特殊变量进行替换，例如\`date\`，若禁止替换，使用 << 'STR'
- <<< ABCD: 获得的输入即为'ABCD'
- base64：将输入变为base64编码


### 输出重定向与管道
- > filename: stdout输出到文件（覆盖）
- >> filename: stdout输出到文件（追加）
- 2> filename: stderr输出到文件
- 2>&1 filename: 将文件句柄2重定向到文件描述符1指向的文件
```
gcc test.c > test.err > 2>&1
```

- 管道：仅把stdout进行管道， 如果需要stderr 2>&1















 
