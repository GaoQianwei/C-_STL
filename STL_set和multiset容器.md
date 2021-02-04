# STL_set和multiset容器

### 一、set/multiset的简介

set是一个**集合**容器，其中所包含的元素是**唯一**的，**集合中的元素按一定的顺序排列**。**元素插入过程是按排序规则插入**，所以不能指定插入位置。

set采用**红黑树**变体的数据结构实现，红黑树属于平衡二叉树。**在插入操作和删除操作上比vector快**。

set不可以直接存取元素。（不可以使用at.(pos)与[]操作符）。

multiset与set的区别：

- set支持唯一键值，**每个元素值只能出现一次**；
- multiset中**同一值可以出现多次**。

不可以直接修改set或multiset容器中的元素值，因为该类容器是自动排序的。如果希望修改一个元素值，必须先删除原有的元素，再插入新的元素。

#include \<set> 

​                               

### 二、set/multiset构造函数

set\<T> st;//set默认构造函数：

mulitset\<T> mst; //multiset默认构造函数

set(const set &st);         //拷贝构造函数

```cpp
set<int> setInt;      //一个存放int的set容器。
multiset<int> mulsetInt;      //一个存放int的multiset容器。
set<int> setIntB(setIntA); //1 3 5 7 9
```



### 三、set的插入与迭代器

set.insert(elem);   //在容器中插入元素。

set.begin(); //返回容器中第一个数据的迭代器。

set.end(); //返回容器中最后一个数据之后的迭代器。

set.rbegin(); //返回容器中倒数第一个元素的迭代器。

set.rend();  //返回容器中倒数最后一个元素的后面的迭代器。 

```cpp
set<int> setInt;
setInt.insert(3); 
setInt.insert(1);
setInt.insert(5);
setInt.insert(2);

for(set<int>::iterator it=setInt.begin(); it!=setInt.end(); ++it){

   int iItem = *it;
   cout << iItem;  //或直接使用cout << *it
}
//这样子便顺序输出 1 2 3 5(默认排序，从小到大)
```

 

### 四、set集合的元素排序

set<int,less\<int> > setIntA; //该容器是按升序方式排列元素。

set<int,greater\<int>> setIntB;  //该容器是按降序方式排列元素。

set\<int> 相当于 set<int,less\<int>>。

less\<int>与greater\<int>中的int可以改成其它类型，该类型主要要跟set容纳的数据类型一致。

```cpp
set<int,greater<int>> setIntB;
setIntB.insert(3);
setIntB.insert(1);
setIntB.insert(5);
setIntB.insert(2);
//此时容器setIntB就包含了按顺序的5,3,2,1元素
```



### 五、函数对象functor的用法

尽管函数指针被广泛用于实现函数回调，但C++还提供了一个重要的实现回调函数的方法，那就是函数对象。

functor，翻译成函数对象，伪函数，算符，是重载了“()”操作符的普通类对象。从语法上讲，它与普通函数行为类似。

greater<>与less<>就是函数对象。 

```cpp
//下面举出greater<int>的简易实现原理。
struct greater{
	bool operator() (const int& iLeft, const int& iRight){
   		return (iLeft>iRight);  //如果是实现less<int>的话，这边是写return (iLeft<iRight);
	}
}
//容器就是调用函数对象的operator()方法去比较两个值的大小。
```

 

### 六、set对象赋值

set& operator=(const set &st);    //重载等号操作符

set.swap(st);               //交换两个集合容器

```cpp
	set<int> setIntA;
	set<int> setIntC;
    
	setIntA.insert(3);
    setIntA.insert(1);
    setIntA.insert(7);
    setIntA.insert(5);
	setIntA.insert(9);    
    
    setIntC = setIntA;       //1 3 5 7 9 
    setIntC.insert(6);
    setIntC.swap(setIntA);    //交换
```



### 七、set的大小

set.size();  //返回容器中元素的数目

set.empty();//判断容器是否为空 

```cpp
set<int> setIntA;
setIntA.insert(3);
setIntA.insert(1);
setIntA.insert(7);
if (!setIntA.empty()){
   int iSize = setIntA.size();      //3
}
```



### 八、set的删除

set.clear();     //清除所有元素

set.erase(pos);  //删除pos迭代器所指的元素，返回下一个元素的迭代器。

set.erase(beg,end);    //删除区间[beg,end)的所有元素 ，返回下一个元素的迭代器。

set.erase(elem);   //删除容器中值为elem的元素。 

```cpp
//删除区间内的元素

//setInt是用set<int>声明的容器，现已包含按顺序的1,3,5,6,9,11元素。
set<int>::iterator itBegin=setInt.begin();
++ itBegin;
set<int>::iterator itEnd=setInt.begin();
++ itEnd;
++ itEnd;
++ itEnd;
setInt.erase(itBegin,itEnd);
//此时容器setInt包含按顺序的1,6,9,11四个元素。

//删除容器中第一个元素
setInt.erase(setInt.begin());       //6,9,11

//删除容器中值为9的元素
set.erase(9);   

//删除setInt的所有元素
setInt.clear();          //容器为空
```

 

### 九、set的查找

set.find(elem);  //查找elem元素，返回指向elem元素的迭代器；若不存在，返回set.end()

set.count(elem);  //返回容器中值为elem的元素个数。对set来说，要么是0，要么是1。对multiset来说，值可能大于1。

set.lower_bound(elem); //返回第一个>=elem元素的迭代器。

set.upper_bound(elem);    // 返回第一个>elem元素的迭代器。

set.equal_range(elem);       //返回容器中与elem相等的上下限的两个迭代器。上限是闭区间，下限是开区间，如[beg,end)。返回两个迭代器，而这两个迭代器被封装在pair中。

```cpp
	set<int> s1;
	s1.insert(7);
	s1.insert(2);
	s1.insert(4);
	s1.insert(5);
	s1.insert(1);

	set<int>::iterator ret = s1.find(14);
	if (ret == s1.end()) {
		cout << "没有找到!" << endl;
	}
	else {
		cout << "ret:" << *ret << endl;
	}

	//找第一个大于等于key的元素
	ret = s1.lower_bound(2);
	if (ret == s1.end()) {
		cout << "没有找到!" << endl;
	}
	else {
		cout << "ret:" << *ret << endl;
	}

	//找第一个大于key的值
	ret = s1.upper_bound(2);
	if (ret == s1.end()) {
		cout << "没有找到!" << endl;
	}
	else {
		cout << "ret:" << *ret << endl;
	}

	//equal_range 返回Lower_bound 和 upper_bound值
	pair<set<int>::iterator, set<int>::iterator> myret = s1.equal_range(2);
	if (myret.first == s1.end()) {
		cout << "没有找到！" << endl;
	}
	else {
		cout << "myret:" << *(myret.first) << endl;
	}

	if (myret.second == s1.end()) {
		cout << "没有找到！" << endl;
	}
	else {
		cout << "myret:" << *(myret.second) << endl;
	}
/*
结果：
没有找到!
ret:2
ret:4
myret:2
myret:4
*/
```

 