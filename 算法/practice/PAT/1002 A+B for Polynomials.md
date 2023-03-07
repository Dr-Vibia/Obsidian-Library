**1002 A+B for Polynomials (25 分)**

This time, you are supposed to find *A*+*B* where *A* and *B* are two polynomials.

### Input Specification:

Each input file contains one test case. Each case occupies 2 lines, and each line contains the information of a polynomial:

*K* *N*1 *a**N*1 *N*2 *a**N*2 ... *N**K* *a**N**K*

where *K* is the number of nonzero terms in the polynomial, *N**i* and *a**N**i* (*i*=1,2,⋯,*K*) are the exponents and coefficients, respectively. It is given that 1≤*K*≤10，0≤*N**K*<⋯<*N*2<*N*1≤1000.

### Output Specification:

For each test case you should output the sum of *A* and *B* in one line, with the same format as the input. Notice that there must be NO extra space at the end of each line. Please be accurate to 1 decimal place.

### Sample Input:

```in
2 1 2.4 0 3.2
2 2 1.5 1 0.5
```

### Sample Output:

```out
3 2 1.5 1 2.9 0 3.2
```

**题目大意**

![img](https://img-blog.csdnimg.cn/20200525173153750.png)

输入两行，每行格式如上，K为多项式中非零项的个数，N为指数，aN为该项的系数。

最后输出两个多项式的和

```c++
#include <bits/stdc++.h>
using namespace std;
int main()
{
    float c[1001]={0};
    int m,n,t;
    float num;
    cin>>m;
    for(int i=0;i<m;i++)
    {
        cin>>t>>num;
        c[t]+=num;
    }
    cin>>n;
    for(int i=0;i<n;i++)
    {
        cin>>t>>num;
        c[t]+=num;
    }
    int cnt=0;
    for(int i=0;i<1001;i++)
    {
        if(c[i]!=0)cnt++;
    }
    cout<<cnt;
    for(int i=1000;i>=0;i--)
    {
        if(c[i]!=0.0)
            cout<<' '<<i<<' '<<fixed<<setprecision(1)<<c[i];//printf(" %d %.1f", i, c[i]);
    }
    return 0;
}
```

