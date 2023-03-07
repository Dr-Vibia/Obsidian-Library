# PAT 1151 cLCA in a Binary Tree（30 分）- 甲级

**The lowest common ancestor (LCA) of two nodes U and V in a tree is the deepest node that has both U and V as descendants.**

**Given any two nodes in a binary tree, you are supposed to find their LCA.**

**Input Specification:**
**Each input file contains one test case. For each case, the first line gives two positive integers: M (≤ 1,000), the number of pairs of nodes to be tested; and N (≤ 10,000), the number of keys in the binary tree, respectively. In each of the following two lines, N distinct integers are given as the inorder and preorder traversal sequences of the binary tree, respectively. It is guaranteed that the binary tree can be uniquely determined by the input sequences. Then M lines follow, each contains a pair of integer keys U and V. All the keys are in the range of int.**

**Output Specification:**
**For each given pair of U and V, print in a line LCA of U and V is A. if the LCA is found and A is the key. But if A is one of U and V, print X is an ancestor of Y. where X is A and Y is the other node. If U or V is not found in the binary tree, print in a line ERROR: U is not found. or ERROR: V is not found. or ERROR: U and V are not found..**

**Sample Input:**
**6 8**
**7 2 3 4 6 5 1 8**
**5 3 7 2 6 4 8 1**
**2 6**
**8 1**
**7 9**
**12 -3**
**0 8**
**99 99**
**Sample Output:**
**LCA of 2 and 6 is 3.**
**8 is an ancestor of 1.**
**ERROR: 9 is not found.**
**ERROR: 12 and -3 are not found.**
**ERROR: 0 is not found.**
**ERROR: 99 and 99 are not found.**

**题目大意：给出中序序列和先序序列，再给出两个点，求这两个点的最近公共祖先～**

**分析：不用建树～已知某个树的根结点，若a和b在根结点的左边，则a和b的最近公共祖先在当前子树根结点的左子树寻找，如果a和b在当前子树根结点的两边，在当前子树的根结点就是a和b的最近公共祖先，如果a和b在当前子树根结点的右边，则a和b的最近公共祖先就在当前子树的右子树寻找。中序加先序可以唯一确定一棵树，在不构建树的情况下，在每一层的递归中，可以得到树的根结点，在此时并入lca算法可以确定两个结点的公共祖先～**

```c++
#include <iostream>
#include <vector>
#include <map>
using namespace std;
unormap<int, int> pos; //记录结点 <结点值，下标>
vector<int> in, pre;
void lca(int inl, int inr, int preRoot, int a, int b) { //找最小祖先
    if (inl > inr) return;
    int inRoot = pos[pre[preRoot]], aIn = pos[a], bIn = pos[b];
    if (aIn < inRoot && bIn < inRoot) //两个结点都在根结点左侧，递归左子树
        lca(inl, inRoot-1, preRoot+1, a, b);
    else if ((aIn < inRoot && bIn > inRoot) || (aIn > inRoot && bIn < inRoot)) //如果两个结点在左右两侧
        printf("LCA of %d and %d is %d.\n", a, b, in[inRoot]);
    else if (aIn > inRoot && bIn > inRoot) //两个结点都在根结点右侧，递归右子树
        lca(inRoot+1, inr, preRoot+1+(inRoot-inl), a, b);
    else if (aIn == inRoot) //如果结点a是根结点
            printf("%d is an ancestor of %d.\n", a, b);
    else if (bIn == inRoot) //如果结点b是根结点
            printf("%d is an ancestor of %d.\n", b, a);
}
int main() {
    int m, n, a, b;
    scanf("%d %d", &m, &n);
    in.resize(n + 1), pre.resize(n + 1);
    for (int i = 1; i <= n; i++) {
        scanf("%d", &in[i]); //输入中序遍历
        pos[in[i]] = i;
    }
    for (int i = 1; i <= n; i++) scanf("%d", &pre[i]); //输入前序遍历
    for (int i = 0; i < m; i++) {
        scanf("%d %d", &a, &b);
        if (pos[a] == 0 && pos[b] == 0)
            printf("ERROR: %d and %d are not found.\n", a, b);
        else if (pos[a] == 0 || pos[b] == 0)
            printf("ERROR: %d is not found.\n", pos[a] == 0 ? a : b);
        else
            lca(1, n, 1, a, b);
    }
    return 0;
}
```

