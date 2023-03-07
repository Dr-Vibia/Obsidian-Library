1136 A Delayed Palindrome (20 分)

Consider a positive integer *N* written in standard notation with *k*+1 digits *a**i* as *a**k*⋯*a*1*a*0 with 0≤*a**i*<10 for all *i* and *a**k*>0. Then *N* is **palindromic** if and only if *a**i*=*a**k*−*i* for all *i*. Zero is written 0 and is also palindromic by definition.

Non-palindromic numbers can be paired with palindromic ones via a series of operations. First, the non-palindromic number is reversed and the result is added to the original number. If the result is not a palindromic number, this is repeated until it gives a palindromic number. Such number is called **a delayed palindrome**. (Quoted from https://en.wikipedia.org/wiki/Palindromic_number )

Given any positive integer, you are supposed to find its paired palindromic number.

### Input Specification:

Each input file contains one test case which gives a positive integer no more than 1000 digits.

### Output Specification:

For each test case, print line by line the process of finding the palindromic number. The format of each line is the following:

```
A + B = C
```

where `A` is the original number, `B` is the reversed `A`, and `C` is their sum. `A` starts being the input number, and this process ends until `C` becomes a palindromic number -- in this case we print in the last line `C is a palindromic number.`; or if a palindromic number cannot be found in 10 iterations, print `Not found in 10 iterations.` instead.

### Sample Input 1:

```in
97152
结尾无空行
```

### Sample Output 1:

```out
97152 + 25179 = 122331
122331 + 133221 = 255552
255552 is a palindromic number.
结尾无空行
```

### Sample Input 2:

```in
196
结尾无空行
```

### Sample Output 2:

```out
196 + 691 = 887
887 + 788 = 1675
1675 + 5761 = 7436
7436 + 6347 = 13783
13783 + 38731 = 52514
52514 + 41525 = 94039
94039 + 93049 = 187088
187088 + 880781 = 1067869
1067869 + 9687601 = 10755470
10755470 + 07455701 = 18211171
Not found in 10 iterations.
结尾无空行
```

**分析：1 将字符串倒置与原字符串比较看是否相等可知s是否为回文串**
**2 字符串s和它的倒置t相加，只需从头到尾相加然后再倒置（记得要处理最后一个进位carry，如果有进位要在末尾+’1’）**
**3 倒置可采用algorithm头文件里面的函数reverse(s.begin(), s.end())直接对s进行倒置**

```c++
#include <iostream>
#include <algorithm>
using namespace std;
string rev(string s) {
    reverse(s.begin(), s.end());
    return s;
}
string add(string s1, string s2) {
    string s = s1;
    int carry = 0;
    for (int i = s1.size() - 1; i >= 0; i--) { //字符串加法
        s[i] = (s1[i] - '0' + s2[i] - '0' + carry) % 10 + '0';
        carry = (s1[i] - '0' + s2[i] - '0' + carry) / 10; //进位
    }
    if (carry > 0) s = "1" + s; /
    return s;
}
int main() {
    string s, sum;
    int n = 10;
    cin >> s;
    if (s == rev(s)) { //要先进行一次判断
        cout << s << " is a palindromic number.\n";
        return 0;
    }
    while (n--) {
        sum = add(s, rev(s));
        cout << s << " + " << rev(s) << " = " << sum << endl;
        if (sum == rev(sum)) {
            cout << sum << " is a palindromic number.\n";
            return 0;
        }
        s = sum;
    }
    cout << "Not found in 10 iterations.\n";
    return 0;
}
```

