# 1029. Median (25)-PAT甲级真题（two points）

**Given an increasing sequence S of N integers, the median is the number at the middle position. For example, the median of S1={11, 12, 13, 14} is 12, and the median of S2={9, 10, 15, 16, 17} is 15. The median of two sequences is defined to be the median of the nondecreasing sequence which contains all the elements of both sequences. For example, the median of S1 and S2 is 13.**

**Given two increasing sequences of integers, you are asked to find their median.**

**Input**

**Each input file contains one test case. Each case occupies 2 lines, each gives the information of a sequence. For each sequence, the first positive integer N (<=1000000) is the size of that sequence. Then N integers follow, separated by a space. It is guaranteed that all the integers are in the range of long int.**

**Output**

**For each test case you should output the median of the two given sequences in a line.**

**Sample Input**
**4 11 12 13 14**
**5 9 10 15 16 17**
**Sample Output**
**13**

**题目大意：给出两个已排序序列，求这两个序列合并后的中间数**

**分析：既然两个数组都是递增的顺序，可以借助归并的思想~与归并排序不同的是，在第一个while里如果找到了中位数，就直接跳出来～
如果其中一个数组已经走到头也没有找到中位数，可以用数学公式直接推导出中位数在另一个数组中的位置～**

```c++
#include <iostream>
const int maxn = 200005;
int n, m, a1[maxn], a2[maxn], cnt = 0, i, j, ans;
int main() {
	scanf("%d", &n);
	for(i = 1; i <= n; i++)	scanf("%d", &a1[i]);
	scanf("%d", &m);
	for(i = 1; i <= m; i++)	scanf("%d", &a2[i]);
	int target = (n + m + 1) / 2;
	i = 1, j = 1;
	while(i <= n && j <= m) {
		ans = a1[i] <= a2[j] ? a1[i++] : a2[j++];
		if(++cnt == target) break;
	}
	if(i <= n && cnt < target)	
		ans = a1[i + target - cnt - 1];
	else if(j <= m && cnt < target)	
		ans = a2[j + target - cnt - 1];
	printf("%d", ans);
	return 0;
}
```

我的

```c++
#include<bits/stdc++.h>
using namespace std;
int cmp1(int n1,int n2)
{
    return n1<n2;
}
int main()
{
    int n1,n2;
    cin>>n1;
    int a[400001];
    int i=0;
    for(i=0;i<n1;i++)
    {
        cin>>a[i];
    }
    cin>>n2;
    for(;i<n1+n2;i++)
    {
        cin>>a[i];
    }
    sort(a,a+n1+n2,cmp1);
    int sum=n1+n2;
    if(sum%2)
        cout<<a[(n1+n2)/2]<<endl;
    else
        cout<<a[(n1+n2)/2-1]<<endl;
    return 0;
}
```

