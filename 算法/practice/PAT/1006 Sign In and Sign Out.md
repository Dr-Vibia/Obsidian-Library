1006 Sign In and Sign Out (25 分)

At the beginning of every day, the first person who signs in the computer room will unlock the door, and the last one who signs out will lock the door. Given the records of signing in's and out's, you are supposed to find the ones who have unlocked and locked the door on that day.

### Input Specification:

Each input file contains one test case. Each case contains the records for one day. The case starts with a positive integer *M*, which is the total number of records, followed by *M* lines, each in the format:

```
ID_number Sign_in_time Sign_out_time
```

where times are given in the format `HH:MM:SS`, and `ID_number` is a string with no more than 15 characters.

### Output Specification:

For each test case, output in one line the ID numbers of the persons who have unlocked and locked the door on that day. The two ID numbers must be separated by one space.

Note: It is guaranteed that the records are consistent. That is, the sign in time must be earlier than the sign out time for each person, and there are no two persons sign in or out at the same moment.

### Sample Input:

```in
3
CS301111 15:30:28 17:00:10
SC3021234 08:00:00 11:25:25
CS301133 21:45:00 21:58:40
```

### Sample Output:

```out
SC3021234 CS301133
```

**题目大意：给出n个人的id、sign in时间、sign out时间，求最早进来的人和最早出去的人的ID～**

**分析：将时间都转换为总秒数，最早和最迟的时间保存在变量minn和maxn中，并同时保存当前最早和最迟的人的ID，最后输出～**

```c++
#include <bits/stdc++.h>
using namespace std;
int main() {
    int n, minn = INT_MAX, maxn = INT_MIN;
    cin>>n;
    string unlocked, locked;
    for(int i = 0; i < n; i++) {
        string t;
        cin >> t;
        int h1, m1, s1, h2, m2, s2;
        scanf("%d:%d:%d %d:%d:%d", &h1, &m1, &s1, &h2, &m2, &s2);//C语言输入时间格式 hh:mm:ss
        int tempIn = h1 * 3600 + m1 * 60 + s1;
        int tempOut = h2 * 3600 + m2 * 60 + s2;
        if (tempIn < minn) 
        {
            minn = tempIn;
            unlocked = t;
        }
        if (tempOut > maxn) 
        {
            maxn = tempOut;
            locked = t;
        }
    }
    cout << unlocked << " " << locked;
    return 0;
}
```

自己写的(直接比较字符串)

```c++
#include<bits/stdc++.h>
using namespace std;
int main()
{
    int n,early=0,late=0;
    cin>>n;
    string id[100],in[100],out[100];
    for(int i=0;i<n;i++)
    {
        cin>>id[i]>>in[i]>>out[i];
    }
    int flag_in,flag_out;
    for(int i=0;i<n;i++)
    {
        if(in[i]<in[early])early=i;
    }
    for(int i=0;i<n;i++)
    {
        if(out[i]>out[late])late=i;
    }
    cout<<id[early]<<' '<<id[late];
    return 0;
}
```

