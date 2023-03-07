# 头文件与名称空间

## 头文件

​	`#include<bits/stdc++.h>`

------

## 名称空间

​	`using namespace std;`

> 不引入：`std::cin >> n; std::cout << n;`

------



# 输入、输出、格式、返回

## 输入

**scanf**

```c
scanf("%d", &n);
char a[50];
scanf("%d", a); //a是数组

while (~scanf("%s", str))
// '~'是取反，当读入'EOF'时，返回值是-1，（-1的补码表示全是1，按位取反后全是0，即为假）
```

**getline**

```c++
string s;
getline(cin, s); //读入一行，包括空格
```

> `cin`输入后，后边会保留一个换行符，然后`getline`忽略空格时，就会造成换行符被读入。所以在`cin`之后用**`getchar`**吸收换行符。
>
> 解释：`scanf`和`cin`输入只是将空格和换行符以前的输入， 而不会删除紧接的空格和字符，而`gets`和`getline`则是将输入缓存中的换行符以前的字符读入，然后删除换行符，若是不吸收，那么再输入n之后的换行符就相当于输入了一行空的字符串
>
> [字符串排序.md](D:\ysy\机试练习\牛客网\字符串排序)

**sscanf函数**

描述：C 库函数 **int sscanf(const char \*str, const char \*format, ...)** 从字符串读取格式化输入。

返回值：如果成功，该函数返回成功匹配和赋值的个数。如果到达文件末尾或发生读错误，则返回 EOF。

```c++
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
   int day, year;
   char weekday[20], month[20], dtm[100];

   strcpy( dtm, "Saturday March 25 1989" );
   sscanf( dtm, "%s %s %d %d", weekday, month, &day, &year );

   printf("%s %d, %d = %s\n", month, day, year, weekday );
   
   return(0);
}

// March 25, 1989 = Saturday
```

------

## 输出

**printf**

```c
printf("%d", n);
printf("%s",str.c_str()); //string变量需要用c_str()函数获取地址
```

**sprintf函数**

`sprintf`函数原型为`int sprintf(char \*str, const char \*format, ...)`。作用是格式化字符串，具体功能如下所示：

（1）将数字变量转换为字符串。

（2）得到整型变量的16进制和8进制字符串。

（3）连接多个字符串。

举例如下所示：

```c++
char str[256] = { 0 };
int data = 1024;
//将data转换为字符串
sprintf(str,"%d",data);
//获取data的十六进制
sprintf(str,"0x%X",data);
//获取data的八进制
sprintf(str,"0%o",data);
const char *s1 = "Hello";
const char *s2 = "World";
//连接字符串s1和s2
sprintf(str,"%s %s",s1,s2);
```

