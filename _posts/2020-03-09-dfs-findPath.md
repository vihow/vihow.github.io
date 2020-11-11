---
layout: post
titile: The Application Of Depth First Search
---

### 🌳在图中搜索能否从某点走到终点
```c++
bool Dfs(V) // 从V点开始深搜
{
    if(V是终点)
        return true;
    将V标记为已访问；
    for(V的每个未被访问的邻接点X)
    {
        if(Dfs(X))
            return true;
    }
    return false;   // V的任意邻接点都无法达到终点，即V也无法达到终点。
}
```

### 🎋记录从起点到终点的路径

使用**path[]**数组保存当前走过的路径，**depth**表示当前访问结点的深度

```c++
Node path[MaxN];
int depth;

bool Dfs(V)
{
    if(V为终点){
        path[depth] = V;
        return true;
    }
    将V标记为已访问；
    // 将该结点暂时加入路径中
    depth++;
    path[depth] = V;

    对所有和V相邻的未被访问的结点U{
        if(Dfs(U))
            return true;
    }

    // V的所有邻接点都无法访问到终点，则V不应出现在路径中
    --depth;
    return false;
}

int main()
{
    将所有点都标记为未访问；
    depth = 0;
    if(Dfs(起点))
    {
        for(int i = 0; i <= depth; ++depth)
            cout << path[i] << endl;
    }
    reutrn 0;
}

```

### 🎍利用DFS遍历一个图
```c++
void Dfs(V)
{
    将V标记为已访问;
    for(V所有未访问的邻接点U){
        Dfs(U);
    }
}

int main()
{
    将所有结点初始化为未访问
    while(图中还有未访问结点K)
        Dfs(K);
}
```

🌈🌈🌈🌈🌈🌈🌈