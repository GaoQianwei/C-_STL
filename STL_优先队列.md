# STL_优先队列

### 一、简介

优先队列容器与队列一样，只能从队尾插入元素，从队首删除元素。但是它有一个特性，就是队列中最大的元素总是位于队首，所以出队时，并非按照先进先出的原则进行，而是将当前队列中最大的元素出队。

元素的比较规则默认按元素值由大到小排序，可以重载“<”操作符来重新定义比较规则。

优先级队列可以用向量(vector)或双向队列(deque)来实现

```
priority_queue<vector<int>, less<int> > pq1; 　　　 // 使用递增less<int>函数对象排序
priority_queue<deque<int>, greater<int> > pq2; 　　// 使用递减greater<int>函数对象排序
```

### 二、基本操作

\#include \<queue>

| 函数接口   |                          功能                          |
| ---------- | :----------------------------------------------------: |
| empty()    |                 如果队列为空，则返回真                 |
| pop()      |              删除对顶元素，删除第一个元素              |
| push(elem) |                      加入一个元素                      |
| size()     |              返回优先队列中拥有的元素个数              |
| top()      | 返回优先队列对顶元素，返回优先队列中有最高优先级的元素 |

### 三、代码示例

```cpp
#include <iostream>
using namespace std;
#include <queue> 

void main()
{

    priority_queue<int> p1; //默认是 最大值优先级队列 

    //priority_queue<int, vector<int>, less<int> > p1**; //相当于这样写

    priority_queue<int, vector<int>, greater<int>> p2; //最小值优先级队列

    p1.push(33);
    p1.push(11);
    p1.push(55);
    p1.push(22);
    cout <<"队列大小" << p1.size() << endl;
    cout <<"队头" << p1.top() << endl;

    while (p1.size() > 0)
    {
         cout << p1.top() << " ";
         p1.pop();
    }
    cout << endl;

    cout << "测试 最小值优先级队列" << endl;
    p2.push(33);
    p2.push(11);
    p2.push(55);
    p2.push(22);
    while (p2.size() > 0)
    {
         cout << p2.top() << " ";
         p2.pop();
    }
}
/*
队列大小4
队头55
55 33 22 11
测试 最小值优先级队列
11 22 33 55
*/
```

