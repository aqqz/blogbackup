---
title: STL常见容器用法
date: 2022-07-10 19:31:00
tags:
---

## vector

vector意为向量，可以理解为变长数组

1. vector定义

```cpp
#include<vector>
using namespace std;
vector<typename> name;
```

vector中存放的类型可以是基本数据类型char, int, double, struct，也可以是STL标准容器，例如vector, set, queue。如果typename也是一个STL容器，定义的时候需要在>>之间加空格，因为在C++11之前会被认为是右移运算符。

```c++
vector<int> name;
vector<double> name;
vector<vector<int> > name; 
```

2. vector元素的访问

(1) 通过下标访问

(2) 通过迭代器访问

迭代器类似指针, 定义
```cpp
vector<typename>:: iterator it;
```

通过迭代器访问vector元素
```cpp
#include<stdio.h>
#include<vector>
using namespace std;

vector<int> vi;
for(int i = 1;i<=5;i++)
{
    vi.push_back(i);
}

vector<int>:: iterator it = vi.begin();
for(int i = 0;i<vi.size();i++)
{
    printf("%d", *(it+i))
}
return 0;
```

begin()函数用于取vi元素的首地址，end()函数用于取尾元素的下一个地址

使用迭代器遍历的第二种方法
```cpp
for(vector<int>:: iterator it=vi.begin();it!=vi.end();it++)
{
    cout<<*it<<endl;
}
```

3. vector常用函数

(1) push_back() 向容器末尾添加一个元素

(2) pop_back() 删除容器末尾元素

(3) size() 范围容器内元素个数

(4) clear() 清空容器内元素

(5) insert(it, x) 向vector的任意迭代器it处插入一个元素x

(6) earse()

- earse(it) 除迭代器it位置的元素

- earse(first, last) 删除[first, last)区间内的元素

## set

set意为集合，是一个内部自动去重和有序的容器

1. 定义

```cpp
#include<set>
using namespace std;

set<typename> name;
```

2. set元素的访问

set只能通过迭代器访问，除了vector和string之外的STL容器都不能用*(it+N)访问

```cpp
set<int> st;
st.insert(2);
st.insert(5);
st.insert(2);
st.insert(3);
set<int>:: iterator it;

for(it=st.begin();it!=st.end();it++)
{
    cout<<*it<<endl; //2 3 5自动去重和排序
}
```

3. 常用函数

(1) insert(x) 把x插入容器，自动去重和排序，时间复杂度O(logN)

(2) find(value) 返回set中值为value的迭代器

(3) earse

- earse(it) 删除迭代器对应的值

- earse(value) 删除set中的value

- earse(first, last) 删除[first, last)区间内的元素

(4) size() 返回set内元素的个数

(5) clear() 清空set元素


## string

在C语言中，一般使用char str[]存放字符串，但是操作不方便，容易出错，为了编程者方便地对字符串进行操作，C++在STL中封装了string类型

1. string定义

```cpp
#include<string>
using namespace std;

string str; //定义，默认是""
string str = "abcd" //定义并初始化
```

2. 访问string中的内容

(1) 通过下标访问

(2) 通过迭代器访问
```cpp
for(string::iterator it = str.begin();it!=str.end();it++)
{
    cout<<*it<<endl;
}
```

3. 常用函数

(1) operator += 字符串拼接运算符

(2) compare operator 比较规则是字典序

(3) size()/length() 返回字符串的长度

(4) insert()

- insert(pos, string) 在pos位置插入字符串string
```cpp
string str = "abcxyz", str2 = "opq";
str.insert(3, str2); //abcopqxyz
```

- insert(it, it2, it3) it为源字符串的待插入位置，it2和it3为待插入字符串的首尾迭代器，表示[it2, it3)插入到it的位置
```cpp
string str = "abcxyz", str2 = "opq";
str.insert(str.begin()+3, str2.begin(), str2.end());
```

(5) earse()

- earse(it) 删除单个元素

- earse(first, last) 删除区间[first, last)内的元素

