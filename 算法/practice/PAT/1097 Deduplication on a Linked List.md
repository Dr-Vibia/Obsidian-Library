1097 Deduplication on a Linked List (25 分)

Given a singly linked list *L* with integer keys, you are supposed to remove the nodes with duplicated absolute values of the keys. That is, for each value *K*, only the first node of which the value or absolute value of its key equals *K* will be kept. At the mean time, all the removed nodes must be kept in a separate list. For example, given *L* being 21→-15→-15→-7→15, you must output 21→-15→-7, and the removed list -15→15.

### Input Specification:

Each input file contains one test case. For each case, the first line contains the address of the first node, and a positive *N* (≤105) which is the total number of nodes. The address of a node is a 5-digit nonnegative integer, and NULL is represented by −1.

Then *N* lines follow, each describes a node in the format:

```
Address Key Next
```

where `Address` is the position of the node, `Key` is an integer of which absolute value is no more than 104, and `Next` is the position of the next node.

### Output Specification:

For each case, output the resulting linked list first, then the removed list. Each node occupies a line, and is printed in the same format as in the input.

### Sample Input:

```in
00100 5
99999 -7 87654
23854 -15 00000
87654 15 -1
00000 -15 99999
00100 21 23854
结尾无空行
```

### Sample Output:

```out
00100 21 23854
23854 -15 99999
99999 -7 -1
00000 -15 87654
87654 15 -1
结尾无空行
```

**题目大意：给一个链表，去重（去掉值或者绝对值相等的），先输出删除后的链表，再输出删除了的链表。**
**分析：用结构体数组存储这个链表，大小为maxn = 100000，node[i]表示地址为i的结点。在结构体中定义一个num变量，将num变量先初始化为2 * maxn。通过改变num变量的值最后sort排序来改变链表的顺序。**
**将没有删除的结点的num标记为cnt1，cnt1为当前没有删除的结点的个数；将需要删除的结点的num标记为maxn + cnt2，cnt2表示当前删除了的结点的个数，因为一开始初始化为了2 \* maxn，所以我们可以通过对num排序达到：num = 0~maxn为不删除结点，num = maxn~2maxn为删除结点，num = 2maxn为无效结点**
**这样sort后就会按照需要输出的顺序将结点排序，我们只需要输出前cnt1+cnt2个结点即可～～**

```c++
#include <cstdio>
#include <stdlib.h>
#include <algorithm>
using namespace std;
const int maxn = 100000;
struct NODE {
    int address, key, next, num = 2 * maxn;
}node[maxn];
bool exist[maxn];
int cmp1(NODE a, NODE b){
    return a.num < b.num;
}
int main() {
    int begin, n, cnt1 = 0, cnt2 = 0, a;
    scanf("%d%d", &begin, &n); //起始地址和结点个数
    for(int i = 0; i < n; i++) {
        scanf("%d", &a); //结点地址
        scanf("%d%d", &node[a].key, &node[a].next); //结点值和下一个结点地址
        node[a].address = a;
    }
    for(int i = begin; i != -1; i = node[i].next) { //遍历链表
        if(exist[abs(node[i].key)] == false) {
            exist[abs(node[i].key)] = true; //将出现过的值（绝对值）标记
            node[i].num = cnt1; //更新num用来排序
            cnt1++; //记录没有删除的结点的个数
        }
        else {
            node[i].num = maxn + cnt2; //更新num用来排序
            cnt2++; //记录删除的结点的个数
        }
    }
    sort(node, node + maxn, cmp1); //空的结点因为num=2*maxn会被排到尾部
    int cnt = cnt1 + cnt2;
    for(int i = 0; i < cnt; i++) {
        if(i != cnt1 - 1 && i != cnt - 1) { //两个链表表尾特殊处理
            printf("%05d %d %05d\n", node[i].address, node[i].key, node[i+1].address);
        } else {
            printf("%05d %d -1\n", node[i].address, node[i].key); //尾结点
        }
    }
    return 0;
}
```

