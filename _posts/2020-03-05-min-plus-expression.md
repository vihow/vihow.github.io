---
layout: post
title:  "最佳加法表达式"
date:   2020-03-05 19:52:07 +0800
---
有一个由1..9组成的数字串.问如果将m个加号插入到这个数字串中,在各种可能形成的表达式中，值最小的那个表达式的值是多少?

### 🤔思路
假定字符串的长度为n, 添加完加号后,表达式的最后一个加号添加在第i个数字后面,则整个问题的最优解为**min{** 前i个数字添加m-1个加号形成的表达式的最小值+第i+1到第n个数字所组成的数的值( m <= i <= n-1) **}**

#### 📕状态
前n个数添加m个加号 V( n, m )

#### 🎃状态转移方程
```
if(m == 0)
    V(n, m) = n个数字构成的整数
else if(m > n-1)
    V(n, m) = INF
else
    V(n, m) = min{ V(n-i, m-1) + Num(i+1, n) } ( m <= i <= n-1)
```

#### 💻代码实现
```c++
#include <iostream>
#include <cmath>
#include <algorithm>

using namespace std;
const int MaxN = 10;
const int INF = 2000000000;
int d[MaxN];


int Num(int left, int right);
int V(int n, int m);
int main()
{
    int n, m;
    cin >> n >> m;
    for(int i = 1; i <= n; ++i)
    {
        cin >> d[i];
    }
    cout << V(n, m);
    return 0;
}

int V(int n, int m)
{
    if( m == 0)
        return Num(1, n);   // 返回第1个数字到第n个数字组成数的值
    if( m > n-1 )
        return INF;
    int minE = INF;
    for(int i = n-1; i >= m; --i)
    {
        int E = V(i, m-1) + Num(i+1, n);
        if(E < minE)
            minE = E;
    }
    return minE;
}

int Num(int left, int right)
{
    int result = 0;
    while(left <= right)
    {
        result = result * 10 + d[left++];
    }
    return result;
}
```

