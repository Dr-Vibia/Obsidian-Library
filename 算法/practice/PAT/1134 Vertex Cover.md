1134 Vertex Cover (25 分)

A **vertex cover** of a graph is a set of vertices such that each edge of the graph is incident to at least one vertex of the set. Now given a graph with several vertex sets, you are supposed to tell if each of them is a vertex cover or not.

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers *N* and *M* (both no more than 104), being the total numbers of vertices and the edges, respectively. Then *M* lines follow, each describes an edge by giving the indices (from 0 to *N*−1) of the two ends of the edge.

After the graph, a positive integer *K* (≤ 100) is given, which is the number of queries. Then *K* lines of queries follow, each in the format:

*N**v* *v*[1] *v*[2]⋯*v*[*N**v*]

where *N**v* is the number of vertices in the set, and *v*[*i*]'s are the indices of the vertices.

### Output Specification:

For each query, print in a line `Yes` if the set is a vertex cover, or `No` if not.

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
5
4 0 3 8 4
6 6 1 7 5 4 9
3 1 8 4
2 2 8
7 9 8 7 6 5 4 2
结尾无空行
```

### Sample Output:

```out
No
Yes
Yes
No
No
结尾无空行
```

**题目大意：给n个结点m条边，再给k个集合。对这k个集合逐个进行判断。每个集合S里面的数字都是结点编号，求问整个图所有的m条边两端的结点，是否至少一个结点出自集合S中。如果是，输出Yes否则输出No**

**分析：用vector v[n]保存某结点属于的某条边的编号，比如a b两个结点构成的这条边的编号为0，则v[a].push_back(0)，v[b].push_back(0)——表示a属于0号边，b也属于0号边。对于每一个集合做判断，遍历集合中的每一个元素，将当前元素能够属于的边的编号i对应的hash[i]标记为1，表示这条边是满足有一个结点出自集合S中的。最后判断hash数组中的每一个值是否都是1，如果有不是1的，说明这条边的两端结点没有一个出自集合S中，则输出No。否则输出Yes～**

```c++
#include <iostream>
#include <vector>
using namespace std;
int main() {
    int n, m, k, nv, a, b, num;
    scanf("%d%d", &n, &m); //n个点，m条边
    vector<int> v[n];
    for (int i = 0;i < m; i++) {
        scanf("%d%d", &a, &b); //边的两端是a和b
        v[a].push_back(i); //存储点a相邻的边的编号
        v[b].push_back(i); //存储点b相邻的边的编号
    }
    scanf("%d", &k); //k个集合
    for (int i = 0; i < k; i++) {
        scanf("%d", &nv); //集合里有nv个结点
        int flag = 0;
        vector<int> hash(m, 0);
        for (int j = 0; j < nv; j++) {
            scanf("%d", &num); //输入每个结点
            for (int t = 0; t < v[num].size(); t++) //遍历每个结点相连的边
                hash[v[num][t]] = 1; //遍历到的边hash值设为1
        }
        for (int j = 0; j < m; j++) {
            if (hash[j] == 0) { //如果有边没有被遍历到，说明这条边的两端结点没有一个出自集合S中
                printf("No\n");
                flag = 1;
                break;
            }
        }
        if (flag == 0) printf("Yes\n");
    }
    return 0;
}
```

