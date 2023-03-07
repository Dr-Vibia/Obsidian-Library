1143 Lowest Common Ancestor (30 分)

The lowest common ancestor (LCA) of two nodes U and V in a tree is the deepest node that has both U and V as descendants.

A binary search tree (BST) is recursively defined as a binary tree which has the following properties:

- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
- Both the left and right subtrees must also be binary search trees.

Given any two nodes in a BST, you are supposed to find their LCA.

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers: M (≤ 1,000), the number of pairs of nodes to be tested; and N (≤ 10,000), the number of keys in the BST, respectively. In the second line, N distinct integers are given as the preorder traversal sequence of the BST. Then M lines follow, each contains a pair of integer keys U and V. All the keys are in the range of **int**.

### Output Specification:

For each given pair of U and V, print in a line `LCA of U and V is A.` if the LCA is found and `A` is the key. But if `A` is one of U and V, print `X is an ancestor of Y.` where `X` is `A` and `Y` is the other node. If U or V is not found in the BST, print in a line `ERROR: U is not found.` or `ERROR: V is not found.` or `ERROR: U and V are not found.`.

### Sample Input:

```in
6 8
6 3 1 2 5 4 8 7
2 5
8 7
1 9
12 -3
0 8
99 99
结尾无空行
```

### Sample Output:

```out
LCA of 2 and 5 is 3.
8 is an ancestor of 7.
ERROR: 9 is not found.
ERROR: 12 and -3 are not found.
ERROR: 0 is not found.
ERROR: 99 and 99 are not found.
结尾无空行
```

**题目大意：给出一棵二叉搜索树的前序遍历，问结点u和v的共同最低祖先是谁～**
**分析：map<int, bool> mp用来标记树中所有出现过的结点，遍历一遍pre数组，将当前结点标记为a，如果u和v分别在a的左、右，或者u、v其中一个就是当前a，即(a >= u && a <= v) || (a >= v && a <= u)，说明找到了这个共同最低祖先a，退出当前循环～最后根据要求输出结果即可～**
**PS：30分的题目30行代码解决，1行1分，惊不惊喜？意不意外？（真的是水题啊…）**

```c++
//先序遍历中遍历到的第一个值在两点之间的点就是最小祖先
#include <iostream>
#include <vector>
#include <map>
using namespace std;
map<int, bool> mp;
int main() {
    int m, n, u, v, a;
    scanf("%d %d", &m, &n);	//m次查询，n个结点
    vector<int> pre(n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &pre[i]);	//输入前序序列
        mp[pre[i]] = true;	//输入的结点标记为true
    }
    for (int i = 0; i < m; i++) {	//m次查询
        scanf("%d %d", &u, &v);	//输入两个结点
        for(int j = 0; j < n; j++) {
            a = pre[j];	//遍历先序序列
            if ((a >= u && a <= v) || (a >= v && a <= u)) break; //如果该结点在u，v之间，说明找到所求点
        } 
        if (mp[u] == false && mp[v] == false) //如果映射里根本没有这两个结点
            printf("ERROR: %d and %d are not found.\n", u, v);
        else if (mp[u] == false || mp[v] == false) //如果映射里没有其中一个结点
            printf("ERROR: %d is not found.\n", mp[u] == false ? u : v);
        else if (a == u || a == v) //如果u或v就是祖先结点
            printf("%d is an ancestor of %d.\n", a, a == u ? v : u);
        else
            printf("LCA of %d and %d is %d.\n", u, v, a);
    }
    return 0;
}
```