(6) clear() 清空字符串内元素

(7) substr(pos, len) 返回字符串从pos位置起，长度为len的子串
```cpp
string str = "Thank you for your smile.";
cout<<str.substr(0, 5); //Thank
cout<<str.substr(14, 4); //your
cout<<str.substr(19, 5); //smile
```

(8) string::npos 用于作为find函数失配时的返回值

(9) find()

- find(str2) 如果str2是当前字符串的字串，返回出现的首位置，否则返回string::npos

- find(str2, pos) 从当前字符串的pos位开始匹配str2，返回结果同上

(10) replace

- replace(pos, len, str2) 把当前字符串从pos位置开始len长度的字串替换为str2

- replace(it1, it2, str2) 把当前字符串位于迭代器[it1, it2)范围的字串替换为str2



## map

map意为映射，可以将任何基本类型映射到任何基本类型，比如将string映射到int，或者将STL容器映射到STL容器

1. map的定义

```cpp
#include<map>
using namespace std;

map<typename1, typename2> mp;
map<string, int> mp2; //建字符串到整形的映射
map<set<int>, string> mp3; //建立set容器到字符串的映射
```

2. map内元素的访问

(1) 通过下标访问
```cpp
int main()
{
    map<char, int> mp;
    mp['c'] = 20;// 建立'c' -> 20
    mp['c'] = 30;// 建立'c' -> 30 (20被覆盖)
    printf("%d", mp['c']); //30
    return 0;
}
```

(2) 通过迭代器访问 通过it->first访问map的key, 通过it->second访问map的value
```cpp
int main()
{
    map<char, int> mp;
    mp['m'] = 20;
    mp['r'] = 30;
    mp['a'] = 40;
    for(map<char, int>::iterator it=mp.begin();it!=mp.end();it++)
    {
        printf("%c, %d", it->first, it->second);
    }
}
```

map的key会按从小到大顺序排列，因为其内部也是基于红黑树实现的

3. 常用函数

(1) find(key) 返回键为key的映射的迭代器

(2) earse()

- earse(it) 删除迭代器it对应的键值对

- earse(key) 删除键为key对应的元素

- earse(first, last) 删除迭代器区间[first, last)内的键值对

(3) size() 返回map内键值对的数量

(4) clear() 清空map的元素

4. map的使用场景

- 需要建立字符或字符串与整数映射的题目

- 判断大整数或其他数据类型是否存在的题目，可以把map当做布尔数组使用

注：map的键和值是唯一的，如果需要一个键对应多个值，需要用multimap，另外C++11中还增加了unordered_map，用散列替代红黑树，只做映射不做排序，速度更快


## queue

queue意为队列，在STL中是一个先进先出的容器

1. queue定义
```cpp
#include<queue>
using namespace std;
queue<typename> q;
```

2. queue内元素的访问

队列只允许元素先进先出，即插入操作发生在队尾，删除操作发生在队头。STL中通过front()访问队头元素, back()访问队尾元素

```cpp
int main()
{
    queue<int> q;
    for(int i = 1;i<=5;i++)
    {
        q.push(i);
    }
    printf("%d, %d", q.front(), q.back());
}
```

3. 常用函数

(1) push(x)  x入队，插入队尾

(2) front(), back() 访问队头、队尾元素

(3) pop() 队头元素出队

(4) empty() 检测queue是否空，空返回true,不空返回false

(5) size() 返回queue内元素的个数

4. 主要用途

实现BFS时，可以通过STL提供的queue,避免自己实现队列遇到错误情况，简化代码

注：使用front()和pop()前，必须用empty()判断队列是否空，队列不空才能pop和取元素

## priority_queue

priority_queue意为优先队列，本质就是一个最大堆（默认）底层用堆实现。在优先队列中，队首元素一定是当前优先队列中优先级最高的那一个。

1. 定义
```cpp
#include<queue>
using namespace std;
priority_queue<typename> name;
```

2. 元素访问

