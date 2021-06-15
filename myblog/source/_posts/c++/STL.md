---
title: STL
date: 2021-05-20 00:14:09
tags:
- c++
category : 
- c++

---
# 容器
## map
```
#include<iostream>
#include<map>
#include<string>
using namespace std;

int main(){
    map<int,string> m;

    //迭代器
    cout << "iterator:" << endl;
    map<int,string>::iterator it;
    m[1] = "123";
    it = m.begin();
    cout << it->first << " " << it->second << endl;//迭代器first对应key  second对应value

    //插入
    cout << "insert:" << endl;
    m[1] = "123";//数组方式写数据对
    m.insert(pair<int,string> (2,"456"));//插入数据对，若存在key则不能插入
    m.insert(map<int,string>::value_type(3,"789"));//同上

    //查找
    cout << m[1] << endl;//索引找值，不存在则返回对应类的初始值
    cout << m.find(1)->second << endl;//通过key找迭代器  找不到则返回end迭代器

    //删除
    cout << "delete:" << endl;
    m.erase(m.begin(),m.end());//删除begin到end之间的元素，end删除则表示删除单个元素
    m.clear();//清空所有元素

    //其他属性
    m[1]="123";
    m[2]="456";
    cout << "others:" << endl;
    cout << m.size() << endl;//返回元素个数
    cout << m.max_size() << endl;//返回可容纳的最大个数
    cout << m.empty() << endl;//返回是否为空，为空则返回true
    map<int,string>::reverse_iterator rit = m.rend();//返回反向迭代器
    it = m.upper_bound(0);//返回第一个大于0的元素的迭代器,找不到返回end
    it = m.lower_bound(0);//同上  大于等于 同func.cpp中用法
    it = m.equal_range(0).first;//返回lower
    it = m.equal_range(0).second;//返回upper，都是二分查找
    getchar();
    return 0;
}
```

## stack&queue

```
#include<iostream>
#include<stack>
#include<queue>
using namespace std;
void stk();
void que();
int main(){
    stk();
    que();
    getchar();
    return 0;
}
void stk(){
    int a=0,n=1;
    stack<int> s,s2;//声明栈
    s.push(a);
    cout << "stack:" << endl;
    s.push(a);//栈顶压入a  无返回值
    s.pop();//弹出栈顶元素  无返回值
    cout << s.top() << endl;//返回栈顶元素 不会删除栈顶元素 注意判断是否为空
    cout << s.empty() << endl;//判断是否为空栈 空栈返回true
    cout << s.size() << endl;//返回栈中元素个数
    s.emplace(a);//栈顶加入元素，可直接写构造函数参数 内部构造,如下  队列同理
    stack<string> s1;
    s1.emplace(3,'a');
    cout << s1.top() << endl;
    s.swap(s2);//交换两个栈的内容，队列同理
}
void que(){
    queue<int> q,q2;//声明队列
    int a=0;
    q.push(a);
    q2.push(a);
    cout << "queue:" << endl;
    q.push(a);//队尾增加元素
    q.emplace(a);//队尾增加元素，可直接写对象的构造函数参数，在内部构造
    q.pop();//删除队首元素
    cout << q.empty() << endl;//判断是否为空队列  空队列返回true
    cout << q.size() << endl;//返回队列元素个数
    cout << q.front() << endl;//返回队首元素
    cout << q.back() << endl;//返回队尾元素
    q.swap(q2);//交换q和q2
}
```