[1108 Finding Average.md](D://ysy//PAT//1108 Finding Average.md)

------

## 格式

**变量类型**

```c
%f //单精度浮点float
%lf //双精度浮点double
%d //整形
%ld //long int
%lld //long long int
%c //字符
%s //字符串
printf("%s",str.c_str()); //string变量需要用c_str()函数获取地址
```

**字宽、填充、精度**

```c
%2d //表示输出场宽为 2 的整数，超过 2 位按实际数据输出，不够 2 位右对齐输出
%02d //表示输出场宽为 2 的整数，超过 2 位按实际数据输出，不够 2 位前置补 0
%5.2d //表示输出场宽为 5 的浮点数，其中小数点后有 2 位，不够 5 位右对齐输出
```

------

## 返回

`return {};`表示“返回函数的返回类型的对象，使用空的 [list-initializer初始化](http://en.cppreference.com/w/cpp/language/list initialization) ”。确切的行为取决于返回的对象的类型。

```c++
vector<int> twoSum(vector<int>& nums, int target) {
    int n = nums.size();
    for (int i = 0; i < n; ++i) {
        for (int j = i + 1; j < n; ++j) {
            if (nums[i] + nums[j] == target) {
                return {i, j}; //返回向量
            }
        }
    }
    return {}; //返回空向量
}
```

------



# 数据结构

## 字符串 `string`

**创建**

```c++
string s0 = "Initial String";
string s1;
string s2 (s0);
string s3 (s0, 8, 3);	//第8个字符开始取3个:"Str"
string s4 ("A character sequence");
string s5 ("Another character sequence", 12);	//取前12个字符:"Another char"
string s6 (10, 'x')	//n个重复的字符x:"xxxxxxxxxx"
```

**取长**

```c++
s.length(); //两者的功能基本相同
s.size();
```

**insert**

```c++
str.insert(0,"hello"); //在字符串头插入
str.insert(str.size(),"hello"); //在字符串尾插入
```

**erase**

```c++
str.erase(0,12); //删除下标0到12的元素
str.erase(7); //删除下标7之后的元素
```

**clear**

```c++
str.clear(); //清空
```

**find**

```c++
int found = str.find("world"); //找字符串，返回下标
int found = str.find('l'); //找字符，返回下标
if(found == string::npos); //找不到返回string::npos

//返回子串出现在母串中的首次出现的位置，和最后一次出现的位置
str.find_first_of("c");
str.find_last_of("");

//查找某一给定位置后的子串的位置
str.find("b",5);
```

**substr**

```c++
string s2 = s.substr(4); //表示从下标 4 开始一直到结束
string s3 = s.substr(5, 3); //表示从下标 5 开始，3 个字符
```



## 向量 `vector`

**初始化**

```c++
vector<int> v(15); //初始化定义大小，默认赋值为 0
vector<int> v(15, 2); //初始化定义大小并赋值
```

**empty**

```c++
v.empty(); //判空
```

**size**

```c++
v.size(); //求大小
```

**resize**

```c++
v.resize(); //分配大小
```

**push_back**

```c++
v.push_back(i); //从尾部添加元素
```

**pop_back()**

```c++
v.pop_back(); //从尾部删除元素
```

**insert**

```c++
v.insert(v.begin(),9); //头部插入9
v.insert(v.begin(),3,15); //头部插入3个15
```

**erase**

```c++
v.erase(v.begin()+5,v.end()); //删除第5后续的元素
```

**clear**

```c++
v.clear(); //清空
```

------



## 集合 `set & unordered_set`

`set`里的元素是各不相同的，而且`set`会按照元素进行从小到大排序

**定义**

```c++
set<int> s; //定义一个空集合s
```

**插入**

```c++
s.insert(1); //向集合s里面插入一个1
```

**输出**

```c++
*(s.begin()) //输出集合s的第一个元素
```

**查找**

```c++
s.find(2); //查找集合s中的值
```

**删除**

```c++
s.erase(1); //删除集合s中的1这个元素
```

**遍历`set`元素**

```c++
for (auto it = s.begin(); it != s.end(); it++)
{
	cout << *it << endl;
}
```

**unordered_set**

`unordered_set`在头⽂件`#include <unordered_set>`中，`set`⾥⾯会按照集合中的元素大小进行排序（从小到大顺序），⽽`unordered_set`省去了这个排序的过程

------



## 映射 `map & unordered_map`

`map`是键值对，`map`会自动将所有的键值对按照键值从小到大排序，`map`使用头文件`#include<map>`

**定义**

```c++
map<string,int>m; //键是string，值是int
```

**存入**

```c++
m["hello"] = 2; //将key为"hello"，value为2的键值对（key-value）存入map中
m.insert(pair<string,int>("Hello",2)); //使用insert()存数据
```

**删除**

```c++
m.erase("Hello"); //删除键为Hello的映射
```

**查找**

```c++
map<string,int>::iterator it; //创建迭代器
it = m.find("Hello"); //找到返回该元素的迭代器，未找到则返回迭代器end()
if(m.find("Hello")!=m.end())
```

**访问**

```c++
cout << m["hello"] <<endl; //访问map中key为"hello"的value，如果key不存在则返回0
```

**判断存在**

```c++
m[num] == 0 //说明num这个值在map中不存在
```

**输出“键”和“值”**

```c++
// 用迭代器遍历，输出map中所有的元素，键⽤it->first获取，值⽤it->second获取
for (auto it = m.begin(); it != m.end(); it++)
{
	cout << it->first << " " << it->second << endl;
}
```

**遍历`map`元素**

```c++
for (auto it = s.begin(); it != s.end(); it++)
{
    //遍历输出<键,值>的“值”
    cout << it->second << endl;
    cout << *it.second << endl;
}
```

**自定义`map`排序**

1. 按键排序

   ```c++
   //默认从小到大排序
   template <class T> struct less : binary_function <T,T,bool> {  
     bool operator() (const T& x, const T& y) const  
       {return x<y;}  
   };
   
   //从大到小排序
   template <class T> struct greater : binary_function <T,T,bool> {  
     bool operator() (const T& x, const T& y) const  
       {return x>y;}  
   };  
   map<string,int,greater<string>>
   
   //自定义排序
   struct comLen{
        bool operator(const string &lhs, const string &rhs)
        {return lhs.length()<rhs.length();}
   }
   map<string,int,comLen> LenLessMap;
   ```

2. 按值排序

   ```c++
   //借助sort、vector、pair实现对map的按值排序
   //其实可以用 结构体+sort+自定义排序
   #include<bits/stdc++.h>
   using namespace std;
   bool cmp(pair<int,int> p1,pair<int,int> p2)//按值从小到大排，值相同按键从小到大排
   {
       if(p1.second==p2.second)
           return p1.first<p2.first;
       else return p1.second<p2.second;
   }
   int main()
   {
       int n;
       cin>>n;
       map<int,int>mp;
       int key,value;
       while(n--)
       {
           cin>>key>>value;
           mp[key]=value;
       }
       vector<pair<int,int>>vec(mp.begin(),mp.end());//mp存储到vector容器中
       sort(vec.begin(),vec.end(),cmp);//sort只能排序线性容器
       for(auto it=vec.begin();it!=vec.end();it++)
       {
           cout<<it->first<<' '<<it->second<<endl;
       }
       return 0;
   }
   ```

**unordered_map**

`unordered_map`在头⽂件`#include <unordered_map>`中，`map`会按照键值对的键`key`进⾏排序，⽽`unordered_map`省去了这个排序的过程

------



## 对组`Pair`

`pair`是将2个数据组合成一组数据

- `stl`中的`map`就是将`key`和`value`放在一起来保存
- 当一个函数需要返回2个数据的时候，可以选择`pair`

pair类型定义在`#include <utility>`头文件中

```c++
pair<T1, T2> p1;            //创建一个空的pair对象（使用默认构造），它的两个元素分别是T1和T2类型，采用值初始化。
pair<T1, T2> p1(v1, v2);    //创建一个pair对象，它的两个元素分别是T1和T2类型，其中first成员初始化为v1，second成员初始化为v2。
make_pair(v1, v2);          // 以v1和v2的值创建一个新的pair对象，其元素类型分别是v1和v2的类型。
p1 < p2;                    // 两个pair对象间的小于运算，其定义遵循字典次序：如 p1.first < p2.first 或者 !(p2.first < p1.first) && (p1.second < p2.second) 则返回true。
p1 == p2；                  // 如果两个对象的first和second依次相等，则这两个对象相等；该运算使用元素的==操作符。
p1.first;                   // 返回对象p1中名为first的公有数据成员
p1.second;                 // 返回对象p1中名为second的公有数据成员

//pair类型的使用相当的繁琐，如果定义多个相同的pair类型对象，可以使用typedef简化声明
typedef pair<string,string> Author;
Author proust("March","Proust");
Author Joy("James","Joy");
```

------



## 栈 `stack`

`#include <stack>`

**定义**

```c++
stack<int> s;
```

**判空**

```c++
s.empty(); //返回栈是否为空
```

**大小**

```c++
s.size(); //返回栈大小
```

**压栈**

```c++
s.push(i); //将元素压入栈s中
```

**移除**

```c++
s.pop(); //移除栈顶元素
```

**访问栈顶**

```c++
s.top(); //访问s的栈顶元素
```



## 队列 `queue`

`#include <queue>`

**定义**

```c++
queue<int> q;
```

**判空**

```c++
q.empty(); //返回队列是否为空
```

**大小**

```c++
q.size(); //返回队列大小
```

**入队**

```c++
q.push(i); //元素i入队
```

**移除**

```c++
q.pop(); //移除队列的队首元素
```

**访问队首和队尾**

```c++
cout << q.front() << ' ' << q.back() << endl; //输出队首和队尾
```

模拟循环队列，`queue`的队首元素弹出队列后，再次将其压入队列尾部。



## 优先队列 `priority_queue`

`#include <queue>`

**定义**

```c++
priority_queue<int> pq;
```

**判空**

```c++
pq.empty(); //返回队列是否为空
```

**大小**

```c++
pq.size(); //返回队列大小
```

**入队**

```c++
pq.push(i); //元素i入队
```

**出队**

```c++
pq.pop(); //最大值出队
```

**访问**

```c++
pq.top(); //访问当前队列中优先级最高的元素（值最大的元素）
```

**优先度低的先输出**

```c++
priority_queue<int,vector<int>,greater<int>> pq; //优先度低的先输出（e.g.h）
```

------

## 结构体 `struct`

在结构体声明的大括号后面必须有一个分号。

```c++
// e.g.树的结点
struct Node {
    Node* left, * right;
    int data;
    Node(int d) :data(d), left(nullptr), right(nullptr) {}	// 快捷构造函数
};
```

```c++
// 构造函数
struct Employee
{
    string name;    // 员工姓名
    int vacationDays,    // 允许的年假
    daysUsed;    //已使用的年假天数
    Employee (string n ="",int d = 0)    // 构造函数
    {
        name = n;
        vacationDays = 10;
        daysUsed = d;
    }
};
```

------



# 实用函数



## `memset`、`fill`（数组填充）

 **`memset` 函数**

`memset`是计算机中`C/C++`语言初始化函数。作用是将某一块内存中的内容全部设置为指定的值（二进制补码）， 这个函数通常为新申请的内存做初始化工作。

**使用方法：**`memset`函数按字节对内存块进行初始化，所以不能用它将`int`数组初始化为0和-1之外的其他值（除非该值高字节和低字节相同）。

```c++
//（1）赋值为-1
memset(q,-1,sizeof(q));
memset(q,255,sizeof(q));
memset(q,0xff,sizeof(q));

//（2）赋值为0
memset(q,0,sizeof(q));

// 如果想要赋1
char q[100];
memset(q,'1',sizeof(q));
```

**`fill`**

```c++
// 给q数组的q[0],q[1],q[2]赋值为5
fill(q,q+3,5);
//填充二维数组
fill(a, a + MAXN * MAXN, 1);
```

头文件：`#include <algorithm>`

格式：fill(初始位置first，最终位置last，值)   //填充范围为`[first,last)`

 (备注：fill大家在竞赛中使用较少，原因不详，据说是速度太慢。)

------



## `bitset`（二进制、位运算）

`bitset`⽤来处理⼆进制位⾮常⽅便。头⽂件是`#include <bitset>`，`bitset`可能在PAT、蓝桥OJ中不常⽤，但是在LeetCode OJ中经常⽤到。⽽且知道`bitset`能够简化⼀些操作，可能⼀些复杂的问题能够直接用`bitset`就很轻易地解决。以下是⼀些常用用法：

```c++
#include <iostream> 
#include <bitset> 
using namespace std; 
int main() { 
    bitset<5> b("11"); //5表示5个二进位 
    // 初始化方式： 
    // bitset<5> b; 都为0 
    // bitset<5> b(u); u为unsigned int，如果u = 1，则输出b的结果为00001 
    // bitset<8> b(s); s为字符串，如"1101"，则输出b的结果为00001101，在前.补0 
    // bitset<5> b(s, pos, n); 从字符串的s[pos]开始，n位长度 

    // 注意，bitset相当于一个数组，但是它是从二进制的低位到高位分别为b[0]、b[1]……的 
    // 所以按照b[i]方式逐位输出和直接输出b结果是相反的 
    cout << b << endl; // 如果bitset<5> b("11"); 则此处输出00011(即正常二进制顺序) 
    for(int i=0; i<5; i++) 
    	cout << b[i]; // 如果bitset<5> b("11"); 则此处输出11000(即正常二进制顺序的倒序) 

    cout << endl << b.any(); //b中是否存在1的二进制位 
    cout << endl << b.none(); //b中不存在1吗？ 
    cout << endl << b.count(); //b中1的二进制位的个数 
    cout << endl << b.size(); //b中二进制位的个数 
    cout << endl << b.test(2); //测试下标为2处是否二进制位为1 
    b.set(4); //把b的下标为4处置1 
    b.reset(); //所有位归零 
    b.reset(3); //b的下标3处归零 
    b.flip(); //b的所有.进制位逐位取反 
    unsigned long a = b.to_ulong(); //b转换为unsigned long类型 
    return 0; 
} 
```

------



## `sort`(排序)

sort函数在头文件`#include <algorithm>`，主要是对一个数组进行排序（ `int arr[]`数组或者`vector`数组都行），`vector`是容器，要用`v.begin()`和`v.end()`表示头尾；而`int arr[]`用`arr`表示数组的首地址，`arr+n`表示尾部

**sort + vector**

```c++
sort(v.begin(), v.end()); //默认从小到大排序
```

**sort + int arr[]**

```c++
sort(arr, arr + 10, cmp); //根据cmp函数规则排序
```

**自定义cmp函数的sort排序**

当比较函数的返回值为`true`时，表示的是比较函数的第一个参数将会排在第二个参数前面

```c++
bool cmp(stu a, stu b) { // cmp函数，返回值是bool，传入的参数类型应该是结构体stu类型 
    if (a.score != b.score) // 如果学生分数不同，就按照分数从大到小排列 
    	return a.score > b.score; 
    else // 如果学生分数相同，就按照学号从小到大排列 
    	return a.number < b.number; 
} 

// 有时候这种简单的if-else语句我喜欢直接用一个C语言里面的三目运算符表示 
bool cmp(stu a, stu b) { 
	return a.score != b.score ? a.score > b.score : a.number < b.number; 
} 
```

> 注意：`sort`函数的`cmp`必须按照规定来写，即必须只是`>`或者`<`，比如：`return a>b;`或者`return a<b;`而不能是`<=`或者`>=`，因为快速排序的思想中，`cmp`函数是当结果为`false`的时候迭代器指针暂停开始交换两个元素的位置，当`cmp`函数`return a<=b`时，若中间元素前面的元素都比它小，而后面的元素都跟它相等或者比它小，那么`cmp`恒返回`true`，迭代器指针会不断右移导致程序越界，发生段错误。

------



## `reverse`（反转）

```c++
// 1.翻转字符串
reverse(s.begin(),s.end());   //翻转整个字符串
reverse(s.begin()+i,s.begin()+k);   //翻转下标i到k（不包含k）
// 2.翻转数组
reverse(a,a+n);		//n为数组长度    翻转整个数组
reverse(a+i,a+k);	//翻转指定范围 下标为i到k（不包括k）
// 3.翻转vector
reverse(vect.begin(),vect.end());//写法和数组一样
```

------



## `swap`（交换）

`#include <algorithm>`

```c++
// This program demonstrates the use of the swap function template.
#include <iostream>
#include <string>
#include <algorithm> // Needed for swap
using namespace std;

int main ()
{
    // Get and swap two chars
    char firstChar, secondChar;
    cout << "Enter two characters: ";
    cin >> firstChar >> secondChar;
    swap(firstChar, secondChar);
    cout << firstChar << " " << secondChar << endl;
    // Get and swap two ints
    int firstInt, secondInt;
    cout << "Enter two integers: ";
    cin >> firstInt >> secondInt;
    swap(firstInt, secondInt);
    cout << firstInt << " " << secondInt << endl;
    // Get and swap two strings
    cout << "Enter two strings: ";
    string firstString, secondString;
    cin >> firstString >> secondString;
    swap(firstString, secondString);
    cout << firstString << " " << secondString << endl;
    return 0;
}
```

```out
Enter two characters: a b
b a
Enter two integers: 12 45
45 12
Enter two strings: http://c.biancheng.net cyuyan
cyuyan http://c.biancheng.net
```

------



## `next_permutation`（全排列）

`next_permutation()`会取得`[first,last)`所标示之序列的下一个排列组合，如果没有下一个排列组合，便返回`false`否则返回`true`。

```c++
// 输入任意一个字符串，输出其字典序的全排列
int main(int argc, char** argv) {
	string str;
	cin>>str;
	sort(str.begin(),str.end());
	do{
		cout<<str<<endl;
	}while(next_permutation(str.begin(),str.end()));
    // for(s.begin(); next_permutation(s.begin(), s.end());)
	return 0;
}
```

> 类似还有`prev_permutation`取得上一个排列组合

------



## `cctype`里的函数（判断类型、大小写转换）

**判断类型**

`#include <cctype>(ctype.h)`中的函数可以判断数字、小写字母、大写字母等，常用的如下:

`isalpha()` 字母（包括大写、小写）

`isdigit()` 数字（0－9）

`islower()` 小写字母

`isupper()` 大写字母

`isalnum()` 字母大写小写+数字

`isblank()` `space` 和 `\t` 

`isspace()` `space`、`\t`、`\r`、`\n`

参数如果为XXX，则返回`true`。

------

**大小写转换**

`cctype`中除了上述所说的用来判断某个字符是否是某种类型，还有两个经常用到的函数： `tolower`和`toupper`，作用是将某个字符转为小写或者大写，这样就不用像原来那样手动判断字符c是否是大写，如果是大写字符就`c = c + 32;`的方法将`char c`转为小写字符啦。这在字符串处理的题目中也是经常.到：

```c++
char c = 'A'; 
char t = tolower(c); // 将c字符转化为小写字符赋值给t，如果c本身就是小写字符也没有关系 
cout << t; // 此处t为'a' 
```

`toupper()`函数用来将小写字母转换为大写字母。只有当参数 c 是一个小写字母，并且存在对应的大写字母时，这种转换才会发生。

在默认情况下，小写字母包括：

```
a b c d e f g h i j k l m n o p q r s t u v w x y z
```

大写字母包括：

```
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
```

**参数**

要转换的字符。它可以是一个有效的字符（被转换为 int 类型），也可以是 EOF（表示无效的字符）。

**返回值**

如果转换成功，那么返回与 c 对应的大写字母；如果转换失败，那么直接返回 c（值未变）。

注意，返回值为 int 类型，你可能需要隐式或者显式地将它转换为 char 类型。

**声明**

```c++
int tolower(int c);
int toupper(int c);
```

**例子**

```c++
#include <stdio.h>
#include <ctype.h>
 
int main(void)
{
    char ch = 'A';
    ch = tolower(ch);
    printf("ch=%c\n",ch);
 
    ch = 'b';
    ch = toupper(ch);
    printf("ch=%c\n",ch);
 
    return 0;
}
```

------



## `auto` 和 迭代器

**auto**

`auto`相当于`vector<int>::iterator`的简写

```c++
for(auto it = c.begin(); it != c.end(); it++)
{
    cout << *it << ' ';
}
```

迭代器访问`vector`、`set`、`map`等，**`c.begin()`**是一个指针，指向容器的**第一个元素**；**`c.end()`**指向容器的**最后一个元素的后一个位置**，所以迭代器指针`it`的`for`循环判断条件是`it != c.end()`。访问元素的值要对`it`指针取值，要在前面加星号，所以是`cout << *it;`

------



## 基于范围的 `for` 循环

除了像C语言的`for`语句`for (i = 0; i < arr.size(); i++)`这样，C++11标准还为C++添加了一种新的`for`循环方式，叫做基于范围（range-based）的`for`循环，这在遍历数组中的每一个元素时使用会比较简便。如想要输出数组`arr`中的每一个值，可以使用如下的方式输出： 

```c++
int arr[4] = {0, 1, 2, 3}; 
for (int i : arr) 
	cout << i << endl; // 输出数组中的每一个元素的值，每个元素占据一行 
```

`i`变量从数组的第一个元素开始，不断执行循环，`i`依次表示数组中的每一个元素，注意，使`int i`的方式定义时，该语句只能用来输出数组中元素的值，而不能修改数组中的元素，如果想要修改，必须使`int &i`这种定义引用变量的方式。如想给数组中的每一个元素都乘以 2，可以使用如下方式：

```c++
int arr[4] = {0, 1, 2, 3}; 
for (int &i : arr) // i为引用变量 
	i=i*2; // 将数组中的每一个元素都乘以2，arr[4]的内容变为了{0, 2, 4, 6} 
```

这种基于范围的`for`循环适用于各种类型的数组，将上述两段代码中的`int`改成其他变量类型如`double`、`char`都是可以的。另外，这种`for`循环方式不仅可以适用于数组，还适用于各种STL容器，比如`vector`、`set`等。加上上面一节所讲的C++11里面很好用的`auto`声明，将`int`、`double`等变量类型替换成`auto`，用起来就更方便啦。 

```c++
// v是.个int类型的vector容器 
 
for (auto i : v) 
	cout<<i<<" "; 
// 上面的写法等价于 
for (int i = 0; i < v.size(); i++) 
	cout << v[i] << " "; 
```

------



## `to_string`（数字转字符串）

`#include <string>`，`to_string`最常用的就是把一个`int`型变量或者一个数字转化为`string`类型的变量，当然也可以转`double`、`float`等类型的变量。

```c++
string s1 = to_string(123);
string s2 = to_string(4.5);
```

------



## `stoi`、`stod`（字符串转数字）

使用`stoi`、`stod`可以将字符串`string`转化为对应的`int`型、`double`型变量。

```c++
string str = "123";
int a = stoi(str);
str = "123.44";
double b = stod(str);
```

> stoi如果遇到的是非法输⼊（比如stoi("123.4")，123.4不是⼀个int型变量）：
>
> 1. 会自动截取最前面的数字，直到遇到不是数字为止(所以说如果是浮点型，会截取前⾯的整数部分)
> 2. 如果最前⾯不是数字，会运行时发生错误

> stod如果是非法输⼊：
>
> 1.	会自动截取最前面的浮点数，直到遇到不满足浮点数为止
> 2.	如果最前面不是数字或者小数点，会运行时发生错误
> 3.	如果最前面是小数点，会自动转化后在前⾯补0

不仅有`stoi`、`stod`两种，相应的还有：

`stof` (string to float)

`stold` (string to long double)

`stol` (string to long)

`stoll` (string to long long)

`stoul` (string to unsigned long)

`stoull` (string to unsigned long long)

------



# 实用算法

## 辗转相除法

欧几里得算法又称辗转相除法，是指用于计算两个非负整数a，b的**最大公约数**。
$$
gcd(a,b) = gcd(b,a mod b)
$$

```c++
int gcd(int a, int b)
{
    if (a % b==0) return b;
    else return gcd(b, a % b);
}
```

> **最小公倍数**：
> $$
> lcm(a,b)=a*b/gcd(a,b)
> $$

------
## 二分查找

```c++
int left = 0, right = nums.size() - 1;
        while(left <= right){
            int mid = (right - left) / 2 + left;
            int num = nums[mid];
            if (num == target) {
                return mid;
            } else if (num > target) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
```
------
## 素数筛法

找到一个素数，将它的所有倍数均标记成非素数。

```c++
const int MAXN =10001;
vector<int> prime;	//保存质数
bool isPrime[MAXN];	//标记数组
void Initial(){
	for(int i = 0; i < MAXN; ++i){
		isPrime[i] = true;	//初始化
	}
    // fill(isPrime,isPrime+MAXN,true);
	isPrime[0] = false;
	isPrime[1] = false;
	for(int i=2; i < MAXN; ++i){
		if(!isPrime[i]){	//非质数则跳过
			continue;
		}
		prime.push_back(i);
		for(int j = i * i; j < MAXN; j += i){	//因为i*k（i>k）必定在求得k的某个素因数（必定小于i）时被标记过
            //为防止溢出，可以改写成 for(int j = i ; j < MAXN / i ; j += i)
			isPrime[j] = false;	//质数的倍数为非质数
		}
	}
	return;
}
```

------

## 约数的个数

一个数约数的个数等于它的各个 **质因数** 的 **指数+1** 的乘积。
$$
x=p_1^{e_1}*p_2^{e_2}...p_n^{e_n}
$$

$$
w(x)=(e_1+1)(e_2+1)...(e_n+1)
$$

```c++
// prime[]是质数数组
cin>>n;
int ans=1;
for(int i=0;i<prime.size()&&prime[i]<=n;i++)
{
    int factor=prime[i];
    int ex=0; //ex是指数的个数
    while(n%factor==0)
    {
        ex++;
        n/=factor;
    }
    ans*=ex+1; //（指数+1）的累乘
}
if(n>1)
    ans*=2;
cout<<ans<<endl;
```

------

## 快速幂

```c++
int FastExponentiation(int a, int b){
	int answer = 1;	//初始化为1
    while(b != 0){	//不断将b转换为二进制数
        if(b % 2 == 1){	//若当前位为1，累乘a的2^k次幂
            answer *= a; //mul(ans,a)
        }
        b /= 2;
        a *= a;	//a不断平方 mul(a,a)
    }
    return answer;
}
```

------

## 最大连续子序列和

```c++
//动态规划
const int MAXN = 1000000;
long long arr[MAXN];
long long dp[MAXN]; //dp表示以A[i]作为末尾的连续序列的最大和

long long MaxSubsequence(int n){
	long long maximum = 0;
	for(int i = 0; i < n; ++i){
		if(i == 0){
			dp[i] = arr[i]; //只有一个元素
		} else{
			dp[i] = max(arr[i], dp[i - 1] + arr[i]); //多个元素
		}
		maximum = max(maximum, dp[i]); //最大连续子序列就是dp中的最大值
	}
	return maximum;
}
```

------

## 循环位移

实现对一个无符号数的循环左移和循环右移

```c++
//val表示需要移位的数 n表示移位位数
//字节数乘以8代表一共多少位
//向右循环移n位的结果：假设数据一共size位，向左移size-n位，再与原数右移n位进行或操作的结果
uint32 bit_move(uint32 val, int n) {
	uint32 size = sizeof(val) * 8;
	n = n % size;
	//return (val >> (size - n) | (val << n));//左移
	return (val << (size - n) | (val >> n));//右移
}
```

------

## 树的遍历

**前序遍历（PreOrder）**

```c++
// 递归
void PreOrder(Node* root){
    if(root==NULL){
        return;
    }
    Visit(root->data);
    PreOrder(root->left);
    PreOrder(root->right);
    return;
}
```

**中序遍历（InOrder）**

```c++
// 递归
void InOrder(Node* root){
    if(root==NULL){
        return;
    }
    InOrder(root->left);
    Visit(root->data);
    InOrder(root->right);
    return;
}
```

**后序遍历（PostOrder）**

```c++
// 递归
void PostOrder(Node* root){
    if(root==NULL){
        return;
    }
    PostOrder(root->left);
    PostOrder(root->right);
    Visit(root->data);
    return;
}
```

**层次遍历（LevelOrder）**

```c++
// 队列
void LevelOrder(Node* root)
{
    queue<Node*> myQueue;
    if(root!=NULL){
        myQueue.push(root);
    }
    while(!myQueue.empty()){
        Node* current=myQueue.front();
        myQueue.pop();
        visit(current->data);
        if(current->left!=NULL){
            myQueue.push(current->left);
        }
        if(current->right!=NULL){
            myQueue.push(current->right);
        }
    }
    return;
}
```

------

## 建树

**二叉树递归建树**

```c++
// 建树：ABC##DE#G##F### 其中“#”表示的是空格，空格字符代表空树
Node* Build(int& position,string s)	// position是整形引用
{
    char c=s[position++];	// 获取当前字符
    if(c=='#')
        return nullptr;
    Node* root=new Node(c);	// 创建新结点
    root->left=Build(position,s);	// position是切分点
    root->right=Build(position,s);
    return root;
}
```

**二叉排序树递归插入建树**

```c++
// 二叉排序树递归插入
Node* Insert(Node* root, int x)
{
    if (root == nullptr)	// 根结点为空，创建新结点
        root = new Node(x);
    else if (x < root->data)	// 递归插入左结点
        root->left = Insert(root->left, x);
    else if (root->data < x)	//递归插入右结点
        root->right = Insert(root->right, x);
    return root;
}
```

------

## 并查集

```c++
const int MAXN = 1000;
int father[MAXN];
int height[MAXN];

// 初始化
void Initial(int n) {
    for (int i=0; i < n; i++) {
        father[i] = i;
        height[i] = 0;
    }
    return;
}

// 查找
int Find(int x) {
    if (x != father[x]) {
        father[x] = Find(father[x]);
    }
    return father[x];
}

// 合并
void Union(int x, int y) {
    x = Find(x);
    y = Find(y);
    if (x != y) {
        if (height[x] < height[y]) {
            father[x] = y;
        } else if (height[x] > height[y]) {
            father[y] = x;
        } else {
            father[y] = x;
            height[x]++;	// 唯一的高度加一
        }
        //father[x] = y;
    }
}
```

**连通分量**

```c++
int N,M;	// N是点，M是边
while(cin >> N >> M) {
    Initial(N);
    int res=0;	// 连通分量个数
    if(N == 0)
        return 0;
    while (M--) {
        int x, y;
        cin >> x >> y;
        Union (x, y);	// 边的两端并入同一组
    }
    for(int i = 1; i <= N; i++)
        if(i == father[i])
            res++;
}
```

**Kruskal算法**

```c++
// 定义边
struct Edge {
    int from;
    int to;
    int length;
    bool operator< (const Edge& e) const {
        return length < e.length;
    }
};

// 边的数组
Edge edge[MAXN * MAXN];

// Kruskal算法
int Kruskal(int n, int edgeNumber) {
    Initial(n);
    sort(edge, edge + edgeNumber);	// 边从小到大排序
    int sum = 0;
    for (int i = 0; i < edgeNumber; i++) {
        Edge current = edge[i];
        if (Find(current.from) != Find(current.to)) {	// 边的两端不在同一组
            Union(current.from, current.to);	// 把边的两端并入同一组
            sum += current.length;
        }
    }
    return sum;
}
```



------



## 动态规划

1. **递推求解**

2. **最大连续子序列和**

3. **最长递增子序列**

4. **最长公共子序列**

   ```c++
   // 字符串1  a b c d e f g
   // 字符串2  a b c d e f g
   //  下 标  0 1 2 3 4 5 6 7
   // s[1]对应b, dp[1][1]对应[a][a] 
   #include<bits/stdc++.h>
   using namespace std;
   const int MAXN=110;
   string s1,s2;
   int dp[MAXN][MAXN]={0};	// dp[i][j]是指[下标i前][下标j前]的最长公共子序列长度
   int main(){
       while (cin >> s1 >> s2) {
           int n = s1.size();
           int m = s2.size();
           for(int i = 0; i <= n; i++) {
               for(int j = 0; j <= m; j++){
                   if (i == 0 || j == 0){	// 边界情况初始化
                       dp[i][j] = 0;
                       continue;
                   }
                   if (s1[i - 1] == s2[j - 1])	// dp的下标应当比s大1
                       dp[i][j] = dp[i - 1][j - 1] + 1;
                   else
                       dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
               }
           }
           cout << dp[n][m] <<endl;
       }
   }
   ```

5. **背包问题**

   [点菜问题](D:\ysy\机试练习\牛客网\点菜问题（01背包）)

6. **其他问题**

   [放苹果](D:\ysy\机试练习\牛客网\放苹果（经典dp）)

   [整数拆分](D:\ysy\机试练习\牛客网\整数拆分（dp）)

------



# 其他

## 二分查找的范围

防止整形最大值相加溢出

```c++
int middle = left + (right - left)/2
```

------

## 大整数的运算

`C++`和`C`需要自己定义大整数型，`Java`需要`import`，`python`没有这个问题

```python
# 大整数相加
while True:
    try:
        a, b = map(int, input().split()) # python以字符串形式读入
        print(a + b)
    except:
        break
```

**`python` 计算阶乘**

```python
# N的阶乘
while True:
    try:
        answer=1
        n=int(input())
        for i in range(1,n+1):
            answer*=i
        print(answer)
    except:
        break
```

**`python`超大整数的计算**

```python
a=pow(10,100)
b=pow(10,100)
print(a)
print(a//3)
print(a//(b//3))
```

```python
10000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
3333333333333333333333333333333333333333333333333333333333333333333333333333333333333333333333333333
3
```

------

## 最大最小整数

`C++`中常量`INT_MAX`和`INT_MIN`分别表示最大、最小整数，定义在头文件`limits.h`中。

```c++
#define INT_MAX 2147483647
#define INT_MIN (-INT_MAX - 1)
```

------

## 重载运算符

```c++
struct Complex{
    int real,imag;
    Complex(int a,int b):real(a),imag(b){}
    bool operator< (Complex c) const{	// 为复数运算重载运算符
        return real*real+imag*imag<c.real*c.real+c.imag*c.imag;
    }
};
```

------

