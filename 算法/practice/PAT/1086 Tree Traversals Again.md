# 1086. Tree Traversals Again (25)-PAT甲级真题（树的遍历，前序中序转后序）

**An inorder binary tree traversal can be implemented in a non-recursive way with a stack. For example, suppose that when a 6-node binary tree (with the keys numbered from 1 to 6) is traversed, the stack operations are: push(1); push(2); push(3); pop(); pop(); push(4); pop(); pop(); push(5); push(6); pop(); pop(). Then a unique binary tree (shown in Figure 1) can be generated from this sequence of operations. Your task is to give the postorder traversal sequence of this tree.
![Snip20160811_80](http://www.liuchuo.net/wp-content/uploads/2016/08/Snip20160811_80.png)**

**Input Specification:**

**Each input file contains one test case. For each case, the first line contains a positive integer N (<=30) which is the total number of nodes in a tree (and hence the nodes are numbered from 1 to N). Then 2N lines follow, each describes a stack operation in the format: “Push X” where X is the index of the node being pushed onto the stack; or “Pop” meaning to pop one node from the stack.**

**Output Specification:**

**For each test case, print the postorder traversal sequence of the corresponding tree in one line. A solution is guaranteed to exist. All the numbers must be separated by exactly one space, and there must be no extra space at the end of the line.**

**Sample Input:**
**6**
**Push 1**
**Push 2**
**Push 3**
**Pop**
**Pop**
**Push 4**
**Pop**
**Pop**
**Push 5**
**Push 6**
**Pop**
**Pop**
**Sample Output:**
**3 4 2 6 5 1**
**题目大意：用栈的形式给出一棵二叉树的建立的顺序，求这棵二叉树的后序遍历**
**分析：栈实现的是二叉树的中序遍历（左根右），而每次push入值的顺序是二叉树的前序遍历（根左右），所以该题可以用二叉树前序和中序转后序的方法做～**
**root为当前子树的根结点在前序pre中的下标，start和end为当前子树的最左边和最右边的结点在中序in中的下标。用i找到当前子树的根结点root在中序中的下标，然后左边和右边就分别为当前根结点root的左子树和右子树。递归实现～**
Update：Github用户littlesevenmo给我发issue提出题目并没有说所有节点的值互不相同。因此，在有多个节点的值相同的情况下，之前的代码会输出错误的结果，所以修改后的代码中添加了key作为索引，前中后序中均保存索引值，然后用value存储具体的值，修改后的代码如下：

```c++
#include <cstdio>
#include <vector>
#include <stack>
#include <cstring>
using namespace std;
vector<int> pre, in, post,value; //value保存值，其他保存下标
void postorder(int root, int start, int end) { //前序、中序推后序
    if (start > end) return;
    int i = start;
    while (i < end && in[i] != pre[root]) i++; //在中序序列里找到前序中的根结点
    postorder(root + 1, start, i - 1); //根结点左边递归
    postorder(root + 1 + i - start, i + 1, end); //根结点右边递归
    post.push_back(pre[root]); //最后加入根结点
}
int main() {
    int n;
    scanf("%d", &n); //n个结点
    char str[5];
    stack<int> s;
    int key=0;
    while (~scanf("%s", str)) { //~表示输入取反，控制while循环
        if (strlen(str) == 4) { //push
            int num;
            scanf("%d", &num);
            value.push_back(num);
            pre.push_back(key); //前序序列
            s.push(key++);
        } else { //pop
            in.push_back(s.top()); //中序序列
            s.pop();
        }
    }
    postorder(0, 0, n - 1);
    printf("%d", value[post[0]]);
    for (int i = 1; i < n; i++)
        printf(" %d",value[post[i]]);
    return 0;
}
```

