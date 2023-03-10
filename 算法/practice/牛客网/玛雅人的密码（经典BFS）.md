## 描述

玛雅人有一种密码，如果字符串中出现连续的2012四个数字就能解开密码。给一个长度为N的字符串，（2=<N<=13）该字符串中只含有0,1,2三种数字，问这个字符串要移位几次才能解开密码，每次只能移动相邻的两个数字。例如02120经过一次移位，可以得到20120,01220,02210,02102，其中20120符合要求，因此输出为1.如果无论移位多少次都解不开密码，输出-1。

### 输入描述：

输入包含多组测试数据，每组测试数据由两行组成。 第一行为一个整数N，代表字符串的长度（2<=N<=13）。 第二行为一个仅由0、1、2组成的，长度为N的字符串。

### 输出描述：

对于每组测试数据，若可以解出密码，输出最少的移位次数；否则输出-1。

## 示例1

输入：

```
5
02120
```

输出：

```
1
```

### 思路

将原始字符串看作树的根节点，进行一次交换的字符串作为子节点，依次往下交换，然后使用广度优先搜索（BFS）遍历这棵树，也就是层序遍历，每层的字符串对应一个 Map 值，含有2012的字符串在哪一层，就输出该层的 Map 值，如图所示。保证树上的每个结点都不相同，直到穷尽。

```c++
#include<iostream>
#include<queue>
#include<string>
#include<unordered_map>

using namespace std;

struct NewStr{
    string s;
    int step;
    NewStr(int i, string s):step(i), s(s){}
};

unordered_map<string, bool> isVisited;//避免重复入队相同字符串
void bfs(string s){
    queue<NewStr> q;
    q.push(NewStr(0, s));
    isVisited[s] = true;
    while(!q.empty()){
        NewStr t = q.front();
        q.pop();
        string ts = t.s;
        if(ts.find("2012") != string::npos){
            cout << t.step << endl;
            return;
        }
        for(int i = 0; i < ts.size() - 1; i ++){
            swap(ts[i], ts[i + 1]);
            if(!isVisited[ts]) {
                q.push(NewStr(t.step + 1, ts));
                isVisited[ts] = true;
            }
            swap(ts[i], ts[i + 1]);
        }
    }
    cout << -1 << endl;
} 

int main(){
    int n;
    string s;
    while(cin>>n>>s){
        bfs(s);
    }
    return 0;
}
```

