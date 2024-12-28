# dfs 深度优先搜索
### 题目
[与或异或-蓝桥杯](https://www.lanqiao.cn/problems/3552/learning/)

### AC代码

```
#include <iostream>
using namespace std;
int ans = 0, a[6][10] = {{},{0, 1, 0, 1, 0, 1}};
void dfs(int r, int j, int k) {
    if(k == 0) 
        a[r][j] = a[r - 1][j] | a[r - 1][j + 1];
    else if(k == 1) 
        a[r][j] = a[r - 1][j] & a[r - 1][j + 1]; 
    else if(k == 2)
        a[r][j] = a[r - 1][j] ^ a[r - 1][j + 1]; 
    if(r == 5 && j == 1) { 
        if(a[r][j] == 1) ans++; 
        return; 
    }
    if(r + j == 6) r++, j = 1;
    else j++; 
    for(int s = 0; s < 3; s++) 
        dfs(r, j, s);
}
int main() {
    for(int k = 0; k < 3; k++) 
        dfs(2, 1, k);
    cout << ans << endl; 
    return 0;  
}
```

### 代码逻辑呈现
```
dfs(2, 1, 0) r = 2, j = 1, k = 0;
    if(k == 0) 
        a[2][1] = a[1][1] | a[1][2];
    else if(k == 1) 
        a[2][1] = a[1][1] & a[1][2];
    else if(k == 2)
        a[2][1] = a[1][1] ^ a[1][2];
    if(r == 5 && j == 1) { 
        if(a[r][j] == 1) ans++; 
        return; 
    }
    if(r + j == 6) r++, j = 1;
    else j++; //j = 2
    for(int s = 0; s < 3; s++) 
        dfs(r, j, s);//dfs(2, 2, 0)
        
dfs(2, 2, 0) r = 2, j = 2, k = 0;
    if(k == 0) 
        a[2][2] = a[1][2] | a[1][3];
    else if(k == 1) 
        a[2][1] = a[1][1] & a[1][2];
    else if(k == 2)
        a[2][1] = a[1][1] ^ a[1][2];
    if(r == 5 && j == 1) { 
        if(a[r][j] == 1) ans++; 
        return; 
    }
    if(r + j == 6) r++, j = 1;
    else j++; //j = 3
    for(int s = 0; s < 3; s++) 
        dfs(r, j, s);//dfs(2, 3, 0)
        
dfs(2, 3, 0) r = 2, j = 3, k = 0;
    if(k == 0) 
        a[2][3] = a[1][3] | a[1][4];
    else if(k == 1) 
        a[2][1] = a[1][1] & a[1][2];
    else if(k == 2)
        a[2][1] = a[1][1] ^ a[1][2];
    if(r == 5 && j == 1) { 
        if(a[r][j] == 1) ans++; 
        return; 
    }
    if(r + j == 6) r++, j = 1;
    else j++; //j = 4
    for(int s = 0; s < 3; s++) 
        dfs(r, j, s);//dfs(2, 4, 0)
        
dfs(2, 4, 0) r = 2, j = 4, k = 0;
    if(k == 0) 
        a[2][4] = a[1][4] | a[1][5];
    else if(k == 1) 
        a[2][1] = a[1][1] & a[1][2];
    else if(k == 2)
        a[2][1] = a[1][1] ^ a[1][2];
    if(r == 5 && j == 1) { 
        if(a[r][j] == 1) ans++; 
        return; 
    }
    if(r + j == 6) r++, j = 1;//r = 3, j = 1
    else j++; 
    for(int s = 0; s < 3; s++) 
        dfs(r, j, s);//dfs(3, 1, 0)
        
dfs(3, 1, 0) r = 3, j = 1, k = 0;
    if(k == 0) 
        a[3][1] = a[2][1] | a[2][2];
    else if(k == 1) 
        a[2][1] = a[1][1] & a[1][2];
    else if(k == 2)
        a[2][1] = a[1][1] ^ a[1][2];
    if(r == 5 && j == 1) { 
        if(a[r][j] == 1) ans++; 
        return; 
    }
    if(r + j == 6) r++, j = 1;
    else j++; //j = 2
    for(int s = 0; s < 3; s++) 
        dfs(r, j, s);//dfs(3, 2, 0)
        
dfs(3, 2, 0) r = 3, j = 2, k = 0;
    if(k == 0) 
        a[3][2] = a[2][2] | a[2][3];
    else if(k == 1) 
        a[2][1] = a[1][1] & a[1][2];
    else if(k == 2)
        a[2][1] = a[1][1] ^ a[1][2];
    if(r == 5 && j == 1) { 
        if(a[r][j] == 1) ans++; 
        return; 
    }
    if(r + j == 6) r++, j = 1;
    else j++; //j = 3
    for(int s = 0; s < 3; s++) 
        dfs(r, j, s);//dfs(3, 3, 0)
        
dfs(3, 3, 0) r = 3, j = 3, k = 0;
    if(k == 0) 
        a[3][3] = a[2][3] | a[2][4];
    else if(k == 1) 
        a[2][1] = a[1][1] & a[1][2];
    else if(k == 2)
        a[2][1] = a[1][1] ^ a[1][2];
    if(r == 5 && j == 1) { 
        if(a[r][j] == 1) ans++; 
        return; 
    }
    if(r + j == 6) r++, j = 1;//r = 4, j = 1
    else j++; 
    for(int s = 0; s < 3; s++) 
        dfs(r, j, s);//dfs(4, 1, 0)
        
dfs(4, 1, 0) r = 4, j = 1, k = 0;
    if(k == 0) 
        a[4][1] = a[3][1] | a[3][2];
    else if(k == 1) 
        a[2][1] = a[1][1] & a[1][2];
    else if(k == 2)
        a[2][1] = a[1][1] ^ a[1][2];
    if(r == 5 && j == 1) { 
        if(a[r][j] == 1) ans++; 
        return; 
    }
    if(r + j == 6) r++, j = 1;
    else j++; //j = 2
    for(int s = 0; s < 3; s++) 
        dfs(r, j, s);//dfs(4, 2, 0)
                                                             //回溯过程
dfs(4, 2, 0) r = 4, j = 2, k = 0;                            dfs(4, 2, 0) r = 4, j = 2, k = 0;
    if(k == 0)                                                  if(k == 0) 
        a[4][2] = a[3][2] | a[3][3];                                a[4][2] = a[3][2] | a[3][3];
    else if(k == 1)                                             else if(k == 1)  
        a[2][1] = a[1][1] & a[1][2];                                a[2][1] = a[1][1] & a[1][2];
    else if(k == 2)                                             else if(k == 2)
        a[2][1] = a[1][1] ^ a[1][2];                                a[2][1] = a[1][1] ^ a[1][2];
    if(r == 5 && j == 1) {                                      if(r == 5 && j == 1) { 
        if(a[r][j] == 1) ans++;                                     if(a[r][j] == 1) ans++; 
        return;                                                     return; 
    }                                                           }
    if(r + j == 6) r++, j = 1;// r = 5, j = 1                   if(r + j == 6) r++, j = 1;// r = 5, j = 1
    else j++;                                                   else j++; 
    for(int s = 0; s < 3; s++)                                  for(int s = 0; s < 3; s++) 
        dfs(r, j, s);//dfs(5, 1, 0)                                 dfs(r, j, s);//dfs(5, 1, 1)
        
dfs(5, 1, 0) r = 5, j = 1, k = 0;                           dfs(5, 1, 1) r = 5, j = 1, k = 1;
    if(k == 0)                                                  if(k == 0)
        a[5][1] = a[4][1] | a[4][2];                                a[5][1] = a[4][1] | a[4][2];
    else if(k == 1)                                             else if(k == 1) 
        a[2][1] = a[1][1] & a[1][2];                                a[2][1] = a[1][1] & a[1][2];
    else if(k == 2)                                             else if(k == 2)
        a[2][1] = a[1][1] ^ a[1][2];                                a[2][1] = a[1][1] ^ a[1][2];
    if(r == 5 && j == 1) {                                      if(r == 5 && j == 1) { 
        if(a[r][j] == 1) ans++;                                     if(a[r][j] == 1) ans++; 
        return;     //开始回溯                                                return; 
    }                                                           }
//    if(r + j == 6) r++, j = 1;
//    else j++; 
//    for(int s = 0; s < 3; s++) 
//        dfs(r, j, s);
```