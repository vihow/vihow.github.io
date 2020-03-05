---
layout: post
title:  "最长公共子序列"
date:   2020-03-05 13:52:07 +0800
---

> 返回字符串 s1, s2 的最长公共子序列的长度
    abc  ac    => 2

### **状态:** 
#### MaxLen(i, j) s1左部 i 个元素的子串与s2左部 j 个元素的子串的最长公共子序列
### **边界：**
#### MaxLen(i, 0) = 0, MaxLen(0, j) = 0
### **状态转移方程：** 
#### if(s1[i-1] == s2[j-1])
    MaxLen[i][j] = MaxLen[i-1][j-1] + 1;
#### else
    MaxLen[i][j] = max(MaxLen[i-1][j], MaxLen[i][j-1]);

- - -
```c++
#include <cstdio>
#include <cstring>
#include <cmath>
#include <algorithm>

using namespace std;
const int MaxN = 110;
int maxLen[MaxN][MaxN];

int main()
{
    string s1, s2;
    while(cin >> s1 >> s2)
    {
        int len1 = s1.lenght(), len2 = s2.length();
        // 初始化边界值
        for(int i = 0; i <= len1; ++i)
            maxLen[i][0] = 0;
        for(int j = 0; j <= len2; ++j)
            maxLen[0][j] = 0
        // 递推每个状态值
        for(int i = 1; i <= len1; ++i)
        {
            for(int j = 1; j <= len2; ++j)
            {
                if(s1[i-1] == s2[j-1])
                    maxLen[i][j] = maxLen[i-1][j-1]+1;
                else
                {
                    maxLen[i][j] = max(maxLen[i-1][j], maxLen[i][j-1]);
                }
            }
        }
        cout << maxLen[len1][len2] << endl;
    }
    return 0;
}
```

 