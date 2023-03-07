1008 Elevator (20 分)

The highest building in our city has only one elevator. A request list is made up with *N* positive numbers. The numbers denote at which floors the elevator will stop, in specified order. It costs 6 seconds to move the elevator up one floor, and 4 seconds to move down one floor. The elevator will stay for 5 seconds at each stop.

For a given request list, you are to compute the total time spent to fulfill the requests on the list. The elevator is on the 0th floor at the beginning and does not have to return to the ground floor when the requests are fulfilled.

### Input Specification:

Each input file contains one test case. Each case contains a positive integer *N*, followed by *N* positive numbers. All the numbers in the input are less than 100.

### Output Specification:

For each test case, print the total time on a single line.

### Sample Input:

```in
3 2 3 1
```

### Sample Output:

```out
41
```

**题目大意：电梯从0层开始向上，给出该电梯依次按顺序停的楼层数，并且已知上升需要6秒/层，下降需要4秒/层，停下来的话需要停5秒，问走完所有需要停的楼层后总共花了多少时间～**

**分析：累加计算输出～now表示现在的层数，a表示将要去的层数，当a > now，电梯上升，需要6 \* (a – now)秒，当a < now，电梯下降，需要4 \* (now – a)秒，每一次需要停5秒，最后输出累加的结果sum～**

```c++
#include<bits/stdc++.h>
using namespace std;
int main() 
{
    int a, now = 0, sum = 0;
    cin >> a;
    while(cin >> a) 
    {
        if(a > now)
            sum = sum + 6 * (a - now);
        else
            sum = sum + 4 * (now - a);
        now = a;
        sum += 5;
    }
    cout << sum;
    return 0;
}
```

自己写的

```c++
#include<bits/stdc++.h>
using namespace std;
int main()
{
    int up=0,down=0;
    int N,num,time;
    int tmp=0;
    cin>>N;
    for(int i=0;i<N;i++)
    {
        cin>>num;
        if(num>tmp)
        {
            up+=num-tmp;
            tmp=num;
        }
        else if(num<tmp)
        {
            down+=tmp-num;
            tmp=num;
        }
    }
    time=6*up+4*down+5*N;
    cout<<time;
    return 0;
}
```

