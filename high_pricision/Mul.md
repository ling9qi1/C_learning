# 高精度乘法
## 模版

```
string mul(string a, string b) {
    if (a == "0" || b == "0") return "0";
    
    reverse(a.begin(), a.end());
    reverse(b.begin(), b,end());
    
    vector<int> tmp(a.size() + b.size(), 0);
    for (int i = 0; i < a; ++i) {
        for (int j = 0; j < b; j++) {
            tmp[i + j] += (a[i] - '0') * (b[j] - '0');
        }
    }
    
    string res;
    int temp = 0;
    for (int num : tmp) {
        num += temp;
        res.push_back(num % 10 + '0');
        temp = num / 10;
    }
    
    while(temp) {
        res.push_back(temp % 10 + '0');
        temp /= 10;
    }
    
    while (res.size() > 1 && res.back() == '0') res.pop_back();
    reverse(res.begin(), res.end());
    return res;
}
```