---
layout: post
titile: Catch That Cow
---
Farmer John has been informed of the location of a fugitive cow and wants to catch her immediately. He starts at a point N (0 ≤ N ≤ 100,000) on a number line and the cow is at a point K (0 ≤ K ≤ 100,000) on the same number line. Farmer John has two modes of transportation: walking and teleporting.

* Walking: FJ can move from any point X to the points X - 1 or X + 1 in a single minute
* Teleporting: FJ can move from any point X to the point 2 × X in a single minute.
<br>
If the cow, unaware of its pursuit, does not move at all, how long does it take for Farmer John to retrieve it?

### 🔥图的广度搜索
* 将源点放入队列q中，并标记为已访问
* 当q非空时循环
    * 从队首取出结点x
    * 考察x是否是目标节点，若是，return
    * 否则，考察x的未访问的邻接点y
        * 存储y的路径上父节点指针*x及该节点层次，将y入队
* 广搜成功结束，根据目标节点v的父节点指针一步步倒查，可以找到该路径，目标节点的层次即为路径长度。

### 🎈该题不需要求路径
    struct Step{
        int x;  // 位置（相当于结点编号）
        int step;   // 从源点到达该结点的步数（相当于层数）
    }

### 💻代码实现
```c++
#define LOCAL
#include <iostream>
#include <cstring>
#include <cmath>
#include <algorithm>
#include <queue>

using namespace std;
const int MaxV = 100000;
int visited[MaxV+10];

struct Step
{
    int x;  // 位置
    int steps;  // 到达x所走的步数（层数）
    Step(int _x, int _steps):x(_x),steps(_steps) {};
};

queue<Step> q;
int main()
{
    int N, K;   // 农夫位置，牛的位置
    cin >> N >> K;
    memset(visited, 0, sizeof(visited));
    q.push(Step(N, 0));
    visited[N] = 1;

    while(!q.empty())
    {
        Step tmp = q.front();
        int x = tmp.x;
        int steps = tmp.steps;
        if(x == K)  // 找到目标
        {
            cout << steps << endl;
            return 0;
        }
        else
        {
            q.pop();
            if(x+1 <= MaxV && !visited[x+1])
            {
                q.push(Step(x+1, steps+1));
                visited[x+1] = 1;
            }
            if(x-1 >= 0 && !visited[x-1])
            {
               q.push(Step(x-1, steps+1));
               visited[x-1] = 1;
            }
            if(2*x <= MaxV && !visited[2*x])
            {
                q.push(Step(2*x, steps+1));
                visited[2*x] = 1;
            }
        }
    }
    return 0;
}
```

🌈🌈🌈🌈🌈🌈🌈