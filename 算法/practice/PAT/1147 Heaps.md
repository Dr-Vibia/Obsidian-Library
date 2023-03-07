1147 Heaps (30 分)

In computer science, a **heap** is a specialized tree-based data structure that satisfies the heap property: if P is a parent node of C, then the key (the value) of P is either greater than or equal to (in a max heap) or less than or equal to (in a min heap) the key of C. A common implementation of a heap is the binary heap, in which the tree is a complete binary tree. (Quoted from Wikipedia at https://en.wikipedia.org/wiki/Heap_(data_structure))

Your job is to tell if a given complete binary tree is a heap.

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers: M (≤ 100), the number of trees to be tested; and N (1 < N ≤ 1,000), the number of keys in each tree, respectively. Then M lines follow, each contains N distinct integer keys (all in the range of **int**), which gives the level order traversal sequence of a complete binary tree.

### Output Specification:

For each given tree, print in a line `Max Heap` if it is a max heap, or `Min Heap` for a min heap, or `Not Heap` if it is not a heap at all. Then in the next line print the tree's postorder traversal sequence. All the numbers are separated by a space, and there must no extra space at the beginning or the end of the line.

### Sample Input:

```in
3 8
98 72 86 60 65 12 23 50
8 38 25 58 52 82 70 60
10 28 15 12 34 9 8 56
结尾无空行
```

### Sample Output:

```out
Max Heap
50 60 65 72 12 23 86 98
Min Heap
60 58 52 38 82 70 25 8
Not Heap
56 12 34 28 9 8 15 10
结尾无空行
```

**题目大意：给一个树的层序遍历，判断它是不是堆，是大顶堆还是小顶堆。输出这个树的后序遍历～**
**分析：30分大题，25行代码，一行代码一分……（(⊙o⊙)嗯） // 我为什么这么机智可爱又伶俐？**
**从后往前检查所有节点（除了根节点）和它的父节点的关系，判断是否破坏最大堆或者最小堆的性质，如果有不满足的情况将maxn或minn置为0，以此排除最大堆或者最小堆～**

**然后后序遍历，对于index结点分别遍历孩子index\*2和右孩子index\*2+1，遍历完左右子树后输出根结点～**

```c++
#include <iostream>
using namespace std;
int a[1005], m, n;
void postOrder(int index) {
    if (index > n) return;
    postOrder(index * 2);
    postOrder(index * 2 + 1);
    printf("%d%s", a[index], index == 1 ? "\n" : " ");
}
int main() {
    scanf("%d %d", &m, &n);
    while (m--) {
        int minn = 1, maxn = 1;
        for (int i = 1; i <= n; i++) scanf("%d", &a[i]);
        for (int i = 2; i <= n; i++) {
            if (a[i] > a[i / 2]) maxn = 0;
            if (a[i] < a[i / 2]) minn = 0;
        }
        if (maxn == 1) printf("Max Heap\n");
        else if (minn == 1) printf("Min Heap\n");
        else printf("Not Heap\n");
        postOrder(1);
    }
    return 0;
}
```

自己写的

```c++
#include<bits/stdc++.h>
using namespace std;
int n,m;
vector<int>v;

void dfs(int index)
{
    if(index<=m)
    {
        if(index*2>m)
        {
            cout<<v[index]<<' ';
            return;
        }
        else
        {
            dfs(index*2);
            dfs(index*2+1);
            if(index==1)cout<<v[index]<<endl;
            else cout<<v[index]<<' ';
        }
    }
    else return;
}

int main()
{
    cin>>n>>m;
    while(n--)
    {
        v.resize(m+1);
        bool max=true,min=true;
        for(int i=1;i<=m;i++)
        {
            cin>>v[i];
            if(i/2>0)
            {
                if(v[i]>v[i/2])max=false;
                else if(v[i]<v[i/2])min=false;
            }
        }
        if(max)cout<<"Max Heap"<<endl;
        else if(min)cout<<"Min Heap"<<endl;
        else cout<<"Not Heap"<<endl;
        dfs(1);
    }
    return 0;
}
```

