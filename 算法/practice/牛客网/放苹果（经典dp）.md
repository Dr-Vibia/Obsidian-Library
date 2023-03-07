## 描述

把M个同样的苹果放在N个同样的盘子里，允许有的盘子空着不放，问共有多少种不同的分法？（用K表示）5，1，1和1，5，1 是同一种分法。

### 输入描述：

每行均包含二个整数M和N，以空格分开。1<=M，N<=10。

### 输出描述：

对输入的每组数据M和N，用一行输出相应的K。

## 示例1

输入：

```
7 3
```

输出：

```
8
```



首先用**递归**的思想来思考这道题：

1. 递归出口：当只有一个盘子或者 含有 0 个 或 1 个苹果的时候只有一种方法；

2. 当盘子数 n 大于苹果数 m 时，则必有 n - m 个空盘子，所以只需求 m 个盘子放 m 个苹果时的方法数即可；

3. 当盘子数 n 小于等于 苹果数 m 时，**总方法数 = 当含有一个空盘子时的方法数 + 不含空盘子时的方法数**。

   > 原因：当在求只含有一个空盘子时的方法数时，已经包含了含有 2 ~ n - 1 个空盘子 的情况。
   >
   > 不含空盘子的计算：先将每个盘子装一个苹果，则问题变成了求 n 个盘子放 m - n 个苹果的方法数了。

其间，还可用记忆搜索优化（此处不再详讲）

然后用**动态规划**来优化代码：

新建一个动态规划表 `dp`；`dp[i][j]` 表示 `i` 个盘子放 `j` 个苹果的方法数。

- 当 i > j 时，`dp[i][j]` = `dp[i - (i - j)][j]` = `dp[j][j]`(原因上面已经讲过）
- 当 i <= j 时，**`dp[i][j]` = `dp[i - 1][j]` + `dp[i][j - i]`;（重点）**

最后`dp[n][m]` 就是所求。

```c++
#include <iostream>

using namespace std;

const int N = 21;

int dp[N][N];

int main(){
    int m, n, k;
    while(cin >> m >> n){
        for(int i = 0; i <= m; i++){
            for(int j = 1; j <= n; j++){
                if(i == 0 || j == 1){
                    dp[i][j] = 1;
                }else if(i < j){
                    dp[i][j] = dp[i][i];
                }else{
                    dp[i][j] = dp[i][j-1] + dp[i-j][j];	// 重点
                }
            }
        }
        printf("%d\n", dp[m][n]);
    }
    return 0;
}
```

递归

```c++
#include <iostream>

using namespace std;

const int N = 21;

int func(int m, int n){
    if(m == 0 || n == 1){
        return 1;
    }else if(m < n){
        return func(m, m);
    }else{
        return func(m, n-1) + func(m-n, n);
    }
}

int main(){
    int m, n, k;
    while(cin >> m >> n){
        int ans = func(m, n);
        printf("%d\n", ans);
    }
    return 0;
}
```

