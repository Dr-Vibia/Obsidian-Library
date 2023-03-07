1021 Deepest Root (25 分)

A graph which is connected and acyclic can be considered a tree. The height of the tree depends on the selected root. Now you are supposed to find the root that results in a highest tree. Such a root is called **the deepest root**.

### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive integer *N* (≤104) which is the number of nodes, and hence the nodes are numbered from 1 to *N*. Then *N*−1 lines follow, each describes an edge by given the two adjacent nodes' numbers.

### Output Specification:

For each test case, print each of the deepest roots in a line. If such a root is not unique, print them in increasing order of their numbers. In case that the given graph is not a tree, print `Error: K components` where `K` is the number of connected components in the graph.

### Sample Input 1:

```in
5
1 2
1 3
1 4
2 5
```

### Sample Output 1:

```out
3
4
5
```

### Sample Input 2:

```in
5
1 3
1 4
2 5
3 4
```

### Sample Output 2:

```out
Error: 2 components
```

**题目大意：给出n个结点（1~n）之间的n条边，问是否能构成一棵树，如果不能构成则输出它有的连通分量个数，如果能构成一棵树，输出能构成最深的树的高度时，树的根结点。如果有多个，按照从小到大输出。**
**分析：首先深度优先搜索判断它有几个连通分量。如果有多个，那就输出Error: x components，如果只有一个，就两次深度优先搜索，先从一个结点dfs后保留最高高度拥有的结点们，然后从这些结点中的其中任意一个开始dfs得到最高高度的结点们，这两个结点集合的并集就是所求**

**证明两次遍历结果的并集为所求的根结点集合**

https://blog.csdn.net/qq_44408319/article/details/105696531

```c++
#include <iostream>
#include <vector>
#include <set>
#include <algorithm>
using namespace std;
int n, maxheight = 0;
vector<vector<int>> v;
bool visit[10010];
set<int> s;//set中的数据唯一且自动排序
vector<int> temp;//记录每次深度遍历中最深树的根结点
void dfs(int node, int height) {//深度优先算法
    if(height > maxheight) {//如果当前深度更深，清空temp并重新记录根结点，更新maxheight
        temp.clear();
        temp.push_back(node);
        maxheight = height;
    } else if(height == maxheight){//如果一样深，temp中增加当前结点
        temp.push_back(node);
    }
    visit[node] = true;//设置该结点为已访问
    for(int i = 0; i < v[node].size(); i++) {//遍历当前结点的所有相连的结点
        if(visit[v[node][i]] == false)//如果这个点没有被访问过，则继续深入遍历
            dfs(v[node][i], height + 1);
    }
}
int main() {
    scanf("%d", &n);//结点数目
    v.resize(n + 1);//实例化n+1个数组（n=0不使用）
    int a, b, cnt = 0, s1 = 0;
    for(int i = 0; i < n - 1; i++) {
        scanf("%d%d", &a, &b);//“边”填入结点的数组中
        v[a].push_back(b);
        v[b].push_back(a);
    }
    for(int i = 1; i <= n; i++) {
        if(visit[i] == false) {//遍历到一个没有访问过的结点
            dfs(i, 1);//深度遍历
            if(i == 1) {
                if (temp.size() != 0) s1 = temp[0];//在第一次遍历中记录一个结点s1
                for(int j = 0; j < temp.size(); j++)//把第一次深度遍历得到的结点存入set中
                    s.insert(temp[j]);
            }
            cnt++;//记录连通分量的个数
        }
    }
    if(cnt >= 2) {
        printf("Error: %d components", cnt);
    } else {//树
        temp.clear();
        maxheight = 0;
        fill(visit, visit + 10010, false);//重置各结点访问状态
        dfs(s1, 1);//再一次深度遍历
        for(int i = 0; i < temp.size(); i++)//将temp数组中记录的根结点们放入set中（去重，排序），即取并集
            s.insert(temp[i]);
        for(auto it = s.begin(); it != s.end(); it++)
            printf("%d\n", *it);
    }
    return 0;
}
```

