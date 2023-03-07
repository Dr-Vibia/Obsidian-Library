1010 Radix (25 分)

Given a pair of positive integers, for example, 6 and 110, can this equation 6 = 110 be true? The answer is `yes`, if 6 is a decimal number and 110 is a binary number.

Now for any pair of positive integers *N*1 and *N*2, your task is to find the radix of one number while that of the other is given.

### Input Specification:

Each input file contains one test case. Each case occupies a line which contains 4 positive integers:

```
N1 N2 tag radix
```

Here `N1` and `N2` each has no more than 10 digits. A digit is less than its radix and is chosen from the set { 0-9, `a`-`z` } where 0-9 represent the decimal numbers 0-9, and `a`-`z` represent the decimal numbers 10-35. The last number `radix` is the radix of `N1` if `tag` is 1, or of `N2` if `tag` is 2.

### Output Specification:

For each test case, print in one line the radix of the other number so that the equation `N1` = `N2` is true. If the equation is impossible, print `Impossible`. If the solution is not unique, output the smallest possible radix.

### Sample Input 1:

```in
6 110 1 10
```

### Sample Output 1:

```out
2
```

### Sample Input 2:

```in
1 ab 1 2
```

### Sample Output 2:

```out
Impossible
```

**解题思路**

> **第一步:先判断出要查找的这个数的进制上下限,下限是该数最大的那个数，上限是两个数中最大的那个数的十进制数**
> **第二步:二分查找,转换成十进制之后,如果该数小于已确定数,说明进制太小,如果大于或者为负数,则证明进制太大**
> **tips:单位数的时候从二进制依次往上找.**

**分析：convert函数：给定一个数值和一个进制，将它转化为10进制。转化过程中可能产生溢出**
**find_radix函数：找到令两个数值相等的进制数。在查找的过程中，需要使用二分查找算法，如果使用当前进制转化得到数值比另一个大或者小于0，说明这个进制太大～**

```c++
#include<bits/stdc++.h>
using namespace std;
long long convert(string n, long long radix) //根据基数radix转化为十进制数
{
    long long sum = 0;
    int index = 0, temp = 0;
    for (auto it = n.rbegin(); it != n.rend(); it++) //auto自动类型推断,rbegin逆向迭代器
    {
        temp = isdigit(*it) ? *it - '0' : *it - 'a' + 10; //isdigit判断是否是数字
        sum += temp * pow(radix, index++);
    }
    return sum;
}
long long find_radix(string n, long long num)//二分法，num为十进制的目标数
{
    char it = *max_element(n.begin(), n.end()); //max_element返回最大值的迭代器
    long long low = (isdigit(it) ? it - '0': it - 'a' + 10) + 1; //基数（进制）最小
    long long high = max(num, low); //基数（进制）最大
    while (low <= high)
    {
        long long mid = (low + high) / 2;
        long long t = convert(n, mid);
        if (t < 0 || t > num) //基数太大（t<0说明溢出变成了负数）
            high = mid - 1;
        else if (t == num)
            return mid;
        else //基数太小
            low = mid + 1;
    }
    return -1; //表示该函数失败
}
int main()
{
    string n1, n2;
    long long tag = 0, radix = 0, result_radix;
    cin >> n1 >> n2 >> tag >> radix;
    result_radix = tag == 1 ? find_radix(n2, convert(n1, radix)) : find_radix(n1, convert(n2, radix));
    if (result_radix != -1) 
    {
        printf("%lld", result_radix); //%d=int, %ld=long, %lld=long long;
    } 
    else {
        printf("Impossible");
    }   
    return 0;
}
```

begin 
方法：begin(); 
解释：begin()函数返回一个迭代器,指向字符串的第一个元素.

end 
方法：end(); 
解释：end()函数返回一个迭代器，指向字符串的末尾(最后一个字符的下一个位置).


rbegin 
方法：rbegin(); 
解释：rbegin()返回一个逆向迭代器，指向字符串的最后一个字符。

rend 
方法：rend(); 
解释：rend()函数返回一个逆向迭代器，指向字符串的开头（第一个字符的前一个位置）。

![img](https://img-blog.csdn.net/20180518122234389?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lzcTk2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

