# PAT 1148 Werewolf – Simple Version – 甲级

**Werewolf（狼人杀） is a game in which the players are partitioned into two parties: the werewolves and the human beings. Suppose that in a game,**

**player #1 said: “Player #2 is a werewolf.”;**
**player #2 said: “Player #3 is a human.”;**
**player #3 said: “Player #4 is a werewolf.”;**
**player #4 said: “Player #5 is a human.”; and**
**player #5 said: “Player #4 is a human.”.**
**Given that there were 2 werewolves among them, at least one but not all the werewolves were lying, and there were exactly 2 liers. Can you point out the werewolves?**

**Now you are asked to solve a harder version of this problem: given that there were N players, with 2 werewolves among them, at least one but not all the werewolves were lying, and there were exactly 2 liers. You are supposed to point out the werewolves.**

**Input Specification:**
**Each input file contains one test case. For each case, the first line gives a positive integer N (5≤N≤100). Then N lines follow and the i-th line gives the statement of the i-th player (1≤i≤N), which is represented by the index of the player with a positive sign for a human and a negative sign for a werewolf.**

**Output Specification:**
**If a solution exists, print in a line in ascending order the indices of the two werewolves. The numbers must be separated by exactly one space with no extra spaces at the beginning or the end of the line. If there are more than one solution, you must output the smallest solution sequence — that is, for two sequences A=a[1],…,a[M] and B=b[1],…,b[M], if there exists 0≤k[k+1]<b[k+1], then A is said to be smaller than B. In case there is no solution, simply print No Solution.**

**Sample Input 1:**
**5**
**-2**
**+3**
**-4**
**+5**
**+4**
**Sample Output 1:**
**1 4**
**Sample Input 2:**
**6**
**+6**
**+3**
**+1**
**-5**
**-2**
**+4**
**Sample Output 2 (the solution is not unique):**
**1 5**
**Sample Input 3:**
**5**
**-2**
**-3**
**-4**
**-5**
**-1**
**Sample Output 3:**
**No Solution**

**题目大意：已知 N 名玩家中有 2 人扮演狼人角色，有 2 人说的不是实话，有狼人撒谎但并不是所有狼人都在撒谎。要求你找出扮演狼人角色的是哪几号玩家，如果有解，在一行中按递增顺序输出 2 个狼人的编号；如果解不唯一，则输出最小序列解；若无解则输出 No Solution～**

**分析：每个人说的数字保存在v数组中，i从1～n、j从i+1～n遍历，分别假设i和j是狼人，a数组表示该人是狼人还是好人，等于1表示是好人，等于-1表示是狼人。k从1～n分别判断k所说的话是真是假，k说的话和真实情况不同（即v[k] * a[abs(v[k])] < 0）则表示k在说谎，则将k放在lie数组中；遍历完成后判断lie数组，如果说谎人数等于2并且这两个说谎的人一个是好人一个是狼人（即a[lie[0]] + a[lie[1]] == 0）表示满足题意，此时输出i和j并return，否则最后的时候输出No Solution～**

```c++
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;
int main() {
    int n;
    cin >> n;
    vector<int> v(n+1);
    for (int i = 1; i <= n; i++) cin >> v[i];
    for (int i = 1; i <= n; i++) {
        for (int j = i + 1; j <= n; j++) {
            vector<int> lie, a(n + 1, 1); /
            a[i] = a[j] = -1; //设置i和j为狼人
            for (int k = 1; k <= n; k++)
                if (v[k] * a[abs(v[k])] < 0) lie.push_back(k); //说的和真实情况不同
            if (lie.size() == 2 && a[lie[0]] + a[lie[1]] == 0) {
                cout << i << " " << j;
                return 0;
            }
        }
    }
    cout << "No Solution";
    return 0;
}
```