## string
```
//学习链接“https://blog.csdn.net/tengfei461807914/article/details/52203202”
#include<iostream>
#include<string>
#include<cstring>
using namespace std;

int main(){
    char ch[]={"world!"};
    cout << sizeof(ch) << endl;
    string s1="Hello ",s2=ch,s("ssss");//初始化，用字符串或字符数组直接赋值或者利用构造函数直接赋值
    s=s1+s2;//直接将s2接在s1后面
    cout << s << endl;//输出应为“Hello world！”
    cout << s.front() << s.back() << endl;//返回第一个/最后一个元素 类似与栈顶的作用
    cout << "length:" << s.size() << endl;//获取s的长度  不包括 '\0'
    cout << "cstring:" << s.c_str() << " length:" << strlen(s.c_str()) << endl;//返回包括'\0'的字符数组

    //begin(),end()
    string::iterator be = s.begin(),en = s.end();//返回s的头尾迭代器

    //substr
    cout << "substr():" << endl;
    s="012345";
    int begin=0,end=3,a=0,n=1;
    cout << s.substr(a) << endl;//返回从a到尾部的string类型
    cout << s.substr(a,n) << " : " << s.substr(0,8) << endl;
    //返回从a开始长度为n的string  如果a+n大于总长度 会抛出out_of_range异常，但运行时返回从a到尾部的string类型
    //cout << s.substr(s.begin(),s.end());不可以用迭代器

    //insert,返回插入后的string
    cout << "insert():" << endl;
    cout << s.insert(begin,s1) << endl; // 在begin处插入s1(可用cstr代替) 原begin处接到尾部s1尾部
    cout << s.insert(begin,s1,a,n) << endl;//在begin处插入s1中从a开始长度为n的string
    cout << s.insert(begin,"hello",n) << endl;//在begin处插入cstr从头开始的n个字符
    cout << s.insert(begin,n,'a') << endl;//在begin处插入n个a
    string::iterator it = s.insert(s.begin(),'a');//在迭代器处插入字符，返回一个指向插入位置的迭代器
    cout << *it << endl;
    it = s.insert(s.begin(),n,'b');//在迭代器处插入n个字符，返回指向插入位置的迭代器
    cout << *it << endl;
    it = s.insert(s.begin(),s1.begin(),s1.end());//在s.begin中插入从s1.begin()到s1.end()的字符串，返回插入位置的迭代器
    cout << *it << endl;

    //erase
    cout << "erase():" << s << endl;
    cout << s.erase(a,n) << endl;//删除s从a处开始的n个字符,返回删除后的string
    it = s.erase(s.begin()+5);//删除迭代器对应位置的字符,返回删除前参数迭代器指向
    cout << *it << " " << s << endl;
    it = s.erase(s.begin()+1,s.end());//删除迭代器到迭代器中间的字符,不包括后迭代器指向的位置,返回删除前的s.begin()+1迭代器
    cout << *it << " " << s << endl;

    //append
    s = s1;
    cout << "append():" << endl;
    cout << s.append(s2) << endl;//直接追加s2，可用cstr和形参代替
    cout << s.append(s2,a,n) << endl;//追加s2第a个开始的n个字符
    cout << s.append("123456",n) << endl;//追加形参的n个字符
    cout << s.append(n,'.') << endl;//追加n个char
    cout << s.append(be,en) << endl;//追加be迭代器到en迭代器的字符不包括en
    cout << s.append(n,56) << endl;//追加n个ascll码为56的字符
    cout << s.append(1,'1');
    s+="123";//函数重载为+

    //replace，可用迭代器代替用于表示位子的数字或数字组合
    s=s1;
    cout << "replace():" << endl;
    cout << s.replace(a,n,s2) << endl;//第a个后面的n-1个字符被s2代替，s2可用cstr和形参代替
    cout << s.replace(a,n,s2,a,n) << endl;//第a个后面的n-1个字符被s2的第a个字符后面的n-1个字符代替 可不等长
    cout << s.replace(a,n,"123",n) << endl;//第a个后面的n-1个字符被形参的前n个字符代替
    cout << s.replace(a,n,n,'a') << endl;//第a个后面的n-1个字符被n个ch代替

    //assign
    cout << "assign:" << endl;
    cout << s.assign(s1) << endl;//s赋值为s1  s1可用cstr和常量代替
    cout << s.assign(n,'a') << endl;//s赋值n个ch
    cout << s.assign(s1.begin(),s1.end()) << endl;//begin迭代器到end迭代器的值赋给s

    //find/rfind,rfind用法同find  结果返回最后一个位置
    cout << "find/rfind:" << endl;
    s= s1;
    cout << s.find(s1) << " " << s.find(s2) << endl;//找到s1第一次在s中出现的位置，不存在则返回结尾std::string:npos，s1可用cstr、常量和字符代替
    cout << s.find(ch,a,n) << endl;//从a处开始找常量或ch的前n个字符,返回同上

    //find_of  返回同find
    cout << "find_of:" << endl;
    cout << s.find_first_of(s1) << endl;//找到s1中任何一个字符第一次出现的位置
    cout << s.find_first_not_of(s1) << endl;//找到第一个不在s1中出现过的字符
    cout << s.find_last_of(s1) << endl;//找到任何一个字符最后一次出现的位置
    cout << s.find_last_not_of(s1) << endl;//找到最后一个不在s1中出现的字符 的位置

    //比较与转换
    s="123";
    n=10;
    cout << "compare and transfer:" << endl;
    cout << s.compare(a,n,s1,a,n) << endl;//s从a起第n-1个字符与s1从a起底n-1个字符比较，相等为0，s>s1返回1 否则返回-1  a、n组合均可删除
    cout << to_string(n) << endl;//n转化为string  n支持多种类型
    cout << stoi(s,0,n) << endl;//s从0开始转化为n进制 i:int  l:long ul:unsigned long   ll::long long  ull::u longlong  f::float  d:double  ld:long double

    getchar();
    return 0;
    
}
```

