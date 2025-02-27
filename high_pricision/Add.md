# 高精度加法
## 模板

```
string add(string a, string b) {
    int temp = 0;
    string res;

    reverse(a.begin(), a.end());
    reverse(b.begin(), b.end());

    for (int i = 0; i < a.size() || i < b.size() || temp; ++i) {
        if (i < a.size()) temp += a[i] - '0';
        if (i < b.size()) temp += b[i] - '0';
        res.push_back(temp % 10 + '0');
        temp /= 10;
    }
    reverse(res.begin(), res.end());
    return res;
}
```