通过top()访问堆顶元素，也就是优先级最高的元素
```cpp
int main()
{
    priority_queue<int> q;
    q.push(3);
    q.push(4);
    q.push(1);
    printf("%d", q.top()); //4
}
```

3. 常用函数

(1) push(x) x入队

(2) top() 返回堆顶元素

(3) pop() 弹出堆顶元素

(4) empty() 检测队列是否空

(5) size() 返回队列内元素的个数

4. priority_queue优先级设置

(1) 基本数据类型优先级设置
此处基本数据类型就是int, double, char等直接可用的数据类型，优先级队列对他们的设计原则是数字大的优先级高

```cpp
priority_queue<int, vector<int>, less<int> > q;//数字越大优先级越高（降序）
priority_queue<double, vector<double>, greater<double> > q2;//数字越小优先级越高（升序）
```

(2) 结构体类型优先级设置

定义表示水果的结构体，包含水果名称和价格两个成员
```cpp
struct fruit
{
    string name;
    int price;
};
```

希望水果价格高的优先级高，需要重载operator < 运算符

```cpp
struct fruit
{
    string name;
    int price;
    friend bool operator < (fruit f1, fruit f2) {
        return f1.price < f2.price; //内部按水果价格排序
    }
};

int main()
{
    priority_queue<fruit> q;
    struct fruit f1, f2, f3;
    f1.name = "桃子";
    f1.price = 3;
    f2.name = "梨子";
    f2.price = 4;
    f3.name = "苹果";
    f3.price = 1;
    q.push(f1);
    q.push(f2);
    q.push(f3);
    cout<<q.top().name<<q.top().price<<endl; //梨子 4
}
```

## stack
stack意为栈，是STL中一个后进先出的容器，插入和删除都在栈顶操作

1. 定义
```cpp
#include<stack>
using namespace std;
stack<typename> s;
```

2. 栈内部元素的访问

由于栈本身是一种后进先出的数据结构，在STL中只能通过top()来访问栈顶元素
```cpp
int main()
{
    stack<int> st;
    for(int i = 1;i<=5;i++)
    {
        st.push(i); // push顺序 1, 2, 3, 4, 5
    }
    printf("%d", st.top()); //5
    return 0;
}
```

3. 常用函数

(1) push(x) x入栈

(2) top() 取栈顶元素

(3) pop() 弹出栈顶元素

(4) empty() 判断栈是否空

(5) size() 返回栈内元素个数

4. 用途

stack用于模拟一些递归栈，用空间换取时间，避免递归层数过多导致的超时


## pair

pair可看作内部有两个元素的结构体，且两个元素的类型可指定
```cpp
struct pair
{
    typename1 first;
    typename2 second;
};
```

1. pair定义
```cpp
#include<map>
using namespace std;
pair<typename1, typename2> name;
```

如果想定义pair同时初始化，只需跟上一个小括号，里面填上两个待初始化的元素

```cpp
pair<string, int> p("haha", 5);
```

如果想在代码中临时定义pair,两种方法：

- 类型定义写在前面，后面用小括号
```cpp
pair<string, int> p("haha", 5);
```
- 使用自带的make_pair方法
```cpp
make_pair("haha", 5);
```


2. pair中元素的访问

pair中只有两个元素：first和second，按结构体方法去访问即可

```cpp
int main()
{
    pair<string, int> p;
    p.first = "haha";
    p.second = 5;
    cout<<p.first<<p.second<<endl;
    p = make_pair("xixi", 55);
    cout<<p.first<<p.second<<endl;
    p = pair<string, int>("heihei", 5);
    cout<<p.first<<p.second<<endl;
    return 0;
}
```

3. 用途

- 用来代替二元结构体及其构造函数，节省编码时间

- 作为map的键值对插入
```cpp
int main()
{
    map<string, int> mp;
    mp.insert(make_pair("heihei", 5));
    mp.insert(make_pair("haha", 10));
    for(auto iterator it = mp.begin();it!=mp.end();it++)
    {
        cout<<it->first<<" "<<it->second<<endl; //haha 10 heihei 5
    }
}
```