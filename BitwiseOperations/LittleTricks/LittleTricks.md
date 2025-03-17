# 快速判断一个数是否是 2 的幂

## 方法一

```
#deinfe lowbit(x) x & (-x)

bool towPower(int x) {
    if (lowbit(x) == x) return true;
    return false;
}
```


## 方法二

```
bool towPower(int x) {
    if ((x & (x - 1)) == 0) {
        return true;
    }
    return false;
}