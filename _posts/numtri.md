---
title: (luogu1216)Number Triangle(USACO1.5)
date: 2017-10-24 11:15:30
categories:
- solution
- dp
tags:
- dp
---

**Blog第一篇**

一道经典题。

两个方法:

## 1.自底向上推出最优解:

用dp[i][j]表示从(i,j)开始的最优解, 答案即为dp[1][1]

状态转移方程: **dp[i][j] = max(dp[i+1][j], dp[i+1][j+1]) + map[i][j]**

```cpp
#include <iostream>
using namespace std;
const int MR(1001);    //n(即题目中的r)的最大值
int map[MR][MR];    //保存输入数据
int dp[MR][MR];    //最优解
int n;
inline int dmax(const int& a,const int& b)    //返回最大值
{ return (a>b ? a : b); }
int main()
{
    cin >> n;    //输入n
    for(int i(1);i<=n;++i)
        for(int j(1);j<=i;++j)
            cin >> map[i][j];    //输入数据
    for(int i(1);i<=n;++i)    dp[n][i] = map[n][i];   //初始化，最后一行数据的最优值即为其本身
    for(int i(n-1);i>0;--i)
        for(int j(1);j<=n;++j)
        {
            dp[i][j] = map[i][j] + dmax(dp[i+1][j], dp[i+1][j+1]);    //向上递推求出最优解
        }
    cout << dp[1][1];    //输出最优解
    return 0;
}
```

## 2.自顶而下推出最优解

用dp[i][j]表示以(i,j)结束的最优解, 则最优解为最后一行中dp的最大值

状态转移方程: **dp[i][j] = max(dp[i-1][j-1],dp[i-1][j]) + map[i][j]**

```cpp
using namespace std;
const int Mn(1002);    //n的最大值(定义成1002是为了便于处理边界)
int dp[Mn][Mn];    //最优解
/*边读边求所以省去了map数组*/
int main()
{
    int n;
    cin >> n;    //输入n
    for(int i(1);i<=n;++i)
        for(int j(1);j<=i;++j)
        {
            int tn; cin >> tn;    //输入数据
            dp[i][j] = max(dp[i-1][j-1],dp[i-1][j]) + tn;    //求解最优解
        }
    int max(0);
    for(int i(1);i<=n;++i)
    if(dp[n][i] > max) max = dp[n][i];    //寻找最优解
    cout << max;    //输出最优解
    return 0;
}
```
可以边读边求解, 但最优解表示较麻烦
