1007 Maximum Subsequence Sum (25 分)

Given a sequence of *K* integers { *N*1, *N*2, ..., *N**K* }. A continuous subsequence is defined to be { *N**i*, *N**i*+1, ..., *N**j* } where 1≤*i*≤*j*≤*K*. The Maximum Subsequence is the continuous subsequence which has the largest sum of its elements. For example, given sequence { -2, 11, -4, 13, -5, -2 }, its maximum subsequence is { 11, -4, 13 } with the largest sum being 20.

Now you are supposed to find the largest sum, together with the first and the last numbers of the maximum subsequence.

### Input Specification:

Each input file contains one test case. Each case occupies two lines. The first line contains a positive integer *K* (≤10000). The second line contains *K* numbers, separated by a space.

### Output Specification:

For each test case, output in one line the largest sum, together with the first and the last numbers of the maximum subsequence. The numbers must be separated by one space, but there must be no extra space at the end of a line. In case that the maximum subsequence is not unique, output the one with the smallest indices *i* and *j* (as shown by the sample case). If all the *K* numbers are negative, then its maximum sum is defined to be 0, and you are supposed to output the first and the last numbers of the whole sequence.

### Sample Input:

```in
10
-10 1 2 3 4 -5 -23 3 7 -21
```

### Sample Output:

```out
10 1 4
```

**题目大意：求最大连续子序列和，输出最大的和以及这个子序列的开始值和结束值。如果所有数都小于0，那么认为最大的和为0，并且输出首尾元素～**
**分析：sum为要求的最大和，temp为临时最大和，leftindex和rightindex为所求的子序列的下标，tempindex标记left的临时下标～**
**temp = temp + v[i]，当temp比sum大，就更新sum的值、leftindex和rightindex的值；当temp < 0，那么后面不管来什么值，都应该舍弃temp < 0前面的内容，因为负数对于总和只可能拉低总和，不可能增加总和，还不如舍弃～**
**舍弃后，直接令temp = 0，并且同时更新left的临时值tempindex。因为对于所有的值都为负数的情况要输出0，第一个值，最后一个值，所以在输入的时候用flag判断是不是所有的数字都是小于0的，如果是，要在输入的时候特殊处理～**

```c++
#include<bits/stdc++.h>
using namespace std;
int main() 
{
    int n;
    cin>>n;
    vector<int> v(n);
    int leftindex = 0, rightindex = n - 1, sum = -1, temp = 0, tempindex = 0;
    for (int i = 0; i < n; i++) //边输入边处理
    {
        cin>>v[i];
        temp = temp + v[i];
        if (temp < 0) 
        {
            temp = 0;
            tempindex = i + 1;
        } 
        else if (temp > sum) 
        {
            sum = temp;
            leftindex = tempindex;
            rightindex = i;
        }
    }
    if (sum < 0) sum = 0;
    cout<<sum<<' '<<v[leftindex]<<' '<<v[rightindex];
    return 0;
}
```

