1009 Product of Polynomials (25 分)

This time, you are supposed to find *A*×*B* where *A* and *B* are two polynomials.

### Input Specification:

Each input file contains one test case. Each case occupies 2 lines, and each line contains the information of a polynomial:

*K* *N*1 *a**N*1 *N*2 *a**N*2 ... *N**K* *a**N**K*

where *K* is the number of nonzero terms in the polynomial, *N**i* and *a**N**i* (*i*=1,2,⋯,*K*) are the exponents and coefficients, respectively. It is given that 1≤*K*≤10, 0≤*N**K*<⋯<*N*2<*N*1≤1000.

### Output Specification:

For each test case you should output the product of *A* and *B* in one line, with the same format as the input. Notice that there must be **NO** extra space at the end of each line. Please be accurate up to 1 decimal place.

### Sample Input:

```in
2 1 2.4 0 3.2
2 2 1.5 1 0.5
```

### Sample Output:

```out
3 3 3.6 2 6.0 1 1.6
```

**题目大意：给出两个多项式A和B，求A\*B的结果～**

**分析：简单模拟～****double类型的arr数组保存第一组数据，ans数组保存结果。当输入第二组数据的时候，一边进行运算一边保存结果。最后按照指数递减的顺序输出所有不为0的项～**
**注意：因为相乘后指数可能最大为2000，所以ans数组最大要开到2001**

```c++
#include<bits/stdc++.h>
using namespace std;
int main()
{
    int n1, n2, a, cnt = 0;
    cin>>n1;
    double b,arr[1001]={0.0},ans[2001]={0.0};
    for(int i = 0; i < n1; i++) 
    {
        cin>>a>>b;
        arr[a] = b;
    }
    cin>>n2;
    for(int i=0;i<n2;i++)
    {
        cin>>a>>b;
        for(int j=0;j<1001;j++)
            ans[j+a]+=arr[j]*b;
    }
    for(int i=2000;i>=0;i--)
        if(ans[i] != 0.0) cnt++;
    cout<<cnt;
    for(int i=2000;i>=0;i--)
        if(ans[i]!=0.0)
            cout<<' '<<i<<' '<<fixed<<setprecision(1)<<ans[i];
            //printf(" %d %.1f",i,ans[i]);
    return 0;
}
```

