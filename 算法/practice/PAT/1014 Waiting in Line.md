1014 Waiting in Line (30 分)

Suppose a bank has *N* windows open for service. There is a yellow line in front of the windows which devides the waiting area into two parts. The rules for the customers to wait in line are:

- The space inside the yellow line in front of each window is enough to contain a line with *M* customers. Hence when all the *N* lines are full, all the customers after (and including) the (*N**M*+1)st one will have to wait in a line behind the yellow line.
- Each customer will choose the shortest line to wait in when crossing the yellow line. If there are two or more lines with the same length, the customer will always choose the window with the smallest number.
- *C**u**s**t**o**m**e**r**i* will take *T**i* minutes to have his/her transaction processed.
- The first *N* customers are assumed to be served at 8:00am.

Now given the processing time of each customer, you are supposed to tell the exact time at which a customer has his/her business done.

For example, suppose that a bank has 2 windows and each window may have 2 customers waiting inside the yellow line. There are 5 customers waiting with transactions taking 1, 2, 6, 4 and 3 minutes, respectively. At 08:00 in the morning, *c**u**s**t**o**m**e**r*1 is served at *w**i**n**d**o**w*1 while *c**u**s**t**o**m**e**r*2 is served at *w**i**n**d**o**w*2. *C**u**s**t**o**m**e**r*3 will wait in front of *w**i**n**d**o**w*1 and *c**u**s**t**o**m**e**r*4 will wait in front of *w**i**n**d**o**w*2. *C**u**s**t**o**m**e**r*5 will wait behind the yellow line.

At 08:01, *c**u**s**t**o**m**e**r*1 is done and *c**u**s**t**o**m**e**r*5 enters the line in front of *w**i**n**d**o**w*1 since that line seems shorter now. *C**u**s**t**o**m**e**r*2 will leave at 08:02, *c**u**s**t**o**m**e**r*4 at 08:06, *c**u**s**t**o**m**e**r*3 at 08:07, and finally *c**u**s**t**o**m**e**r*5 at 08:10.

### Input Specification:

Each input file contains one test case. Each case starts with a line containing 4 positive integers: *N* (≤20, number of windows), *M* (≤10, the maximum capacity of each line inside the yellow line), *K* (≤1000, number of customers), and *Q* (≤1000, number of customer queries).

The next line contains *K* positive integers, which are the processing time of the *K* customers.

The last line contains *Q* positive integers, which represent the customers who are asking about the time they can have their transactions done. The customers are numbered from 1 to *K*.

### Output Specification:

For each of the *Q* customers, print in one line the time at which his/her transaction is finished, in the format `HH:MM` where `HH` is in [08, 17] and `MM` is in [00, 59]. Note that since the bank is closed everyday after 17:00, for those customers who cannot be served before 17:00, you must output `Sorry` instead.

### Sample Input:

```in
2 2 7 5
1 2 6 4 3 534 2
3 4 5 6 7
```

### Sample Output:

```out
08:07
08:06
08:10
17:00
Sorry
```

**题目大意：n个窗口，每个窗口可以排队m人。有k位用户需要服务，给出了每位用户需要的minute数，所有客户在8点开始服务，如果有窗口还没排满就入队，否则就在黄线外等候。如果有某一列有一个用户走了服务完毕了，黄线外的人就进来一个。如果同时就选窗口数小的。求q个人的服务结束时间。**
**如果一个客户在17:00以及以后还没有开始服务（此处不是结束服务是开始17:00）就不再服务输出sorry；如果这个服务已经开始了，无论时间多长都要等他服务完毕。**
**分析：设立结构体，里面包含poptime为队首的人出队（结束）的时间，和endtime为队尾的人结束的时间。poptime是为了让黄线外的人可以计算出哪一个队列先空出人来（poptime最小的那个先有人服务完毕），endtime是为了入队后加上自己本身的服务所需时间可以计算出自己多久才能被服务完毕～且前一个人的endtime可以得知自己是不是需要被Sorry（如果前一个人服务结束时间超过17:00，自己当前入队的人就是sorry），还有一个queue表示所有当前该窗口的排队队列。**
**对于前m\*n个人，也就是排的下的情况下，所有人依次到窗口前面排队。对于m\*n之后的人，当前人选择poptime最短的入队，让队伍的第一个人出列），如果前面一个人导致的endtime超过17点就标记自己的sorry为true。**
**计算时间的时候按照分钟计算，最后再考虑08点开始和转换为小时分钟的形式会比较简便。**

```c++
#include <iostream>
#include <queue>
#include <vector>
using namespace std;
struct node //poptime队首的人出队的时间，endtime队尾的人结束的时间
{
    int poptime, endtime;
    queue<int> q;
};
int main()
{
    int n, m, k, q, index = 1; //n个窗口，每个窗口排m个人，k位用户，q个人查询
    scanf("%d%d%d%d", &n, &m, &k, &q);
    vector<int> time(k + 1), result(k + 1); //time记录服务的时长，result记录每个人结束服务的时间
    for(int i = 1; i <= k; i++)
    {
        scanf("%d", &time[i]);
    }
    vector<node> window(n + 1);
    vector<bool> sorry(k + 1, false);
    for(int i = 1; i <= m; i++) //遍历黄线内排队的人，即前m*n个人
    {
        for(int j = 1; j <= n; j++) //遍历窗口
        {
            if(index <= k) //遍历用户，依次入队
            {
                window[j].q.push(time[index]);
                if(window[j].endtime >= 540)
                    sorry[index] = true;
                window[j].endtime += time[index];
                if(i == 1) //poptime为队首（i=1）的endtime（服务时间）
                    window[j].poptime = window[j].endtime;
                result[index] = window[j].endtime;
                index++;
            }
        }
    }
    while(index <= k) //m*n之后的人
    {
        int tempmin = window[1].poptime, tempwindow = 1;
        for(int i = 2; i <= n; i++) //遍历窗口，寻找poptime最早的窗口
        {
            if(window[i].poptime < tempmin)
            {
                tempwindow = i;
                tempmin = window[i].poptime;
            }
        }
        window[tempwindow].q.pop();
        window[tempwindow].q.push(time[index]);
        window[tempwindow].poptime +=  window[tempwindow].q.front();
        if(window[tempwindow].endtime >= 540)
            sorry[index] = true;
        window[tempwindow].endtime += time[index];
        result[index] = window[tempwindow].endtime;
        index++;
    }
    for(int i = 1; i <= q; i++)
    {
        int query, minute;
        scanf("%d", &query);
        if(sorry[query] == true)
        {
            printf("Sorry\n");
        } else
        {
            minute = result[query];
            printf("%02d:%02d\n",(minute + 480) / 60, (minute + 480) % 60); //%02d，宽度为2，左边补0
        }
    }
    return 0;
}
```

