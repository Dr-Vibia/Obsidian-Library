1019 General Palindromic Number (20 分)

A number that will be the same when it is written forwards or backwards is known as a **Palindromic Number**. For example, 1234321 is a palindromic number. All single digit numbers are palindromic numbers.

Although palindromic numbers are most often considered in the decimal system, the concept of palindromicity can be applied to the natural numbers in any numeral system. Consider a number *N*>0 in base *b*≥2, where it is written in standard notation with *k*+1 digits *a**i* as ∑*i*=0*k*(*a**i**b**i*). Here, as usual, 0≤*a**i*<*b* for all *i* and *a**k* is non-zero. Then *N* is palindromic if and only if *a**i*=*a**k*−*i* for all *i*. Zero is written 0 in any base and is also palindromic by definition.

Given any positive decimal integer *N* and a base *b*, you are supposed to tell if *N* is a palindromic number in base *b*.

### Input Specification:

Each input file contains one test case. Each case consists of two positive numbers *N* and *b*, where 0<*N*≤109 is the decimal number and 2≤*b*≤109 is the base. The numbers are separated by a space.

### Output Specification:

For each test case, first print in one line `Yes` if *N* is a palindromic number in base *b*, or `No` if not. Then in the next line, print *N* as the number in base *b* in the form "*a**k* *a**k*−1 ... *a*0". Notice that there must be no extra space at the end of output.

### Sample Input 1:

```in
27 2
```

### Sample Output 1:

```out
Yes
1 1 0 1 1
```

### Sample Input 2:

```in
121 5
```

### Sample Output 2:

```out
No
4 4 1
```

题目大意：给出两个整数a和b，问十进制的a在b进制下是否为回文数。是的话输出Yes，不不是输出No。并且输出a在b进制下的表示，以空格隔开
分析：将a转换为b进制形式，保存在int的数组里面，比较数组左右两端是否对称。
注意：如果是0，要输出Yes和0

```c++
#include <cstdio>
using namespace std;
int main() {
	int a, b;
	scanf("%d %d", &a, &b);
	int arr[40], index = 0;
	while(a != 0) {
		arr[index++] = a % b;
		a = a / b;
	}
	int flag = 0;
	for(int i = 0; i < index / 2; i++) {
		if(arr[i] != arr[index-i-1]) {
			printf("No\n");
			flag = 1;
			break;
		}
	}
	if(!flag) printf("Yes\n");
	for(int i = index - 1; i >= 0; i--) {
		printf("%d", arr[i]);
		if(i != 0) printf(" ");
	}
	if(index == 0)
		printf("0");
	return 0;
}
```

自己写的15分

```c++
#include<bits/stdc++.h>
using namespace std;
int main()
{
    int n,b;
    cin>>n>>b;
    int tmp=n;
    string s="";
    if(n==0)
    {
        cout<<"Yes"<<endl<<n;
        return 0;
    }
    while(tmp)
    {
        s=to_string(tmp%b)+s;
        tmp/=b;
    }
    string stmp=s;
    reverse(stmp.begin(),stmp.end());
    if(stmp==s)
        cout<<"Yes"<<endl;
    else
        cout<<"No"<<endl;
    for(int i=0;i<s.size();i++)
    {
        if(i!=0)cout<<' ';
        cout<<s[i];
    }
    return 0;
}
```

