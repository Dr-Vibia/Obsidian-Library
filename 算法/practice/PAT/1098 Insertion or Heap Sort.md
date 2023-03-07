1098 Insertion or Heap Sort (25 分)

According to Wikipedia:

**Insertion sort** iterates, consuming one input element each repetition, and growing a sorted output list. Each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there. It repeats until no input elements remain.

**Heap sort** divides its input into a sorted and an unsorted region, and it iteratively shrinks the unsorted region by extracting the largest element and moving that to the sorted region. it involves the use of a heap data structure rather than a linear-time search to find the maximum.

Now given the initial sequence of integers, together with a sequence which is a result of several iterations of some sorting method, can you tell which sorting method we are using?

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤100). Then in the next line, *N* integers are given as the initial sequence. The last line contains the partially sorted sequence of the *N* numbers. It is assumed that the target sequence is always ascending. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, print in the first line either "Insertion Sort" or "Heap Sort" to indicate the method used to obtain the partial result. Then run this method for one more iteration and output in the second line the resulting sequence. It is guaranteed that the answer is unique for each test case. All the numbers in a line must be separated by a space, and there must be no extra space at the end of the line.

### Sample Input 1:

```in
10
3 1 2 8 7 5 9 4 6 0
1 2 3 7 8 5 9 4 6 0结尾无空行
```

### Sample Output 1:

```out
Insertion Sort
1 2 3 5 7 8 9 4 6 0结尾无空行
```

### Sample Input 2:

```
10
3 1 2 8 7 5 9 4 6 0
6 4 5 1 0 3 2 7 8 9
```

### Sample Output 2:

```
Heap Sort
5 4 3 1 0 2 6 7 8 9
```

**题目大意：给出n和n个数的序列a和b，a为原始序列，b为排序其中的一个步骤，问b是a经过了堆排序还是插入排序的，并且输出它的下一步～**

**分析：插入排序的特点是：b数组前面的顺序是从小到大的，后面的顺序不一定，但是一定和原序列的后面的顺序相同～所以只要遍历一下前面几位，遇到不是从小到大的时候，开始看b和a是不是对应位置的值相等，相等就说明是插入排序，否则就是堆排序啦～**

**插入排序的下一步就是把第一个不符合从小到大的顺序的那个元素插入到前面已排序的里面的合适的位置，那么只要对前几个已排序的+后面一位这个序列sort排序即可～while(p <= n && b[p – 1] <= b[p]) p++；int index = p；找到第一个不满足条件的下标p并且赋值给index，b数组下标从1开始，所以插入排序的下一步就是sort(b.begin() + 1, b.begin() + index + 1)后的b数组～**

**堆排序的特点是后面是从小到大的，前面的顺序不一定，又因为是从小到大排列，堆排序之前堆为大顶堆，前面未排序的序列的最大值为b[1]，那么就可以从n开始往前找，找第一个小于等于b[1]的数字b[p]（while(p > 2 && b[p] >= b[1]) p–；），把它和第一个数字交换（swap(b[1], b[p])；），然后把数组b在1~p-1区间进行一次向下调整（downAdjust(b, 1, p – 1)；）～向下调整，low和high是需要调整的区间，因为是大顶堆，就是不断比较当前结点和自己的孩子结点哪个大，如果孩子大就把孩子结点和自己交换，然后再不断调整直到到达区间的最大值不能再继续了为止～**

```c++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;
void downAdjust(vector<int> &b, int low, int high) {
    int i = 1, j = i * 2;
    while(j <= high) {
        if(j + 1 <= high && b[j] < b[j + 1]) j = j + 1;
        if (b[i] >= b[j]) break;
        swap(b[i], b[j]);
        i = j; j = i * 2;
    }
}
int main() {
    int n, p = 2;
    scanf("%d", &n);
    vector<int> a(n + 1), b(n + 1);
    for(int i = 1; i <= n; i++) scanf("%d", &a[i]);
    for(int i = 1; i <= n; i++) scanf("%d", &b[i]);
    while(p <= n && b[p - 1] <= b[p]) p++;
    int index = p;
    while(p <= n && a[p] == b[p]) p++;
    if(p == n + 1) {
        printf("Insertion Sort\n");
        sort(b.begin() + 1, b.begin() + index + 1);
    } else {
        printf("Heap Sort\n");
        p = n;
        while(p > 2 && b[p] >= b[1]) p--;
        swap(b[1], b[p]);
        downAdjust(b, 1, p - 1);
    }
    printf("%d", b[1]);
    for(int i = 2; i <= n; i++)
        printf(" %d", b[i]);
    return 0;
}
```

