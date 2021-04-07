---
title: "MPI_first"
date: 2021-04-07T00:15:05+08:00
draft: false
tags: ["MPI"]
---

# MPI 初探
- MPI_Init(NULL, NULL); // 两个参数保留未来使用

- MPI_COMM_WORLD    // a built-in communicator

每个进程有一个特定的rank

获取进程rank:
```
int world_rank;
MPI_Comm_Rank(MPI_COMM_WORLD, &world_rank);
```

获取总的并行进程数：
```
int world_size;
MPI_Comm_Size(MPI_COMM_WORLD, &world_size)
```

## Message sending and receiving
- 发送消息
```
MPI_Send(
    void* data,
    int count,
    MPI_Type datatype,
    int destination,
    int tag,
    MPI_Comm communicator
)
```
- 接收消息
```
MPI_Receive(
    void* data,
    int count,
    MPI_Type datatype,
    int source,
    int tag,
    MPI_Comm communicator
)
```

| task | due |
| ---- | ----|
|学习pytorch的自动求导机制|4/10|
|学习cmake和make相关知识| 4/10|
