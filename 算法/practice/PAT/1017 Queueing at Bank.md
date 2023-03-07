1017 Queueing at Bank (25 分)

Suppose a bank has *K* windows open for service. There is a yellow line in front of the windows which devides the waiting area into two parts. All the customers have to wait in line behind the yellow line, until it is his/her turn to be served and there is a window available. It is assumed that no window can be occupied by a single customer for more than 1 hour.

Now given the arriving time *T* and the processing time *P* of each customer, you are supposed to tell the average waiting time of all the customers.

### Input Specification:

Each input file contains one test case. For each case, the first line contains 2 numbers: *N* (≤104) - the total number of customers, and *K* (≤100) - the number of windows. Then *N* lines follow, each contains 2 times: `HH:MM:SS` - the arriving time, and *P* - the processing time in minutes of a customer. Here `HH` is in the range [00, 23], `MM` and `SS` are both in [00, 59]. It is assumed that no two customers arrives at the same time.

Notice that the bank opens from 08:00 to 17:00. Anyone arrives early will have to wait in line till 08:00, and anyone comes too late (at or after 17:00:01) will not be served nor counted into the average.

### Output Specification:

For each test case, print in one line the average waiting time of all the customers, in minutes and accurate up to 1 decimal place.

### Sample Input:

```in
7 3
07:55:00 16
17:00:01 2
07:59:59 15
08:01:00 60
08:00:00 30
08:00:02 2
08:03:00 10
```

### Sample Output:

```out
8.2
```

**题目大意：有n个客户，k个窗口。已知每个客户的到达时间和需要的时长，如果有窗口就依次过去，如果没有窗口就在黄线外等候（黄线外只有一个队伍，先来先服务），求客户的平均等待时长。银行开放时间为8点到17点，再8点之前不开门，8点之前来的人都要等待，在17点后来的人不被服务。**

**分析：用一个结构体存储客户的到达时间和办理业务时间~首先把所有hh:mm:ss格式的时间全化成以当天0点为基准的秒数。注意晚于17:00的客户不算在内～既然客户是排队的，那么排序后对于每个客户都是同样的处理方式～使用一个优先队列维护窗口办理完业务的时间～如果最早结束服务的窗口时间早于客户的到达时间，不需要等待，直接执行 q.push(p[i].come + p[i].time);否则客户的等待时间是q.top() – p[i].come～**

```c++
#include <iostream>
#include <queue>
#include <algorithm>
using namespace std;
const int maxn = 10005;
struct person {
    int come, time; //come记录到达时间，time记录服务需要的时间
} p[maxn];
int cmp(person p1, person p2) { return p1.come < p2.come; }
int n, k, cnt, total; //cnt记录的是有效客户
int main() {
    scanf("%d%d", &n, &k);
    for (int i = 1; i <= n; i++) {
        int hh, ss, mm, tt;
        scanf("%d:%d:%d %d", &hh, &mm, &ss, &tt);
        int sum = hh * 3600 + mm * 60 + ss;
        if (sum > 61200) continue; //超过17:00的跳过
        p[++cnt].time = tt * 60; //以秒为单位
        p[cnt].come = sum;
    }
    sort(p + 1, p + 1 + cnt, cmp); //按到达时间先后排序
    priority_queue<int, vector<int>, greater<int> > q; //创建优先级队列，按时间从小到大排
    for (int i = 1; i <= k; ++i) q.push(28800); //每个窗口服务时间初始设置为8:00
    for (int i = 1; i <= cnt; ++i) {
        if (q.top() <= p[i].come) //立即提供服务
        {
            q.push(p[i].come + p[i].time); //加入窗口服务完后的新时间
            q.pop(); //弹出旧的窗口服务时间
        } else //需要等待
        {
            total += q.top() - p[i].come; //累加等待时间
            q.push(q.top() + p[i].time);
            q.pop();
        }
    }
    (!cnt) ? printf("0.0\n") : printf("%.1lf", ((double)total/60.0)/(double) cnt); //保留一位小数 %lf是double
    return 0;
}
```

