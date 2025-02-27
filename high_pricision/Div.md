# 高精度除法
## 模版

```
//高精度除以低精度
string div(string a, int b) {
    long long num = 0;
    string res;
    for (char ch : a) {
        num = num * 10 +(ch - '0');
        res.push_back(num / b + '0');
        num %= b;
    }
    reverse(res.begin(), res.end());
    while (res.size() > 1 && res.back() == '0') res.pop_back();
    reverse(res.begin(), res.end());
    return res.empty ? "0" : res;
}
```