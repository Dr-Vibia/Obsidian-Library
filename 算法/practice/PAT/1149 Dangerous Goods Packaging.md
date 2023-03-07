1149 Dangerous Goods Packaging (25 分)

When shipping goods with containers, we have to be careful not to pack some incompatible goods into the same container, or we might get ourselves in serious trouble. For example, oxidizing agent （氧化剂） must not be packed with flammable liquid （易燃液体）, or it can cause explosion.

Now you are given a long list of incompatible goods, and several lists of goods to be shipped. You are supposed to tell if all the goods in a list can be packed into the same container.

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers: *N* (≤104), the number of pairs of incompatible goods, and *M* (≤100), the number of lists of goods to be shipped.

Then two blocks follow. The first block contains N pairs of incompatible goods, each pair occupies a line; and the second one contains M lists of goods to be shipped, each list occupies a line in the following format:

```
K G[1] G[2] ... G[K]
```

where `K` (≤1,000) is the number of goods and `G[i]`'s are the IDs of the goods. To make it simple, each good is represented by a 5-digit ID number. All the numbers in a line are separated by spaces.

### Output Specification:

For each shipping list, print in a line `Yes` if there are no incompatible goods in the list, or `No` if not.

### Sample Input:

```in
6 3
20001 20002
20003 20004
20005 20006
20003 20001
20005 20004
20004 20006
4 00001 20004 00002 20003
5 98823 20002 20003 20006 10010
3 12345 67890 23333
结尾无空行
```

### Sample Output:

```out
No
Yes
Yes
结尾无空行
```

**题目大意：集装箱运输货物时，我们必须特别小心，不能把不相容的货物装在一只箱子里。比如氧化剂绝对不能跟易燃液体同箱，否则很容易造成爆炸。给定一张不相容物品的清单，需要你检查每一张集装箱货品清单，判断它们是否能装在同一只箱子里。对每箱货物清单，判断是否可以安全运输。如果没有不相容物品，则在一行中输出 Yes，否则输出 No～**

**分析：用map存储每一个货物的所有不兼容货物～在判断给出的一堆货物是否是相容的时候，判断任一货物的不兼容货物是否在这堆货物中～如果存在不兼容的货物，则这堆货物不能相容～如果遍历完所有的货物，都找不到不兼容的两个货物，则这堆货物就是兼容的～**

```c++
#include <iostream>
#include <vector>
#include <map>
using namespace std;
int main() {
    int n, k, t1, t2;
    map<int,vector<int>> m;
    scanf("%d%d", &n, &k);	//n对不相容货物，k批货物
    for (int i = 0; i < n; i++) {
        scanf("%d%d", &t1, &t2);
        m[t1].push_back(t2);	//对于货物t1，将t2存储为不相容货物
        m[t2].push_back(t1);	//对于货物t2，将t1存储为不相容货物
    }
    while (k--) {
        int cnt, flag = 0, a[100000] = {0};
        scanf("%d", &cnt);	//cnt件货物
        vector<int> v(cnt);
        for (int i = 0; i < cnt; i++) {
            scanf("%d", &v[i]);
            a[v[i]] = 1;	//标记下标为v[i]d货物存在
        }
        for (int i = 0; i < v.size(); i++)	//对每个货物进行检查
            for (int j = 0; j < m[v[i]].size(); j++)	//遍历该货物的不相容货物清单
                if (a[m[v[i]][j]] == 1) flag = 1;	//存在不相容的货物
        printf("%s\n",flag ? "No" :"Yes");
    }
    return 0;
}
```

