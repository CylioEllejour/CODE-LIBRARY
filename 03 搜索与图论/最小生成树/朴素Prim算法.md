# 朴素版prim算法 —— 模板题 [AcWing 858. Prim算法求最小生成树](https://www.acwing.com/problem/content/860/)

## 时间复杂度是 $O(n^2+m)$, $n$ 表示点数，$m$ 表示边数

```cpp
int n;      // n表示点数
int g[N][N];        // 邻接矩阵，存储所有边
int dist[N];        // 存储其他点到当前最小生成树的距离
bool st[N];     // 存储每个点是否已经在生成树中

// 如果图不连通，则返回INF(值是0x3f3f3f3f), 否则返回最小生成树的树边权重之和
int prim()
{
    memset(dist, 0x3f, sizeof dist);

    int res = 0;
    for (int i = 0; i < n; i ++ )
    {
        int t = -1;
        for (int j = 1; j <= n; j ++ ) // 寻找集合外最小的一点
            if (!st[j] && (t == -1 || dist[t] > dist[j]))
                t = j;

        if (i && dist[t] == INF) return INF;  // 对不连通图的判断

        if (i) res += dist[t];
        st[t] = true;

        // 注意：此处处与Dijkstra的区别，此处表示用该点更新其他集合外的点到集合的距离
        for (int j = 1; j <= n; j ++ ) dist[j] = min(dist[j], g[t][j]); 
    }

    return res;
}
```
