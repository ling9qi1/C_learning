## 题目大意

给你一个 $events$ 数组，其中 $events[i] = [startDay[i], endDay[i], value[i]$ ，表示第 $i$ 个会议在 $startDay[i]$ 天开始，第 $endDay[i]$ 天结束，如果你参加这个会议，你能得到价值 $value[i]$ 。同时给你一个整数 $k$ 表示你能参加的最多会议数目。  
你同一时间只能参加一个会议，但你能同时参加一个开始日期与另一个结束日期相同的两个会议。  
请你返回能得到的会议价值最大和，同时将会议的下标按时间顺序输出。


- 先思考没有 $k$ 和按时间顺序输出的限制，代码如下

```
#include <iostream>
#include <algorithm>

using namespace std;
typedef long long LL;
const int MAX = 1e6 + 100;

struct Node {
    int u, v, w;
} node[MAX];

bool cmp(const Node &a, const Node &b) {
    if (a.v != b.v) return a.v < b.v;
    else return a.u < b.u;
}

bool check(int x, int y) {
    return node[x].v <= node[y].u;
}

int prev(int x) {
    int l = -1, r = x - 1;
    while (l + 1 != r) {
        int mid = (l + r) / 2;
        if (check(mid, x)) {
            l = mid;
        }
        else {
            r = mid;
        }
    }
    return l;
}
int n, dp[MAX];


int main() {
#ifdef JiuQi
    freopen("text.txt", "r", stdin);
#endif // JiuQi
    ios::sync_with_stdio(false);
    cin.tie(0), cout.tie(0);

    cin >> n;

    sort(node + 1, node + n + 1, cmp);

    for (int i = 1; i <= n; ++i) {
        cin >> node[i].u >> node[i].v >> node[i].w;
    }

    for (int i = 1; i <= n; ++i) {
        dp[i] = max(dp[i - 1], dp[prev(i)] + node[i].w);
    }
    cout << dp[n] << endl;

    return 0;
}
```