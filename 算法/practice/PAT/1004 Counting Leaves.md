**1004 Counting Leaves (30 分)**

A family hierarchy is usually presented by a pedigree tree. Your job is to count those family members who have no child.

家庭层次结构通常由谱系树表示。你的工作是统计那些没有孩子的家庭成员。

### Input Specification:

Each input file contains one test case. Each case starts with a line containing 0<*N*<100, the number of nodes in a tree, and *M* (<*N*), the number of non-leaf nodes. Then *M* lines follow, each in the format:

每个输入文件包含一个测试用例。每个案例都以一行开始，其中包含 0<*N*<100（树中的节点数）和 *M* (<*N*)（非叶节点数）。然后是 *M* 行，每行格式为：

```
ID K ID[1] ID[2] ... ID[K]
```

where `ID` is a two-digit number representing a given non-leaf node, `K` is the number of its children, followed by a sequence of two-digit `ID`'s of its children. For the sake of simplicity, let us fix the root ID to be `01`.

其中“ID”是代表给定非叶节点的两位数，“K”是其子节点的编号，后跟其子节点的两位“ID”序列。为简单起见，让我们将根 ID 固定为“01”。

The input ends with *N* being 0. That case must NOT be processed.

输入以 *N* 为 0 结束。不能处理这种情况。

### Output Specification:

For each test case, you are supposed to count those family members who have no child **for every seniority level** starting from the root. The numbers must be printed in a line, separated by a space, and there must be no extra space at the end of each line.

对于每个测试用例，您应该从根开始计算 **每个资历级别** 没有孩子的家庭成员。数字必须打印成一行，用空格分隔，每行末尾不能有多余的空格。

The sample case represents a tree with only 2 nodes, where `01` is the root and `02` is its only child. Hence on the root `01` level, there is `0` leaf node; and on the next level, there is `1` leaf node. Then we should output `0 1` in a line.

示例案例表示只有 2 个节点的树，其中“01”是根节点，“02”是其唯一的子节点。因此在根`01`层，有`0`叶节点；在下一层，有 1 个叶节点。然后我们应该在一行中输出“0 1”。

### Sample Input:

```in
2 1
01 1 02
```

### Sample Output:

```out
0 1
```

**题目大意：给出一棵树，问每一层各有多少个叶子结点～**

**分析：可以用dfs也可以用bfs～如果用dfs，用二维数组保存每一个有孩子结点的结点以及他们的孩子结点，从根结点开始遍历，直到遇到叶子结点，就将当前层数depth的book[depth]++；标记第depth层拥有的叶子结点数，最后输出～**

```c++
#include <bits/stdc++.h>
using namespace std;

vector<int> v[100];
int book[100], maxdepth = -1;

void dfs(int index, int depth) 
{
    if(v[index].size() == 0) //该结点为叶子结点
    {
        book[depth]++;//计数加一
        maxdepth = max(maxdepth, depth);//更新深度
        return ;
    }
    for(int i = 0; i < v[index].size(); i++)//遍历该结点的孩子结点
        dfs(v[index][i], depth + 1);
}

int main() 
{
    int n, m, k, node, c;
    cin>>n>>m;//n为结点数，m为非叶结点数
    for(int i = 0; i < m; i++) //遍历每个非叶结点
    {
        cin>>node>>k;//输入非叶结点的编号和它拥有的子结点数量
        for(int j = 0; j < k; j++) //输入子结点
        {
            cin>>c
            v[node].push_back(c);
        }
    }
    dfs(1, 0);
    cout<<book[0];
    for(int i = 1; i <= maxdepth; i++)//输出每一层的叶子结点数量
        cout<<' '<<book[i];
    return 0;
}
```

