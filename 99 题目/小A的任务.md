# 小A的任务

## 题目描述

小A现在需要完成有序的 $A$ 类任务和 $B$ 类任务各 $n$ 个，初始时只有第 $1$ 个 $A$ 类任务可以进行。进行第 $i$ 个 $A$ 类任务需在完成第 $i - 1$ 个 $A$ 类任务之后，进行第 $i$ 个 $B$ 类任务需要在完成第 $i$ 个 $A$ 类任务之后。且在同一时刻只能进行 $A$ 类和 $B$ 类中的一类任务，同一类的任务只能同时进行一个，任何一个任务都至多完成一次。  
  
总共有 $q$ 次询问，每次询问你需要回答完成 $k$ 个 $B$ 类任务至少需要多长时间。

第一行两个整数 $n\;(1\leq n \leq 10^5)$ 和 $q\;(1\leq q \leq 100)$ ，分别表示任务个数与询问次数。  
  
第二行 $n$ 个整数，其中第 $i$ 个数字 $a_i\;(1\leq a_i \leq 10^9)$ 表示完成第 $i$ 个 $A$ 类任务所需要的时间。  
  
第三行 $n$ 个整数，其中第 $i$ 个数字 $b_i\;(1\leq b_i \leq 10^9)$ 表示完成第 $i$ 个 $B$ 类任务所需要的时间。  
  
接下来 $q$ 行，每行一个整数 $k\;(1\leq k \leq n)$ ，表示询问。

对于每次询问，输出一行一个整数，表示询问结果。

## 解题思路

由于完成$k$个$B$类任务至少需要完全$k$个$A$类任务，最坏情况需要完成所以所有$A$类任务。

可以构建一个大根堆，存入前$k$个任务，然后向后遍历，对比堆顶小的进行更新入堆并将原有的堆顶弹出，同时也更新堆中的$B$类任务耗时和。与对应的$A$类任务耗时相加，得到总耗时，如果比答案小，就更新答案，得到最小答案。

## AC代码

```C++
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5 + 10;

typedef pair<int, int> PII;

int a[N];
int b[N];
long long suma[N];

int main()
{
    int n, t;
    cin >> n >> t;
    for (int i = 1; i <= n; i++)
    {
        cin >> a[i];
        suma[i] = suma[i - 1] + a[i];
    }

    for (int i = 1; i <= n; i++)
    {
        cin >> b[i];
    }

    while (t--)
    {
        int k;
        cin >> k;
        priority_queue<int> q;
        long long res = 0;
        for (int i = 1; i <= k; i++)
        {
            q.push(b[i]);
            res += b[i];
        }
        long long ans = res + suma[k];
        for (int i = k + 1; i <= n; i++)
        {
            long long cnt = suma[i];
            if(b[i]<q.top())
            {
                res -= q.top();
                q.pop();
                q.push(b[i]);
                res += b[i];
                ans = min(ans,res + cnt);
            }
        }
        cout << ans << endl;
    }
    return 0;
}
```