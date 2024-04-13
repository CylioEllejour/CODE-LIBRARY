# [小A的线段（easy version）](https://ac.nowcoder.com/acm/contest/78306/D)

## 题目描述

**本题为 easy version ，与 hard version 的区别仅为** $m$ **的数据范围。**

在一个标有 $1-n$ 的数轴上给定 $m$ 条线段，第 $i$ 个线段的左右端点分别为 $st_i$ , $ed_i$ ，求有多少种线段的选择方案可以使得数轴上的每个整数点至少被覆盖两次。

定义两种选择方案不同当且仅当至少有一个线段在两种方案中的状态（选/不选）不同。

由于方案数可能很多，所以你需要输出满足条件的方案数对 $998244353$ 取模的结果。

第一行两个正整数 $n\;(2\leq n \leq 10^5)$ 和 $m\;(1\leq m \leq10)$ ，分别表示数轴长度和线段个数。  
  
接下来 $m$ 行，每行两个正整数，其中第 $i$ 行的两个正整数 $st_i$ 和 $ed_i\;(1\leq st_i<ed_i \leq n)$ 分别表示第 $i$ 条线段的起点和终点。

输出满足条件的方案数对 $998244353$ 取模的结果。

## 解题思路

由于线段的数量$m\;(1\leq m \leq10)$不多，可以使用状态压缩来表示线段的选取情况。

对于状态是否符合条件的校验，直接暴力。

## AC代码

```C++
#include <bits/stdc++.h>

using namespace std;

const int M = 11;
const int N = 2e5 + 10;

const int mod = 998244353;

int p[M][2];

int n, m;

int st[N];

bool check(int x)
{
    int k = m ;
    for (int i = 1; i <= n; i++)
        st[i] = 0;
    int node = true;
    while (x)
    {
        if (x & 1)
        {
            for (int j = p[k][0]; j <= p[k][1]; j++)
            {
                st[j]++;
            }
        }
        k--;
        x >>= 1;
    }
    for (int i = 1; i <= n; i++)
        if (st[i] < 2)
            node = false;
    return node;
}

int main()
{
    cin >> n >> m;
    for (int i = 1; i <= m; i++)
    {
        int st, ed;
        cin >> st >> ed;
        p[i][0] = st;
        p[i][1] = ed;
    }
    int mm = 1 << m;
    int ans = 0;
    for (int i = 1; i <= mm; i++)
    {
        if (check(i))
            ans++;
        ans %= mod;
    }
    cout << ans << endl;
    return 0;
}
```
