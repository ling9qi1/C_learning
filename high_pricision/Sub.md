# 高精度减法
## 模板

先说思路，先判断a, b两个数的相对大小，如果a < b, 则需要加上负号，麻烦的是借位和处理前导零。

```
string sub(string a, string b) {
    //先判断a, b 的相对大小，来确定是否需要加上'-'
    bool flag = false;
    if (a.size() < b.size() || a.size() == b.size() && a < b) {
        swap(a, b);
        flag = true;
    }
    //反转字符串，方便做减法运算
    reverse(a.begin(), a.end());
    reverse(b.begin(), b.end());
    
    int borr = 0;  //设置出保存借位的变量
    string res;
    //模拟减法过程
    for (int i = 0; i < a.size(); ++i) {
        int numA = a[i] - '0' - borr;
        int numB = i < b.size() ? b[i] - '0' : 0;
        borr = 0;  //不要忘记把借位重置为0
        
        if (numA < numB) {
            numA += 10;
            borr = 1;
        }
        res.push_back(numA - numB + '0');
    }
    //处理前导零，但是不要把单个的0给处理掉
    while (res.size() > 1 && res.back() == '0') {
        res.pop_back();
    }
    if (flag) res.push_back('-');
    reverse(res.begin(), res.end());
    return res;
}
```