## vector
```
#include<iostream>
#include<vector>

using namespace std;

int main(){
    int n=5,a=1;
    vector<int> v(n,a);//构造含有n个a的vector,a，n均可根据情况删除
    vector<int> v1(v);//赋值v到v1
    vector<int> v2(v.begin(),v.end());//赋值begin到end之间的元素到v2 不包括右边界
    //增加元素
    cout << "add element: " << endl;
    v.push_back(a);//尾部增加元素a
    cout << *v.insert(v.begin(),n,a+1) << endl;//在迭代器处插入n个a  n可省，返回插入位置迭代器
    cout << *v.insert(v.begin(),v1.begin(),v1.end()) << endl;//在迭代器位置处插入begin到end间的元素
    cout << *v.emplace(v.begin(),5) << endl;//在迭代器前插入单个元素

    //减少元素
    cout << "delete element: " << endl;
    v.pop_back();//删除最后一个元素
    cout << *v.erase(v.begin()+1,v.end()-1) << endl;//删除迭代器到迭代器间的元素,后者可删除
    v1.clear();//清空元素

    //访问元素
    cout << "get element:" << endl;
    v.assign(n,a);
    cout << v.at(n-1) << endl;//返回位置n-1的元素
    cout << v.front() << " " << v.back() << endl;//返回开头和结尾的元素
    cout << *v.begin() << *v.end() << endl;//返回头尾迭代器
    cout << *v.rbegin() << *v.rend() << endl;//返回反向迭代器

    //大小
    cout << "size:" << endl;
    cout << v.empty() << endl;//判断是否为空，空则返回true
    cout << v.size() << v.max_size() << v.capacity() << endl;//分别返回向量元素个数、最大可允许个数、当前所能容纳最大个数

    //其他
    cout << "others:" << endl;
    v.swap(v1);//交换所有元素
    v.assign(n,a);//设置前n个元素为a
    v.assign(v1.begin(),v1.end());//设置为
    cout << v[0] << endl;
    getchar();
    return 0;
}
```

# 迭代器
```
#include<iostream>
#include<string>
#include<vector>
#include<deque>
#include<list>
#include<set>
#include<map>
using namespace std;
int main(){
    string s="Hello world!";
    string::iterator it;//声明随机访问迭代器  容器类型::iterator 
    string::const_iterator c_it;//const类型迭代器
    string::reverse_iterator r_it;//反向迭代器
    string::const_reverse_iterator c_r_it;//常量反向迭代器
    it = s.begin();//初始化迭代器
    it++;//令迭代器指向下一个元素
    cout << *it << " " << *(it+2) << " " << it[2] << endl;//it指向对应字符 类似指针

    //可用迭代器：随机访问迭代器可事项双向迭代器所有功能，且可随机访问容器的任何位置 双向迭代器支持--和++操作  单项迭代器只支持++
    string::iterator strit;//随机访问迭代器
    vector<int>::iterator vit;//随机访问迭代器
    deque<int>::iterator qit;//随机访问迭代器
    list<int>::iterator lit;//双向迭代器
    set<int>::iterator sit;//双向迭代器
    map<int,int>::iterator mit;//双向迭代器

    //迭代器辅助函数
    string::iterator p1,p2;
    int n=2;
    p1 = s.begin();
    p2 = s.end();
    advance(p1,n);//迭代器向前或向后移动n个元素
    cout << distance(p1,p2) << endl;//返回p1需要经过多少次++才能等于p2  如果p1在p2后面则会死循环
    iter_swap(p1,p2);//交换p1 和p2
    getchar();
    return 0;
}
```

# 算法
```
#include<iostream>
#include<algorithm>
#include<map>
#include<vector>
#include<string>
#include<random>
#include<time.h>
using namespace std;

int main(){
    string s="123";
    reverse(s.begin(),s.end());//#include<algorithm>  反转迭代间内容 不包括s.end()
    cout << s << endl;

    s="1234";
    cout << *lower_bound(s.begin(),s.end(),'2') << endl;//查找两个迭代器范围内第一个大于等于‘2’的元素
    cout << *upper_bound(s.begin(),s.end(),'2') << endl;//同上  大于  注意：本函数使用二分法，默认是有序排列的，所以可能出错
    cout << *equal_range(s.begin(),s.end(),'2').first << " " << *equal_range(s.begin(),s.end(),'2').second << endl;//找上述两个,lower先

    cout << max(0,1) << endl;//支持多种数据比较，返回最大值
    cout << min(0,1) << endl;//同上，返回最小值

    sort(s.begin(),s.end(),[](auto a,auto b){return a>b;});//从begin到end排序，第三个参数为排序方式，可以是函数名，不写默认升序
                                                           //也可以是实例中的函数形式 返回值为1取前一个数，否则取后一个数

    cout << s << endl;

    //随机产生浮点数#include<random>
    random_device rd;//随机种子
    mt19937 mt(rd());//伪随机数生成器，参数为种子
    uniform_real_distribution<> dis(1.0,2.0);//连续均匀分布，浮点类型
    cout << dis(mt) << endl;
    
    getchar();
    return 0;
}
```