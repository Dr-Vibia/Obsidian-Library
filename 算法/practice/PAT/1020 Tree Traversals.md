1020 Tree Traversals (25 分)

Suppose that all the keys in a binary tree are distinct positive integers. Given the postorder and inorder traversal sequences, you are supposed to output the level order traversal sequence of the corresponding binary tree.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤30), the total number of nodes in the binary tree. The second line gives the postorder sequence and the third line gives the inorder sequence. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, print in one line the level order traversal sequence of the corresponding binary tree. All the numbers in a line must be separated by exactly one space, and there must be no extra space at the end of the line.

### Sample Input:

```in
7
2 3 1 5 7 6 4
1 2 3 4 5 6 7
```

### Sample Output:

```out
4 1 6 3 5 7 2
```

**题目大意：给定一棵二叉树的后序遍历和中序遍历，请你输出其层序遍历的序列。这里假设键值都是互不相等的正整数。**

**分析：与后序中序转换为前序的代码相仿（无须构造二叉树再进行广度优先搜索～），只不过加一个变量index，表示当前的根结点在二叉树中所对应的下标（从0开始），所以进行一次输出先序的递归过程中，就可以把根结点下标index及所对应的值存储在map<int, int> level中，map是有序的会根据index从小到大自动排序，这样递归完成后level中的值就是层序遍历的顺序**

**左子树在后序中的根结点为root – (end – i + 1)，即为当前根结点-(右子树的个数+1)。左子树在中序中的起始点start为start，末尾end点为i – 1.右子树的根结点为当前根结点的前一个结点root – 1，右子树的起始点start为i+1，末尾end点为end。**

**如果你不知道如何将后序和中序转换为先序，请看：[https://www.liuchuo.net/archives/2090](http://www.liuchuo.net/archives/2090)**

```c++
#include <cstdio>
#include <vector>
#include <map>
using namespace std;
vector<int> post, in;
map<int, int> level;
void pre(int root, int start, int end, int index) {
    if(start > end) return ;
    int i = start;
    while(i < end && in[i] != post[root]) i++;//在中序树中找到根节点
    level[index] = post[root];//将根节点的值填入到map中
    pre(root - 1 - end + i, start, i - 1, 2 * index + 1);//递归左子树
    pre(root - 1, i + 1, end, 2 * index + 2);//递归右子树
}
int main() {
    int n;
    scanf("%d", &n);
    post.resize(n);//后序树
    in.resize(n);//中序数
    for(int i = 0; i < n; i++) scanf("%d", &post[i]);
    for(int i = 0; i < n; i++) scanf("%d", &in[i]);
    pre(n-1, 0, n-1, 0);//将数据填入二叉树，下标从0开始，后序树中根节点即最后一个结点
    auto it = level.begin();
    printf("%d", it->second);//根节点
    while(++it != level.end()) printf(" %d", it->second);
    return 0;
}
```

