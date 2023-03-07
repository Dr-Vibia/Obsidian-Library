1153 Decode Registration Card of PAT (25 分)

A registration card number of PAT consists of 4 parts:

- the 1st letter represents the test level, namely, `T` for the top level, `A` for advance and `B` for basic;
- the 2nd - 4th digits are the test site number, ranged from 101 to 999;
- the 5th - 10th digits give the test date, in the form of `yymmdd`;
- finally the 11th - 13th digits are the testee's number, ranged from 000 to 999.

Now given a set of registration card numbers and the scores of the card owners, you are supposed to output the various statistics according to the given queries.

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers *N* (≤104) and *M* (≤100), the numbers of cards and the queries, respectively.

Then *N* lines follow, each gives a card number and the owner's score (integer in [0,100]), separated by a space.

After the info of testees, there are *M* lines, each gives a query in the format `Type Term`, where

- `Type` being 1 means to output all the testees on a given level, in non-increasing order of their scores. The corresponding `Term` will be the letter which specifies the level;
- `Type` being 2 means to output the total number of testees together with their total scores in a given site. The corresponding `Term` will then be the site number;
- `Type` being 3 means to output the total number of testees of every site for a given test date. The corresponding `Term` will then be the date, given in the same format as in the registration card.

### Output Specification:

For each query, first print in a line `Case #: input`, where `#` is the index of the query case, starting from 1; and `input` is a copy of the corresponding input query. Then output as requested:

- for a type 1 query, the output format is the same as in input, that is, `CardNumber Score`. If there is a tie of the scores, output in increasing alphabetical order of their card numbers (uniqueness of the card numbers is guaranteed);
- for a type 2 query, output in the format `Nt Ns` where `Nt` is the total number of testees and `Ns` is their total score;
- for a type 3 query, output in the format `Site Nt` where `Site` is the site number and `Nt` is the total number of testees at `Site`. The output must be in non-increasing order of `Nt`'s, or in increasing order of site numbers if there is a tie of `Nt`.

If the result of a query is empty, simply print `NA`.

### Sample Input:

```in
8 4
B123180908127 99
B102180908003 86
A112180318002 98
T107150310127 62
A107180908108 100
T123180908010 78
B112160918035 88
A107180908021 98
1 A
2 107
3 180908
2 999
结尾无空行
```

### Sample Output:

```out
Case 1: 1 A
A107180908108 100
A107180908021 98
A112180318002 98
Case 2: 2 107
3 260
Case 3: 3 180908
107 2
123 2
102 1
Case 4: 2 999
NA
结尾无空行
```

题目大意：给出一组学生的准考证号和成绩，准考证号包含了等级(乙甲顶)，考场号，日期，和个人编号信息，并有三种查询方式
查询一：给出考试等级，找出该等级的考生，按照成绩降序，准考证升序排序
查询二：给出考场号，统计该考场的考生数量和总得分
查询三：给出考试日期，查询改日期下所有考场的考试人数，按照人数降序，考场号升序排序

分析：先把所有考生的准考证和分数记录下来～
1.按照等级查询，枚举选取匹配的学生，然后排序即可
2.按照考场查询，枚举选取匹配的学生，然后计数、求和
3.按日期查询每个考场人数，用unordered_map存储，最后排序汇总～
注意:1.第三个用map存储会超时，用unordered_map就不会超时啦～
2.排序传参建议用引用传参，这样更快，虽然有时候不用引用传参也能通过，但还是尽量用，养成好习惯～

```c++
#include <iostream>
#include <vector>
#include <unordered_map>
#include <algorithm>
using namespace std;
struct node {
    string t;
    int value;
};
bool cmp(const node &a, const node &b) {
    return a.value != b.value ? a.value > b.value : a.t < b.t;
}
int main() {
    int n, k, num;
    string s;
    cin >> n >> k; //n个考生，k个查询
    vector<node> v(n);
    for (int i = 0; i < n; i++) //输入准考证和成绩
        cin >> v[i].t >> v[i].value;
    for (int i = 1; i <= k; i++) {
        cin >> num >> s;
        printf("Case %d: %d %s\n", i, num, s.c_str()); //把string对象转换成C中的字符串样式
        vector<node> ans;
        int cnt = 0, sum = 0;
        if (num == 1) {
            for (int j = 0; j < n; j++)
                if (v[j].t[0] == s[0]) ans.push_back(v[j]); //列出z考试等级的考生
        } else if (num == 2) {
            for (int j = 0; j < n; j++) {
                if (v[j].t.substr(1, 3) == s) { //列出指定考场的考生
                    cnt++;
                    sum += v[j].value;
                }
            }
            if (cnt != 0) printf("%d %d\n", cnt, sum);
        } else if (num == 3) {
            unordered_map<string, int> m;
            for (int j = 0; j < n; j++)
                if (v[j].t.substr(4, 6) == s) m[v[j].t.substr(1, 3)]++; //列出指定日期的考生
            for (auto it : m) ans.push_back({it.first, it.second});
        }
        sort(ans.begin(), ans.end(),cmp); //对筛选出的学生进行排序
        for (int j = 0; j < ans.size(); j++)
            printf("%s %d\n", ans[j].t.c_str(), ans[j].value);
        if (((num == 1 || num == 3) && ans.size() == 0) || (num == 2 && cnt == 0)) printf("NA\n");
    }
    return 0;
}
```

