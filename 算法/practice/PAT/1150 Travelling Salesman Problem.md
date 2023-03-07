1150 Travelling Salesman Problem (25 分)

The "travelling salesman problem" asks the following question: "Given a list of cities and the distances between each pair of cities, what is the shortest possible route that visits each city and returns to the origin city?" It is an NP-hard problem in combinatorial optimization, important in operations research and theoretical computer science. (Quoted from "https://en.wikipedia.org/wiki/Travelling_salesman_problem".)

In this problem, you are supposed to find, from a given list of cycles, the one that is the closest to the solution of a travelling salesman problem.

### Input Specification:

Each input file contains one test case. For each case, the first line contains 2 positive integers *N* (2<*N*≤200), the number of cities, and *M*, the number of edges in an undirected graph. Then *M* lines follow, each describes an edge in the format `City1 City2 Dist`, where the cities are numbered from 1 to *N* and the distance `Dist` is positive and is no more than 100. The next line gives a positive integer *K* which is the number of paths, followed by *K* lines of paths, each in the format:

*n* *C*1 *C*2 ... *Cn*

where *n* is the number of cities in the list, and *Ci* 's are the cities on a path.

### Output Specification:

For each path, print in a line `Path X: TotalDist (Description)` where `X` is the index (starting from 1) of that path, `TotalDist` its total distance (if this distance does not exist, output `NA` instead), and `Description` is one of the following:

- `TS simple cycle` if it is a simple cycle that visits every city;
- `TS cycle` if it is a cycle that visits every city, but not a simple cycle;
- `Not a TS cycle` if it is NOT a cycle that visits every city.

Finally print in a line `Shortest Dist(X) = TotalDist` where `X` is the index of the cycle that is the closest to the solution of a travelling salesman problem, and `TotalDist` is its total distance. It is guaranteed that such a solution is unique.

### Sample Input:

```in
6 10
6 2 1
3 4 1
1 5 1
2 5 1
3 1 8
4 1 6
1 6 1
6 3 1
1 2 1
4 5 1
7
7 5 1 4 3 6 2 5
7 6 1 3 4 5 2 6
6 5 1 4 3 6 2
9 6 2 1 6 3 4 5 2 6
4 1 2 5 1
7 6 1 2 5 4 3 1
7 6 3 2 5 4 1 6
结尾无空行
```

### Sample Output:

```out
Path 1: 11 (TS simple cycle)
Path 2: 13 (TS simple cycle)
Path 3: 10 (Not a TS cycle)
Path 4: 8 (TS cycle)
Path 5: 3 (Not a TS cycle)
Path 6: 13 (Not a TS cycle)
Path 7: NA (Not a TS cycle)
Shortest Dist(4) = 8
结尾无空行
```

**题目大意：给出一条路径，判断这条路径是这个图的旅行商环路、简单旅行商环路还是非旅行商环路～**

**分析：如果给出的路径存在某两个连续的点不可达或者第一个结点和最后一个结点不同或者这个路径没有访问过图中所有的点，那么它就不是一个旅行商环路(flag = 0)～如果满足了旅行商环路的条件，那么再判断这个旅行商环路是否是简单旅行商环路，即是否访问过n+1个结点（源点访问两次）～最后输出这些旅行商环路中经过的路径最短的路径编号和路径长度～**

```c++
#include <iostream>
#include <vector>
#include <set>
using namespace std;
int e[300][300], n, m, k, ans = 99999999, ansid;
vector<int> v;
void check(int index) {
    int sum = 0, cnt, flag = 1;
    scanf("%d", &cnt);	//路径上有cnt个点
    set<int> s;
    vector<int> v(cnt);
    for (int i = 0; i < cnt; i++) {
        scanf("%d", &v[i]);	//记录点的顺序
        s.insert(v[i]);	//不重复的点
    }
    for (int i = 0; i < cnt - 1; i++) {
        if(e[v[i]][v[i+1]] == 0) flag = 0;		//不存在路径，标记flag为0
        sum += e[v[i]][v[i+1]];	//sum记录总路径长度
    }
    if (flag == 0) {	//不连通
        printf("Path %d: NA (Not a TS cycle)\n", index);
    } else if(v[0] != v[cnt-1] || s.size() != n) {	//首尾不相连或没有访问所有点
        printf("Path %d: %d (Not a TS cycle)\n", index, sum);
    } else if(cnt != n + 1) {	//不是简单旅行商环路
        printf("Path %d: %d (TS cycle)\n", index, sum);
        if (sum < ans) {	//更新最小路径长度和路径方案
            ans = sum;
            ansid = index;
        }
    } else {	//是简单旅行商环路
        printf("Path %d: %d (TS simple cycle)\n", index, sum);
        if (sum < ans) {	//更新最小路径长度和路径方案
            ans = sum;
            ansid = index;
        }
    }
}
int main() {
    scanf("%d%d", &n, &m);	//n个城市，m条路
    for (int i = 0; i < m; i++) {
        int t1, t2, t;
        scanf("%d%d%d", &t1, &t2, &t);	//城市1，城市2，距离
        e[t1][t2] = e[t2][t1] = t;
    }
    scanf("%d", &k);	//k条路径
    for (int i = 1; i <= k; i++) check(i);
    printf("Shortest Dist(%d) = %d\n", ansid, ans);
    return 0;
}
```

