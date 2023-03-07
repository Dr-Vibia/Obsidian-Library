## 描述

有一个神奇的口袋，总的容积是40，用这个口袋可以变出一些物品，这些物品的总体积必须是40。John现在有n个想要得到的物品，每个物品的体积分别是a1，a2……an。John可以从这些物品中选择一些，如果选出的物体的总体积是40，那么利用这个神奇的口袋，John就可以得到这些物品。现在的问题是，John有多少种不同的选择物品的方式。

### 输入描述：

输入的第一行是正整数n (1 <= n <= 20)，表示不同的物品的数目。接下来的n行，每行有一个1到40之间的正整数，分别给出a1，a2……an的值。

### 输出描述：

输出不同的选择物品的方式的数目。

## 示例1

输入：

```
3
20
20
20
```

复制

输出：

```
3
```





DFS

```c++
#include <iostream>
using namespace std;
int a[30];
int N;
int Ways(int w,int k)//从前k件物品中选择和为w的物品
{
    if(w==0)return 1;
    if(k<=0)return 0;
    return Ways(w,k-1)+Ways(w-a[k],k-1);//不放入第k件物品+放入第k件物品
}
int main() 
{
    cin>>N;
    for(int i=1;i<=N;++i)
        cin>>a[i];
    cout<<Ways(40,N);
    return 0;
}
```

DP

```c++
#include <bits/stdc++.h>
using namespace std;
int a[30];
int N;
int Ways[40][30];//Ways[i][j]表示从前j种物品里凑出体积i的方法数
int main() {
    cin>>N;
    memset(Ways,0,sizeof(Ways));
    for(int i=1;i<=N;i++)
    {
        cin>>a[i];
        Ways[0][i]=1;
    }
    Ways[0][0]=1;
    for(int w=1;w<=40;++w)
    {
        for(int k=1;k<=N;k++)
        {
            Ways[w][k]=Ways[w][k-1];//不放入a[k]
            if(w-a[k]>=0)
                Ways[w][k]+=Ways[w-a[k]][k-1];//放入a[k]
        }
    }
    cout<<Ways[40][N];
    return 0;
}
```

