# Kruskal + LCA(倍增)

# P1967 [NOIP 2013 提高组] 货车运输

## 题目背景

NOIP2013 提高组 D1T3

## 题目描述

A 国有 $n$ 座城市，编号从 $1$ 到 $n$，城市之间有 $m$ 条双向道路。每一条道路对车辆都有重量限制，简称限重。  

现在有 $q$ 辆货车在运输货物， 司机们想知道每辆车在不超过车辆限重的情况下，最多能运多重的货物。

## 输入格式

第一行有两个用一个空格隔开的整数 $ n,m$，表示 A 国有 $ n$ 座城市和 $m$ 条道路。  

接下来 $m$ 行每行三个整数 $x, y, z$，每两个整数之间用一个空格隔开，表示从 $x $ 号城市到 $ y $ 号城市有一条限重为 $z$ 的道路。    
注意： $x \neq y$，两座城市之间可能有多条道路 。

接下来一行有一个整数 $q$，表示有 $q$ 辆货车需要运货。

接下来 $q$ 行，每行两个整数 $x,y$，之间用一个空格隔开，表示一辆货车需要从 $x$ 城市运输货物到 $y$ 城市，保证 $x \neq y$

## 输出格式

共有 $q$ 行，每行一个整数，表示对于每一辆货车，它的最大载重是多少。  
如果货车不能到达目的地，输出 $-1$。

## 输入输出样例 #1

### 输入 #1

```
4 3
1 2 4
2 3 3
3 1 1
3
1 3
1 4
1 3
```

### 输出 #1

```
3
-1
3
```

## 说明/提示

对于 $30\%$ 的数据，$1 \le n < 1000$，$1 \le m < 10,000$，$1\le q< 1000$；

对于 $60\%$ 的数据，$1 \le n < 1000$，$1 \le m < 5\times 10^4$，$1 \le q< 1000$；

对于 $100\%$ 的数据，$1 \le n < 10^4$，$1 \le m < 5\times 10^4$，$1 \le q< 3\times 10^4 $，$0 \le z \le 10^5$。

---

### 思路 

由于要让路径的权值尽量大，所以先生成最大生成树，然后再找 u， v 两个点的最近公共祖先，找祖先的同时把路径中的最小权值找到，因为在车经过整条路的时候无法超过这个最小权值。

---

*AC代码*

```
#include <iostream>
#include <algorithm>
#include <vector>
#include <climits>

using namespace std;
typedef long long LL;
const LL MAX = 5e5 + 100;

struct Edge {
    LL u, v, w;
    bool operator<(const Edge &t) const {
        return w > t.w;
    }
} edge[MAX];

struct Node {
    LL v, w;
    Node(LL v, LL w) : v(v), w(w) {}
};

LL n, m, fa[MAX], dep[MAX], f[MAX][20], q, minEdge[MAX][20], minPath, x, y;
vector<Node> node[MAX];

void init() {
    for (LL i = 1; i <= n; ++i) {
        fa[i] = i;
    }
}

LL Find(LL x) {
    return x == fa[x] ? x : fa[x] = Find(fa[x]);
}

void Union(LL x, LL y) {
    fa[Find(x)] = Find(y);
}

void Kruskal() {
    init();
    sort(edge + 1, edge + 1 + m);
    for (LL i = 1; i <= m; ++i) {
        if (Find(edge[i].u) != Find(edge[i].v)) {
            Union(edge[i].u, edge[i].v);
            node[edge[i].u].push_back(Node(edge[i].v, edge[i].w));
            node[edge[i].v].push_back(Node(edge[i].u, edge[i].w));
        }
    }
}

void dfs(LL u, LL fa, LL w) {
    dep[u] = dep[fa] + 1;
    f[u][0] = fa;
    minEdge[u][0] = w;

    for (int i = 1; i < 20; ++i) {
        if (f[u][i - 1] == 0) break;
        f[u][i] = f[f[u][i - 1]][i - 1];
        minEdge[u][i] = min(minEdge[u][i - 1], minEdge[f[u][i - 1]][i - 1]);
    }

    for (auto it : node[u]) {
        LL v = it.v, w = it.w;
        if (v != fa) dfs(v, u, w);
    }
}

LL LCA(LL u, LL v) {
    if (dep[u] < dep[v]) swap(u, v);
    minPath = LLONG_MAX;

    for (int i = 19; i >= 0; --i) {
        if (dep[f[u][i]] >= dep[v]) {
            minPath = min(minPath, minEdge[u][i]);
            u = f[u][i];
        }
    }

    if (u == v) return minPath;

    for (int i = 19; i >= 0; --i) {
        if (f[u][i] != f[v][i]) {
            minPath = min({minPath, minEdge[u][i], minEdge[v][i]});
            u = f[u][i];
            v = f[v][i];
        }
    }
    return min({minPath, minEdge[u][0], minEdge[v][0]});
}

int main() {
#ifdef JiuQi
    freopen("test.txt", "r", stdin);
#endif

    scanf("%lld %lld", &n, &m);
    for (LL i = 1; i <= m; ++i) {
        scanf("%lld %lld %lld", &edge[i].u, &edge[i].v, &edge[i].w);
    }

    Kruskal();

    for (int i = 1; i <= n; ++i) {
        if (Find(i) == i) dfs(i, 0, LLONG_MAX);
    }

    scanf("%lld", &q);
    while (q--) {
        scanf("%lld %lld", &x, &y);
        if (Find(x) == Find(y)) {
            printf("%lld\n", LCA(x, y));
        }
        else {
            printf("-1\n");
        }
    }

    return 0;
}
```