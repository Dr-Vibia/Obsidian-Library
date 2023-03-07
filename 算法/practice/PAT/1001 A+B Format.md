1001 A+B Format (20 分)

Calculate *a*+*b* and output the sum in standard format -- that is, the digits must be separated into groups of three by commas (unless there are less than four digits).

### Input Specification:

Each input file contains one test case. Each case contains a pair of integers *a* and *b* where −106≤*a*,*b*≤106. The numbers are separated by a space.

### Output Specification:

For each test case, you should output the sum of *a* and *b* in one line. The sum must be written in the standard format.

### Sample Input:

```in
-1000000 9
```

### Sample Output:

```out
-999,991
```

Python

```python
a,b = map(int,input().split())
print(format(a+b,','))
```

```python
map(function, iterable, ...)
```

**map()** 会根据提供的函数对指定序列做映射。第一个参数 function 以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的新列表。

C++

```c++
#include<bits/stdc++.h>
using namespace std;
int main()
{
    int a,b,c;
    cin>>a>>b;
    c=a+b;
    string num=to_string(c);
    string ans;
    for(int i=num.size()-1,j=0;i>=0;i--)//从后往前遍历
    {
        ans=num[i]+ans;
        j++;
        if(j%3==0&&num[i-1]!='-'&&i) ans=','+ans;//前一位不能为'-'
    }
    cout<<ans<<endl;
    return 0;
}
```

