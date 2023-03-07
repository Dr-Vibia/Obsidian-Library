1005 Spell It Right (20 分)

Given a non-negative integer *N*, your task is to compute the sum of all the digits of *N*, and output every digit of the sum in English.

### Input Specification:

Each input file contains one test case. Each case occupies one line which contains an *N* (≤10100).

### Output Specification:

For each test case, output in one line the digits of the sum in English words. There must be one space between two consecutive words, but no extra space at the end of a line.

### Sample Input:

```in
12345
```

### Sample Output:

```out
one five
```

```c++
#include<bits/stdc++.h>
using namespace std;
int main()
{
    string num[10]={"zero","one","two","three","four","five","six","seven","eight","nine"};
    string c;
    cin>>c;
    int sum=0;
    for(int i=0;i<c.size();i++)
        sum+=c[i]-'0';
    string str=to_string(sum);
    for(int i=0;i<str.size();i++)
    {
        if(i!=0)cout<<' ';
        cout<<num[str[i]-'0'];
    }
    return 0;
}
```

