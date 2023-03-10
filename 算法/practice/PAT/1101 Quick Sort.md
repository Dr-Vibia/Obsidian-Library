1101 Quick Sort (25 分)

There is a classical process named **partition** in the famous quick sort algorithm. In this process we typically choose one element as the pivot. Then the elements less than the pivot are moved to its left and those larger than the pivot to its right. Given *N* distinct positive integers after a run of partition, could you tell how many elements could be the selected pivot for this partition?

For example, given *N*=5 and the numbers 1, 3, 2, 4, and 5. We have:

- 1 could be the pivot since there is no element to its left and all the elements to its right are larger than it;
- 3 must not be the pivot since although all the elements to its left are smaller, the number 2 to its right is less than it as well;
- 2 must not be the pivot since although all the elements to its right are larger, the number 3 to its left is larger than it as well;
- and for the similar reason, 4 and 5 could also be the pivot.

Hence in total there are 3 pivot candidates.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤105). Then the next line contains *N* distinct positive integers no larger than 109. The numbers in a line are separated by spaces.

### Output Specification:

For each test case, output in the first line the number of pivot candidates. Then in the next line print these candidates in increasing order. There must be exactly 1 space between two adjacent numbers, and no extra space at the end of each line.

### Sample Input:

```in
5
1 3 2 4 5
```

### Sample Output:

```out
3
1 4 5
```

**题目大意：快速排序中，我们通常采用某种方法取一个元素作为主元，通过交换，把比主元小的元素放到它的左边，比主元大的元素放到它的右边。 给定划分后的N个互不相同的正整数的排列，请问有多少个元素可能是划分前选取的主元？例如给定N = 5, 排列是1、3、2、4、5。则：**
**1的左边没有元素，右边的元素都比它大，所以它可能是主元；**
**尽管3的左边元素都比它小，但是它右边的2它小，所以它不能是主元；**
**尽管2的右边元素都比它大，但其左边的3比它大，所以它不能是主元；**
**类似原因，4和5都可能是主元。**
**因此，有3个元素可能是主元。
给N个数，第一行输出可能是主元的个数，第二行输出这些元素～**

**分析：对原序列sort排序，逐个比较，当当前元素没有变化并且它左边的所有值的最大值都比它小的时候就可以认为它一定是主元（很容易证明正确性的，毕竟无论如何当前这个数要满足左边都比他小右边都比他大，那它的排名【当前数在序列中处在第几个】一定不会变）～**
**如果硬编码就直接运行超时了…后来才想到这种方法～**
**一开始有一个测试点段错误，后来才想到因为输出时候v[0]是非法内存，改正后发现格式错误（好像可以说明那个第2个测试点是0个主元？…）然后加了最后一句printf(“\n”);才正确（难道是当没有主元的时候必须要输出空行吗…）**

```c++
#include <iostream>
#include <algorithm>
#include <vector>
int v[100000];
using namespace std;
int main() {
    int n, max = 0, cnt = 0;
    scanf("%d", &n);
    vector<int> a(n), b(n);
    for (int i = 0; i < n; i++) { //存储两份数组a和b
        scanf("%d", &a[i]);
        b[i] = a[i];
    }
    sort(a.begin(), a.end()); //对a进行排序
    for (int i = 0; i < n; i++) {
        if(a[i] == b[i] && b[i] > max) //a，b相同且b大于它左边的数
            v[cnt++] = b[i]; //把主元记录到v中
        if (b[i] > max)
            max = b[i];
    }
    printf("%d\n", cnt);
    for(int i = 0; i < cnt; i++) {
        if (i != 0) printf(" ");
        printf("%d", v[i]);
    }
    printf("\n");
    return 0;
}
```

