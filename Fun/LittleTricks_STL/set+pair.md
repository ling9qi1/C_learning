![alt text](image.png)


# 仔细读题！！！  
# 认真审题！！！

## AC 代码

```
#include <iostream>
#include <algorithm>
#include <set>
#include <vector>
#include <map>
#define PII pair<int, int>
using namespace std;

int n, T;

void sovle(int T) {
    T *= 2;
    map<int, PII> mp;
    vector<int> a(T);
    set<PII> st;
    for (int i = 0; i < T; ++i) {
        cin >> a[i];
        if (mp.find(a[i]) != mp.end()) {
            mp[a[i]].second = i;
        }
        else {
            mp[a[i]].first = i;
        }
     }

     for (int i = 0; i < T - 1; ++i) {
        auto [v1, v2] = mp[a[i]];  //对于 pair<int, int> 的用法，用 [x, y] 直接被赋值
        auto [u1, u2] = mp[a[i + 1]];

        if (abs(v1 - v2) == 1 || abs(u1 - u2) == 1) continue;
        if (abs(v1 - u1) == 1 && abs(v2 - u2) == 1) st.emplace(min(a[i], a[i + 1]), max(a[i], a[i + 1]));  //用 emplace 可直接在（）内构建，如果用 st.insert()，则需在外面先构建，再传入进来，eg.PII p = {1, 2}; st.insrt(p);
     }
     cout << st.size() << endl;
}

int main() {
#ifdef JiuQi
    freopen("test.txt", "r", stdin);
#endif // JiuQi
  ios::sync_with_stdio(false);
  cin.tie(nullptr);

    cin >> n;
    for (int i = 0; i < n; ++i) {
        cin >> T;
        sovle(T);
    }
    return 0;
}
```

---


## AC 代码（官方）

```
#include <algorithm>
#include <iostream>
#include <set>
#include <utility> //这个里面含有 pair<>等模板, swap等函数
#include <vector>
using namespace std;

int main() {
  int T;
  cin >> T;
  while (T--) {
    int N;
    cin >> N;
    vector<int> A(2 * N);
    for (auto& a : A) cin >> a;  //这种用法。。。挺奇怪的

    vector<vector<int>> position(N + 1);
    for (int i = 0; i < 2 * N; i++) position[A[i]].push_back(i);

    set<pair<int, int>> answers;
    for (int i = 0; i + 1 < 2 * N; i++) {
      int a = A[i], b = A[i + 1];
      if (position[a][0] + 1 == position[a][1]) continue;
      if (position[b][0] + 1 == position[b][1]) continue;
      vector<int> v{position[a][0], position[a][1], position[b][0],
                    position[b][1]};
      sort(begin(v), end(v));
      if (v[0] + 1 == v[1] and v[2] + 1 == v[3]) {
        answers.emplace(minmax(a, b));  //这是将较小值赋给 a，将较大值赋给 b，然后以pair<int, int> 的形式（这是由于之前对于answers 的定义）存进 answeers 这个set 中
      }
    }
    cout << answers.size() << "\n";
  }
}
```