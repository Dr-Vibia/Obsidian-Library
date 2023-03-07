1155 Heap Paths (30 分)

In computer science, a **heap** is a specialized tree-based data structure that satisfies the heap property: if P is a parent node of C, then the key (the value) of P is either greater than or equal to (in a max heap) or less than or equal to (in a min heap) the key of C. A common implementation of a heap is the binary heap, in which the tree is a complete binary tree. (Quoted from Wikipedia at https://en.wikipedia.org/wiki/Heap_(data_structure))

One thing for sure is that all the keys along any path from the root to a leaf in a max/min heap must be in non-increasing/non-decreasing order.

Your job is to check every path in a given complete binary tree, in order to tell if it is a heap or not.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (1<*N*≤1,000), the number of keys in the tree. Then the next line contains *N* distinct integer keys (all in the range of **int**), which gives the level order traversal sequence of a complete binary tree.

### Output Specification:

For each given tree, first print all the paths from the root to the leaves. Each path occupies a line, with all the numbers separated by a space, and no extra space at the beginning or the end of the line. The paths must be printed in the following order: for each node in the tree, all the paths in its right subtree must be printed before those in its left subtree.

Finally print in a line `Max Heap` if it is a max heap, or `Min Heap` for a min heap, or `Not Heap` if it is not a heap at all.

### Sample Input 1:

```in
8
98 72 86 60 65 12 23 50
结尾无空行
```

### Sample Output 1:

```out
98 86 23
98 86 12
98 72 65
98 72 60 50
Max Heap
结尾无空行
```

### Sample Input 2:

```in
8
8 38 25 58 52 82 70 60
结尾无空行
```

### Sample Output 2:

```out
8 25 70
8 25 82
8 38 52
8 38 58 60
Min Heap
结尾无空行
```

### Sample Input 3:

```in
8
10 28 15 12 34 9 8 56
结尾无空行
```

### Sample Output 3:

```out
10 15 8
10 15 9
10 28 34
10 28 12 56
Not Heap
结尾无空行
```

题目大意：给出一颗完全二叉树，打印出从根节点到所有叶节点的路径，打印顺序先右后左，即先序遍历的镜像。然后判断该树是大顶堆、小顶堆或者不是堆～

分析：1.深搜打印出所有路径（从右往左，即先序的镜像），vector保存一路上的节点，通过push和pop回溯，维护路径，index <= n是对只有左叶节点没有右叶节点的点特判
2.判断是否为堆：从第二个节点开始遍历，如果比父节点小，就不是小顶堆，如果比父节点大，就不是大顶堆～

```c++
#include <iostream>
#include <vector>
using namespace std;
vector<int> v;
int a[1009], n, isMin = 1, isMax = 1;
void dfs(int index) {
    if (index * 2 > n && index * 2 + 1 > n) { //判断已经是叶子结点
        if (index <= n) {
            for (int i = 0; i < v.size(); i++)
                printf("%d%s", v[i], i != v.size() - 1 ? " " : "\n"); //打印路径，不是最后一个" ",最后一个"\n"
        }
    } else {
        v.push_back(a[index * 2 + 1]); //先输入右孩子
        dfs(index * 2 + 1);
        v.pop_back();
        v.push_back(a[index * 2]); //再输入z
        dfs(index * 2);
        v.pop_back();
    }
}
int main() {
    cin >> n;
    for (int i = 1; i <= n; i++)
        scanf("%d", &a[i]);
    v.push_back(a[1]);
    dfs(1);
    for (int i = 2; i <= n; i++) {
        if (a[i/2] > a[i]) isMin = 0; //父结点>子结点，则不是最小堆
        if (a[i/2] < a[i]) isMax = 0; //父结点<子结点，则不是最大堆
    }
    if (isMin == 1)
        printf("Min Heap");
    else 
        printf("%s", isMax == 1 ? "Max Heap" : "Not Heap"); 
    return 0;
}
```

自己复现

```c++
#include<bits/stdc++.h>
using namespace std;
int a[1009] = { 0 };
vector<int>s;
int isMin = 1, isMax = 1;
int n;
void dfs(int index)
{
    if (index <= n)
    {
        if (index * 2 > n && index * 2 + 1 > n)
        {
            for (int i = 0; i < s.size(); i++)
            {
                if (i == s.size() - 1)cout << s[i] << endl;
                else cout << s[i] << ' ';
            }
        }
        else
        {
            s.push_back(a[2 * index + 1]);
            dfs(2 * index + 1);
            s.pop_back();
            s.push_back(a[2 * index]);
            dfs(2 * index);
            s.pop_back();
        }
    }
    else return;
}
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++)
    {
        cin >> a[i];
    }
    s.push_back(a[1]);
    dfs(1);
    for (int i = 2; i <= n; i++) {
        if (a[i / 2] > a[i]) isMin = 0;
        if (a[i / 2] < a[i]) isMax = 0;
    }
    if (isMin)cout << "Min Heap";
    else if (isMax)cout << "Max Heap";
    else cout << "Not Heap";
    return 0;
}
```

