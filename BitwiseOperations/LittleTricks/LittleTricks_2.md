- 相对运动

- 对于数值很大的数组储存

$vis[x][y]$ $(1 <= x <= 2e5,$  $1 <= y <= 2e5)$  
等价于，不对，下面的更好，不会爆栈   
$map<pair<LL, LL>, LL>  vis;$


![alt text](02cb5e0f7ceee3257910465866fc9239.png)


## AC代码

```
#include <bits/stdc++.h>
using namespace std;
typedef long long LL;
const LL MAX = 2e5 + 100;

LL n, x, y;
string str;
map<pair<LL, LL>, LL> vis;

int main() {
#ifdef JiuQi
    freopen("test.txt", "r", stdin);
#endif
    ios::sync_with_stdio(false);
    cin.tie(0), cout.tie(0);

	cin >> n >> x >> y >> str;
	
	x = x + MAX;
	y = y + MAX;
	int a = MAX, b = MAX;
	vis[{a, b}] = 1;
	for (int i = 0; i < n; ++i) {
		if (str[i] == 'N') {
			++a, ++x;
			vis[{a, b}] = 1;
			
		}
		else if (str[i] == 'S') {
			--a, --x;
			vis[{a, b}] = 1;
		}
		else if (str[i] == 'W') {
			++b, ++y;
			vis[{a, b}] = 1;
		}
		else {
			--b, --y;
			vis[{a, b}] = 1;
		}
		if (vis[{x, y}]) {
			cout << 1;
		}
		else {
			cout << 0;
		}
	}
    return 0;
}
```
