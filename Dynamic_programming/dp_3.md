![alt text](Screenshot_20250311_080025.jpg)

先说一下，本人太懒了，所以直接盗用 题解和 deepseek 的思考过程，你如果看懂了题解，就没必要看后面 deepseek 的思考过程了。

## 题解

![alt text](Screenshot_20250311_093221.jpg)

## deepseek 的思考过程

这道题目需要我们在给定的BOSS指令序列中选择攻击方式，使得总伤害最大化。关键在于合理使用切手技攻击以触发识破效果，并管理根势的获取与消耗。

### 方法思路
1. **动态规划状态设计**：
   - 使用`dp[i][r]`表示处理到第`i`个指令时，根势为`r`（0-3）的最大伤害。
   - 状态转移分为两种情况：当前指令是`J`（BOSS攻击）或`K`（BOSS待机）。

2. **状态转移分析**：
   - **当指令为`J`时**：
     - **普通攻击**：伤害增加`a`，根势不变。
     - **切手技攻击**（需根势≥1）：触发识破，伤害增加`2*b`，根势不变。
     - **闪避**：根势增加1（不超过3），不造成伤害。
   - **当指令为`K`时**：
     - **普通攻击**：伤害增加`a`，根势不变。
     - **切手技攻击**（需根势≥1）：伤害增加`b`，根势减少1。

3. **初始化和结果提取**：
   - 初始状态为根势0，伤害0。
   - 遍历所有指令后，取所有根势状态的最大伤害作为结果。

### 解决代码
```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

void solve() {
    int n, a, b;
    string s;
    cin >> n >> a >> b >> s;

    vector<ll> prev_dp(4, LLONG_MIN);
    prev_dp[0] = 0;

    for (char c : s) {
        vector<ll> curr_dp(4, LLONG_MIN);
        for (int r = 0; r < 4; ++r) {
            if (prev_dp[r] == LLONG_MIN) continue;

            if (c == 'J') {
                // 普通攻击
                if (curr_dp[r] < prev_dp[r] + a)
                    curr_dp[r] = prev_dp[r] + a;

                // 切手技攻击
                if (r >= 1) {
                    ll damage = prev_dp[r] + 2 * b;
                    if (curr_dp[r] < damage)
                        curr_dp[r] = damage;
                }

                // 闪避
                int new_r = min(r + 1, 3);
                if (curr_dp[new_r] < prev_dp[r])
                    curr_dp[new_r] = prev_dp[r];
            } else {
                // 普通攻击
                if (curr_dp[r] < prev_dp[r] + a)
                    curr_dp[r] = prev_dp[r] + a;

                // 切手技攻击
                if (r >= 1) {
                    int new_r = r - 1;
                    ll damage = prev_dp[r] + b;
                    if (curr_dp[new_r] < damage)
                        curr_dp[new_r] = damage;
                }
            }
        }
        prev_dp = move(curr_dp);
    }

    ll ans = *max_element(prev_dp.begin(), prev_dp.end());
    cout << ans << '\n';
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int t;
    cin >> t;
    while (t--) solve();
    return 0;
}
```

### 代码解释
- **动态规划数组`prev_dp`和`curr_dp`**：分别表示当前和下一步的状态，每个状态存储4种根势对应的最大伤害。
- **指令处理**：根据当前指令类型（`J`或`K`）和当前根势状态，计算所有可能的操作对应的伤害，并更新下一步状态。
- **结果提取**：遍历所有指令后，从最终状态中找到最大伤害值输出。

该方法通过动态规划有效管理了根势状态，确保在每一步选择最优攻击策略，时间复杂度为O(n)，能够高效处理大规模输入。


![alt text](Screenshot_20250311_092227.jpg)

![alt text](Screenshot_20250311_092320.jpg)

![alt text](Screenshot_20250311_092412.jpg)

![alt text](Screenshot_20250311_092506.jpg)



