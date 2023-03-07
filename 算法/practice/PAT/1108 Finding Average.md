# 1108. Finding Average (20)-PAT甲级真题

**The basic task is simple: given N real numbers, you are supposed to calculate their average. But what makes it complicated is that some of the input numbers might not be legal. A “legal” input is a real number in [-1000, 1000] and is accurate up to no more than 2 decimal places. When you calculate the average, those illegal numbers must not be counted in.**

**Input Specification:**

**Each input file contains one test case. For each case, the first line gives a positive integer N (<=100). Then N numbers are given in the next line, separated by one space.**

**Output Specification:**

**For each illegal input number, print in a line “ERROR: X is not a legal number” where X is the input. Then finally print in a line the result: “The average of K numbers is Y” where K is the number of legal inputs and Y is their average, accurate to 2 decimal places. In case the average cannot be calculated, output “Undefined” instead of Y. In case K is only 1, output “The average of 1 number is Y” instead.**

**Sample Input 1:**
**7**
**5 -3.2 aaa 9999 2.3.4 7.123 2.35**
**Sample Output 1:**
**ERROR: aaa is not a legal number**
**ERROR: 9999 is not a legal number**
**ERROR: 2.3.4 is not a legal number**
**ERROR: 7.123 is not a legal number**
**The average of 3 numbers is 1.38**
**Sample Input 2:**
**2**
**aaa -9999**
**Sample Output 2:**
**ERROR: aaa is not a legal number**
**ERROR: -9999 is not a legal number**
**The average of 0 numbers is Undefined
**
**分析：用非常好用的sscanf和sprintf即可解决～
sscanf() – 从一个字符串中读进与指定格式相符的数据
sprintf() – 字符串格式化命令，主要功能是把格式化的数据写入某个字符串中**

```c++
#include <iostream>
#include <cstdio>
#include <string.h>
using namespace std;
int main() {
    int n, cnt = 0;
    char a[50], b[50];
    double temp = 0.0, sum = 0.0;
    cin >> n;
    for(int i = 0; i < n; i++) {
        scanf("%s", a);
        sscanf(a, "%lf", &temp); //将a这个字符串中提取浮点型数据存放到temp当中（从头开始读入数字，字符串j）
        sprintf(b, "%.2f",temp); //将temp这个数据按%.2f的形式存储到b这个字符串当中
        int flag = 0;
        for(int j = 0; j < strlen(a); j++) //精度不一样也报错
            if(a[j] != b[j]) flag = 1;
        if(flag || temp < -1000 || temp > 1000) {
            printf("ERROR: %s is not a legal number\n", a);
            continue;
        } else {
            sum += temp;
            cnt++;
        }
    }
    if(cnt == 1)
        printf("The average of 1 number is %.2f", sum);
    else if(cnt > 1)
        printf("The average of %d numbers is %.2f", cnt, sum / cnt);
    else
        printf("The average of 0 numbers is Undefined");
    return 0;
}
```

