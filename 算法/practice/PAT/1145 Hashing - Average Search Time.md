1145 Hashing - Average Search Time (25 分)

The task of this problem is simple: insert a sequence of distinct positive integers into a hash table first. Then try to find another sequence of integer keys from the table and output the average search time (the number of comparisons made to find whether or not the key is in the table). The hash function is defined to be *H*(*k**ey*)=*k**ey*%*TS**i**ze* where *TS**i**ze* is the maximum size of the hash table. Quadratic probing (with positive increments only) is used to solve the collisions.

Note that the table size is better to be prime. If the maximum size given by the user is not prime, you must re-define the table size to be the smallest prime number which is larger than the size given by the user.

### Input Specification:

Each input file contains one test case. For each case, the first line contains 3 positive numbers: MSize, N, and M, which are the user-defined table size, the number of input numbers, and the number of keys to be found, respectively. All the three numbers are no more than 104. Then N distinct positive integers are given in the next line, followed by M positive integer keys in the next line. All the numbers in a line are separated by a space and are no more than 105.

### Output Specification:

For each test case, in case it is impossible to insert some number, print in a line `X cannot be inserted.` where `X` is the input number. Finally print in a line the average search time for all the M keys, accurate up to 1 decimal place.

### Sample Input:

```in
4 5 4
10 6 4 15 11
11 4 15 2
结尾无空行
```

### Sample Output:

```out
15 cannot be inserted.
2.8
结尾无空行
```

**题目大意：给定一个序列，用平方探测法解决哈希冲突，然后给出m个数字，如果这个数字不能够被插入就输出”X cannot be inserted.”，然后输出这m个数字的平均查找时间**
**分析：先找到大于tsize的最小的素数为真正的tsize，然后建立一个tsize长度的数组。首先用平方探测法插入数字a，每次pos = (a + j \* j) % tsize，j是从0～tsize-1的数字，如果当前位置可以插入就将a赋值给v[pos]，如果一次都没有能够插入成功就输出”X cannot be inserted.”。其次计算平均查找时间，每次计算pos = (a + j \* j) % tsize，其中j <= tsize，如果v[pos]处正是a则查找到了，则退出循环，如果v[pos]处不存在数字表示没查找到，那么也要退出循环。每次查找的时候，退出循环之前的j就是这个数字的查找长度。最后ans除以m得到平均查找时间然后输出～**

```c++
#include <iostream>
#include <vector>
using namespace std;
bool isprime(int n) {	//判断是否是质数
    if (n <= 1) return false;
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0) return false;
    return true;
}
int main() {
    int tsize, n, m, a;
    scanf("%d %d %d", &tsize, &n, &m);	//表的大小，n个要插入的数，m个要查询的数
    while(!isprime(tsize)) tsize++;	//计算真正的表的大小
    vector<int> v(tsize);
    for (int i = 0; i < n; i++) {
        scanf("%d", &a);	//输入要插入的数据
        int flag = 0;
        for (int j = 0; j < tsize; j++) {
            int pos = (a + j * j) % tsize;	//计算要插入的位置（平方探测到tsize）
            if (v[pos] == 0) {	//如果为空，可以插入
                v[pos] = a;	//更新下标，表示已经插入
                flag = 1;	//标记可插入
                break;
            }
        }
        if (!flag) printf("%d cannot be inserted.\n", a);
    }
    int ans = 0;
    for (int i = 0; i < m; i++) {
        scanf("%d", &a);	
        for (int j = 0; j <= tsize; j++) {
            ans++;	//累积
            int pos = (a + j * j) % tsize;
            if (v[pos] == a || v[pos] == 0) break;	//v[pos]为a说明探测到，v[pos]为0说明c
        }
    }
    printf("%.1lf\n", ans * 1.0 / m);	//double类型一位精度
    return 0;
}
```

