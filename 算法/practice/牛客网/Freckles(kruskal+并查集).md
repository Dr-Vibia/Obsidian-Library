## 描述

  In an episode of the Dick Van Dyke show, little Richie connects the freckles on his Dad's back to form a picture of the Liberty Bell. Alas, one of the freckles turns out to be a scar, so his Ripley's engagement falls through.   Consider Dick's back to be a plane with freckles at various (x,y) locations. Your job is to tell Richie how to connect the dots so as to minimize the amount of ink used. Richie connects the dots by drawing straight lines between pairs, possibly lifting the pen between lines. When Richie is done there must be a sequence of connected lines from any freckle to any other freckle.

### 输入描述：

  The first line contains 0 < n <= 100, the number of freckles on Dick's back. For each freckle, a line follows; each following line contains two real numbers indicating the (x,y) coordinates of the freckle.

### 输出描述：

  Your program prints a single real number to two decimal places: the minimum total length of ink lines that can connect all the freckles.

## 示例1

输入：

```
3
1.0 1.0
2.0 2.0
2.0 4.0
```

复制

输出：

```
3.41
```

**kruskal+并查集**

```c++
#include<stdio.h>
#include<math.h>
#include<stdlib.h>
typedef struct Node{
    int s; // 起点
    int d; // 终点
    double dis; // 距离
}Edge; // 边结构体
Edge E[4950]; // 100个点最多4950条边
int father[100];
int n; // 点个数
int cnt = 0; // 边个数
void init()
{
    for(int i = 0;i<n;i++)
        father[i] = i;
}
int findfather(int n)
{
    if(father[n] == n)
        return n;
    else
        return findfather(father[n]);
}

int cmp(const void*a,const void*b)
{
    Edge *x = (Edge *)a;
    Edge *y = (Edge *)b;
    return x->dis*1000 - y->dis*1000;
}
double kruskal()
{
    double ans = 0;
    qsort(E,cnt,sizeof(Edge),cmp);
    int j = 0; // 已添加的边的个数
    for(int i = 0;i<cnt;i++)
    {
        if(j == n-1)
            break;
        int x,y;
        //合并
        x = findfather(E[i].s);
        y = findfather(E[i].d);
        if(x!=y)
        {
            father[x] = y;
            ans += E[i].dis;
            j++;
        }
        else
            continue;
    }
    return ans;
}

int main()
{
    scanf("%d",&n);
    double c[n][2];
    init(); // father初始化
    for(int i = 0;i<n;i++)
        scanf("%lf%lf",&c[i][0],&c[i][1]);
    for(int i = 0;i<n;i++)
    {
        for(int j = i+1;j<n;j++)
        {
            E[cnt].s = i;
            E[cnt].d = j;
            E[cnt].dis = sqrt( (c[i][0]-c[j][0]) * (c[i][0]-c[j][0]) + (c[i][1]-c[j][1]) * (c[i][1]-c[j][1]) );
            cnt ++;
        }
    }
    printf("%.2lf",kruskal());
    return 0;
}
```

