---
layout: post
title: Skating Problem
---
Michael喜欢滑雪百这并不奇怪，因为滑雪的确很刺激。可是为了获得速度，滑的区域必须向下倾斜，而且当你滑到坡底，你不得不再次走上坡或者等待升降机来载你。Michael想知道载一个区域中最长的滑坡。<br><br>区域由一个二维数组给出。数组的每个数字代表点的高度。下面是一个例子<br>

    1  2  3  4  5
    16 17 18 19 6
    15 24 25 20 7
    14 23 22 21 8
    13 12 11 10 9

一个人可以从某个点滑向**上下左右**相邻四个点之一，当且仅当高度减小。<br>在上面的例子中，一条可滑行的滑坡为24-17-16-1。当然25-24-23-...-3-2-1更长。事实上，这是最长的一条。<br><br>输入输入的第一行表示区域的行数R和列数C(1 <= R,C <= 100)。下面是R行，每行有C个整数，代表高度h，0<=h<=10000。输出输出最长区域的长度。

**样例输入**

    5 5 
    1  2  3  4  5 
    16 17 18 19 6
    15 24 25 20 7
    14 23 22 21 8
    13 12 11 10 9

**样例输出**
    
    25


### 🔥状态
    L(i, j): 在坐标（i, j）处可达到的最长长度

### ❄状态转移方程
    如果（i，j）周围点均高于（i，j）, 则L(i, j) = 1;
    否则 L(i, j) = max { V( (i,j)周围较低点 ) } + 1

### 🐟解法一. “人人为我”递推型

将所有坐标（i, j）按高度排序, 全部初始化为L(i, j) = 1
<br> 从最低点开始遍历， 每经过一个点(i, j)用递推方程更新该点L值

### 🌠解法二. "我为人人"递推型

将所有坐标（i, j）按高度排序, 全部初始化为L(i, j) = 1
<br> 从最低点开始遍历， 每经过一个点(i, j)，更新周围比其更高点的L值。
    
    例如：if( H(i+1,j) > H(i,j) )
    {
        L(i+1,j) = max{ L(i+1, j), L(i, j) + 1}; 
    }

### 💻 代码实现
```c++
#include <iostream>
#include <cmath>
#include <algorithm>

using namespace std;

const int MaxN = 10010;
int height[MaxN][MaxN];
int L[MaxN][MaxN];

struct Loc{
    int i;
    int j;
    int height;
}loc[MaxN*MaxN];

struct cmp{
    bool operator() (const struct Loc &loc1, const struct Loc &loc2) const {
        return loc1.height < loc2.height;
    }
};

bool IsLower(int i, int j, int h);

int r, c;
int main()
{
    cin >> r >> c;  // 行数与列数
    int k = 1;
    int h;
    for(int i = 1; i <= r; ++i)
    {
        for(int j = 1; j <= c; ++j)
        {  
            cin >> h;
            height[i][j] = h;
            L[i][j] = 1;
            loc[k].i = i;
            loc[k].j = j;
            loc[k].height = h;
            ++k;
        }
    }

    // 将loc数组根据height从低到高排序
    sort(loc+1, loc+k, cmp());
    // 遍历所有坐标
    for(int cnt = 2; cnt < k; ++cnt)
    {
        int i = loc[cnt].i;
        int j = loc[cnt].j;
        int h = loc[cnt].height;
        // 该点相邻点
        int i1 = i+1, j1 = j;   // 下方坐标
        int i2 = i-1, j2 = j;   // 上方坐标
        int i3 = i, j3 = j-1;   // 左方坐标
        int i4 = i, j4 = j+1;   // 右方坐标
        int l1 = 0, l2 = 0, l3 = 0, l4 = 0;
        if(IsLower(i1, j1, h))
            l1 = L[i1][j1];
        if(IsLower(i2, j2, h))
            l2 = L[i2][j2];
        if(IsLower(i3, j3, h)) 
            l3 = L[i3][j3];
        if(IsLower(i4, j4, h))
            l4 = L[i4][j4];

        if(l1==0 && l2==0 && l3==0 && l4==0)    // 周围点均高于（i，j）
            L[i][j] = 1;
        else
        {
            L[i][j] = max(max(l1, l2), max(l3, l4)) + 1; 
        }

    }
    // cout << *max_element(L+r+1, L+r+1+r*c);
    int maxL = 0;
    for(int i = 1; i <= r; ++i)
    {
        for(int j = 1; j <= c; ++j)
        {
            if(L[i][j] > maxL)
                maxL = L[i][j];
        }
    }
    cout << maxL;
    return 0;
}

bool IsLower(int i, int j, int h)
{
    if(i < 1 || i > r || j < 1 || j > c)
        return false;   // 超出边界
    return height[i][j] < h;
}
```
<br><br><br>
🌈🌈🌈🌈🌈🌈🌈🌈🌈






