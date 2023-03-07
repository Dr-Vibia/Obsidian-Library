1154 Vertex Coloring (25 分)

A **proper vertex coloring** is a labeling of the graph's vertices with colors such that no two vertices sharing the same edge have the same color. A coloring using at most *k* colors is called a (proper) ***k\*-coloring**.

Now you are supposed to tell if a given coloring is a proper *k*-coloring.

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers *N* and *M* (both no more than 104), being the total numbers of vertices and edges, respectively. Then *M* lines follow, each describes an edge by giving the indices (from 0 to *N*−1) of the two ends of the edge.

After the graph, a positive integer *K* (≤ 100) is given, which is the number of colorings you are supposed to check. Then *K* lines follow, each contains *N* colors which are represented by non-negative integers in the range of **int**. The *i*-th color is the color of the *i*-th vertex.

### Output Specification:

For each coloring, print in a line `k-coloring` if it is a proper `k`-coloring for some positive `k`, or `No` if not.

### Sample Input:

```in
10 11
8 7
6 8
4 5
8 4
8 1
1 2
1 4
9 8
9 1
1 0
2 4
4
0 1 0 1 4 1 0 1 3 0
0 1 0 1 4 1 0 1 0 0
8 1 0 1 4 1 0 5 3 0
1 2 3 4 5 6 7 8 8 9结尾无空行
```

### Sample Output:

```out
4-coloring
No
6-coloring
No结尾无空行
```

**题目大意：给出一个图（先给出所有边，后给出每个点的颜色），问是否满足：所有的边的两个点的颜色不相同**
**分析：把所有边存起来，把所有点的颜色存起来（存的过程中放入set统计颜色个数），枚举所有边，检查是否每条边的两点个颜色是否相同，若全不相同，则输出颜色个数，否则输出No～**

```c++
#include <iostream>
#include <vector>
#include <set>
using namespace std;
struct node {int t1, t2;}; //每条边有两个顶点
int main() {
    int n, m, k;
    cin >> n >> m; //n个点，m条边
    vector<node> v(m);
    for (int i = 0; i < m; i++)
        scanf("%d %d", &v[i].t1, &v[i].t2);
    cin >> k;
    while (k--) {
        int a[10009] = {0};
        bool flag = true;
        set<int> se; //se记录不重复的颜色的个数
        for (int i = 0; i < n; i++) {
            scanf("%d", &a[i]);
            se.insert(a[i]);
        }
        for (int i = 0; i < m; i++) { /
            if (a[v[i].t1] == a[v[i].t2]) {
                flag = false;
                break;
            }
        }
        if (flag) 
            printf("%d-coloring\n", se.size());
        else 
            printf("No\n");
    }
    return 0;
}
```

