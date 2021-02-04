# STL_map和multimap容器

### 一、map/multimap的简介

map是标准的**关联式**容器，一个map是一个键值对序列，即(key,value)对。它提供基于key的快速检索能力。

map中**key**值是唯一的**。集合中的元素按一定的顺序**排列。元素插入过程是按排序规则插入，所以不能指定插入位置。

map的具体实现采用红黑树变体的平衡二叉树的数据结构，在插入操作和删除操作上比vector快。

map可以直接存取key所对应的value，支持[]操作符，如map[key]=value。

multimap与map的区别：map支持唯一键值，每个键只能出现一次；而multimap中相同键可以出现多次。multimap不支持[]操作符。

#include \<map> 

​                           

### 二、map/multimap对象的默认构造

map/multimap采用模板类实现，对象的默认构造形式：

- map<T1,T2> mapTT; 
- multimap<T1,T2> multimapTT; 

```cpp
map<int, char> mapA;
map<string,float> mapB;
//其中T1,T2还可以用各种指针类型或自定义类型
```



### 三、map的插入与迭代器

map.insert(...);  //往容器插入元素，返回pair<iterator,bool>

假设map<int, int> mymap，在map中插入元素的方式：

1. 通过pair的方式插入对象：mymap.insert(pair<int, int>(10, 10));

2. 通过pair的方式插入对象：mymap.insert(make_pair(20, 20));

3. 通过value_type的方式插入对象：mymap.insert(map<int, int>::value_type(30, 30));

4. 通过数组的方式插入值：mymap[40] = 40。

```cpp
//map容器模板参数，第一个参数key的类型，第二参数value类型
	map<int, int> mymap;

	//插入数据  pair.first key值 piar.second value值
	//第一种
	pair<map<int, int>::iterator, bool> ret = mymap.insert(pair<int, int>(10, 10));
	//第二种
	mymap.insert(make_pair(20, 20));
	//第三种
	mymap.insert(map<int, int>::value_type(30, 30));
	//第四种，发现如果key不存在，创建pair插入到map容器中；如果发现key存在，那么会修改key对应的value。
	mymap[40] = 40;
	mymap[10] = 20;
	mymap[50] = 50;

	for (map<int, int>::iterator it = mymap.begin(); it != mymap.end(); it++) {
		cout << "key:" << (*it).first << " value:" << it->second << endl;
	}
/*
结果：
key:10 value:20
key:20 value:20
key:30 value:30
key:40 value:40
key:50 value:50
*/
```

前三种方法，采用的是insert()方法，该方法返回值为pair<iterator,bool>

```cpp
	pair<map<int, int>::iterator, bool> ret = mymap.insert(pair<int, int>(10, 10));
	if (ret.second) {
		cout << "第一次插入成功!" << endl;
	}
	else {
		cout << "插入失败!" << endl;
	}
/*
结果：
第一次插入成功!
*/
```

第四种方法非常直观，但存在一个性能的问题。插入3时，先在mapStu中查找主键为3的项，若没发现，则将一个键为3，值为初始化值的对组插入到mapStu中，然后再将值**修改**。若发现已存在3这个键，则修改这个键对应的value。  

map<T1,T2,less\<T1> > mapA; //该容器是按键的升序方式排列元素。未指定函数对象，默认采用less\<T1>函数对象。

map<T1,T2,greater\<T1>> mapB;  //该容器是按键的降序方式排列元素。

less\<T1>与greater\<T1> 可以替换成其它的函数对象functor。

可编写自定义函数对象以进行自定义类型的比较，使用方法与set构造时所用的函数对象一样。

 

### 四、map对象的拷贝构造与赋值

map(const map &mp);         //拷贝构造函数

map& operator=(const map &mp);    //重载等号操作符

map.swap(mp);                //交换两个集合容器       

```cpp
map<int, string> mapA;
mapA.insert(pair<int,string>(3,"小张"));
mapA.insert(pair<int,string>(1,"小杨"));    
mapA.insert(pair<int,string>(7,"小赵"));    
mapA.insert(pair<int,string>(5,"小王"));    
map<int ,string> mapB(mapA);            //拷贝构造
map<int, string> mapC;
mapC = mapA;                              //赋值
mapC[3] = "老张";
mapC.swap(mapA);         //交换
```



### 五、map的大小

map.size(); //返回容器中元素的数目

map.empty();//判断容器是否为空         

```cpp
map<int, string> mapA;
mapA.insert(pair<int,string>(3,"小张"));    
mapA.insert(pair<int,string>(1,"小杨"));    
if (mapA.empty())
{
   int iSize = mapA.size();       //iSize == 4
}
```



### 六、map的删除

map.clear();        //删除所有元素

map.erase(pos); //删除pos迭代器所指的元素，返回下一个元素的迭代器。

map.erase(beg,end);   //删除区间[beg,end)的所有元素 ，返回下一个元素的迭代器。

map.erase(keyElem);   //删除容器中key为keyElem的对组。

```cpp
map<int, string> mapA;
mapA.insert(pair<int,string>(3,"小张"));   
mapA.insert(pair<int,string>(1,"小杨"));   
mapA.insert(pair<int,string>(7,"小赵"));   
mapA.insert(pair<int,string>(5,"小王"));    
 //删除区间内的元素
map<int,string>::iterator itBegin=mapA.begin();
++ itBegin;
++ itBegin;

map<int,string>::iterator itEnd=mapA.end();
mapA.erase(itBegin,itEnd);         //此时容器mapA包含按顺序的{1,"小杨"}{3,"小张"}两个元素。

mapA.insert(pair<int,string>(7,"小赵"));    
mapA.insert(pair<int,string>(5,"小王"));    

//删除容器中第一个元素
mapA.erase(mapA.begin());  //此时容器mapA包含了按顺序的{3,"小张"}{5,"小王"}{7,"小赵"}三个元素

//删除容器中key为5的元素
mapA.erase(5);  

//删除mapA的所有元素
mapA.clear();          //容器为空
```



### 七、map的查找

map.find(key);  //查找键key是否存在，若存在，返回该键的元素的迭代器；若不存在，返回map.end();

map.count(keyElem);  //返回容器中key为keyElem的对组个数。对map来说，要么是0，要么是1。对multimap来说，值可能大于1。

map.begin(); //返回容器中第一个数据的迭代器。

map.end(); //返回容器中最后一个数据之后的迭代器。

map.rbegin(); //返回容器中倒数第一个元素的迭代器。

map.rend();  //返回容器中倒数最后一个元素的后面的迭代器。

map.lower_bound(keyElem); //返回第一个key>=keyElem元素的迭代器。

map.upper_bound(keyElem);   // 返回第一个key>keyElem元素的迭代器      

map.equal_range(keyElem);       //返回容器中key与keyElem相等的上下限的两个迭代器。上限是闭区间，下限是开区间，如[beg,end)。

```cpp
	map<int, int> mymap;
	mymap.insert(make_pair(1, 4));
	mymap.insert(make_pair(2, 5));
	mymap.insert(make_pair(3, 6));

	pair<map<int, int>::iterator, map<int, int>::iterator> ret = mymap.equal_range(2);
	if (ret.first != mymap.end()) {
		cout << "找到lower_bound！" << endl;
	}
	else {
		cout << "没有找到";
	}

	if (ret.second != mymap.end()) {
		cout << "找到upper_bound！" << endl;
	}
	else {
		cout << "没有找到";
	}
/*
结果：
找到lower_bound！
找到upper_bound！
*/
```

