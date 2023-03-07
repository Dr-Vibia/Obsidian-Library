As an emergency rescue team leader of a city, you are given a special map of your country. The map shows several scattered cities connected by some roads. Amount of rescue teams in each city and the length of each road between any pair of cities are marked on the map. When there is an emergency call to you from some other city, your job is to lead your men to the place as quickly as possible, and at the mean time, call up as many hands on the way as possible.

作为城市的紧急救援队队长，您将获得一张您所在国家/地区的特殊地图。地图显示了由一些道路连接的几个分散的城市。地图上标出了每个城市的救援队数量以及任何一对城市之间的每条道路的长度。当其他城市有紧急电话给你时，你的工作是尽快带领你的人到达那个地方，同时尽可能多地在路上打电话。

### Input Specification:

Each input file contains one test case. For each test case, the first line contains 4 positive integers: *N* (≤500) - the number of cities (and the cities are numbered from 0 to *N*−1), *M* - the number of roads, *C*1 and *C*2 - the cities that you are currently in and that you must save, respectively. The next line contains *N* integers, where the *i*-th integer is the number of rescue teams in the *i*-th city. Then *M* lines follow, each describes a road with three integers *c*1, *c*2 and *L*, which are the pair of cities connected by a road and the length of that road, respectively. It is guaranteed that there exists at least one path from *C*1 to *C*2.

每个输入文件包含一个测试用例。对于每个测试用例，第一行包含 4 个正整数：N (≤500) - 城市数量（城市编号从 0 到 N−1），M - 道路数量，C1和C2分别是您当前所在和必须保存的城市。下一行包含 N 个整数，其中第 i 个整数是第 i 个城市的救援队数量。然后是 M 行，每行用三个整数 c 描述一条道路1,c2和L，分别是道路连接的城市对和道路的长度。保证至少存在一条来自 C 的路径1到C2。

### Output Specification:

For each test case, print in one line two numbers: the number of different shortest paths between *C*1 and *C*2, and the maximum amount of rescue teams you can possibly gather. All the numbers in a line must be separated by exactly one space, and there is no extra space allowed at the end of a line.

对于每个测试用例，在一行中打印两个数字：C 之间不同最短路径的数量1和C2，以及你可能聚集的最大数量的救援队。一行中的所有数字必须正好用一个空格隔开，并且行尾不允许有多余的空格。

### Sample Input:

```in
5 6 0 2
1 2 1 5 3
0 1 1
0 2 2
0 3 1
1 2 1
2 4 1
3 4 1
```

5个城市，6条路，起点0，终点2，每个城市的救援队1 2 1 5 3，城市0和城市1之间的路权重1……

### Sample Output:

```out
2 4
```

**题目大意：n个城市m条路，每个城市有救援小组，所有的边的边权已知。给定起点和终点，求从起点到终点的最短路径条数以及最短路径上的救援小组数目之和。如果有多条就输出点权（城市救援小组数目）最大的那个～**

**分析：用一遍Dijkstra算法～救援小组个数相当于点权，用Dijkstra求边权最小的最短路径的条数，以及这些最短路径中点权最大的值～dis[i]表示从出发点到i结点最短路径的路径长度，num[i]表示从出发点到i结点最短路径的条数，w[i]表示从出发点到i点救援队的数目之和～当判定dis[u] + e[u][v] < dis[v]的时候，不仅仅要更新dis[v]，还要更新num[v] = num[u], w[v] = weight[v] + w[u]; 如果dis[u] + e[u][v] == dis[v]，还要更新num[v] += num[u]，而且判断一下是否权重w[v]更小，如果更小了就更新w[v] = weight[v] + w[u];** 

```c++
#include <bits/stdc++.h>
using namespace std;
int n, m, c1, c2;//n个城市，m条路，c1起点，c2终点
int e[510][510], weight[510], dis[510], num[510], w[510];//e[i][j]i到j的距离，weight[]救援队数量，dis[i]到i最近距离，num[i]到i路径条数，w[i]到i救援队总数（'数字'默认为0）
bool visit[510];//默认false
const int inf = 99999999;//不可达
int main() {
    cin>>n>>m>>c1>>c2;
    for(int i = 0; i < n; i++)
        cin>>weight[i];
    fill(e[0], e[0] + 510 * 510, inf);
    fill(dis, dis + 510, inf);
    int a, b, c;
    for(int i = 0; i < m; i++) 
    {
        cin>>a>>b>>c;
        e[a][b] = e[b][a] = c;
    }
    dis[c1] = 0;
    w[c1] = weight[c1];
    num[c1] = 1;
    for(int i = 0; i < n; i++) //遍历n次
    {
        int u = -1, minn = inf;//u记录当前选择的点（新起点）
        for(int j = 0; j < n; j++) 
        {
            if(visit[j] == false && dis[j] < minn) //挑选一个未被选择且距离最短的点
            {
                u = j;
                minn = dis[j];
            }
        }
        if(u == -1) break;
        visit[u] = true;//标记该点已选择过
        for(int v = 0; v < n; v++) 
        {
            if(visit[v] == false && e[u][v] != inf) 
            {
                if(dis[u] + e[u][v] < dis[v]) //更新dis距离，w权重，继承num路数
                {
                    dis[v] = dis[u] + e[u][v];
                    num[v] = num[u];
                    w[v] = w[u] + weight[v];
                }
                else if(dis[u] + e[u][v] == dis[v]) //更新num路数，检测是否更新w权重
                {
                    num[v] = num[v] + num[u];
                    if(w[u] + weight[v] > w[v])
                        w[v] = w[u] + weight[v];
                }
            }
        }
    }
    cout<<num[c2]<<w[c2];
    return 0;
}
```

