# STL_list容器

### 一、List简介

链表是一种物理存储单元上非连续、非顺序的存储结构，数据元素的逻辑顺序是通过链表中的指针链接次序实现的。

链表由一系列结点（链表中每一个元素称为结点）组成，结点可以在运行时动态生成。每个结点包括两个部分：一个是存储数据元素的数据域，另一个是存储下一个结点地址的指针域。

相较于vector的连续线性空间，list的好处是每次插入或者删除一个元素，就是配置或者释放一个元素的空间。因此，list对于空间的运用有绝对的精准，一点也不浪费。而且，对于任何位置的元素插入或元素的移除，list永远是常数时间。

List和vector是两个最常被使用的容器。

list容器是一个**双向链表容器**，可高效地进行插入删除元素。

list不可以随机存取元素，所以不支持at.(pos)函数与[]操作符。

#include \<list> 

 <img src="C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210125101251344.png" alt="image-20210125101251344" style="zoom:50%;" />

### 二、list对象的默认构造

list采用采用模板类实现,对象的默认构造形式：list\<T> LIST; 如：

```cpp
list<int> lstInt;      //定义一个存放int的list容器。
list<float> lstFloat;   //定义一个存放float的list容器。
list<string> lstString;   //定义一个存放string的list容器。              
//尖括号内还可以设置指针类型或自定义类型。
```



### 三、list头尾的添加移除操作

list.push_back(elem);      //在容器尾部加入一个元素

list.pop_back();       //删除容器中最后一个元素

list.push_front(elem);   //在容器开头插入一个元素

list.pop_front();       //从容器开头移除第一个元素

```cpp
	list<int> lstInt;
	lstInt.push_back(1);
	lstInt.push_back(3);
	lstInt.push_back(5);
	lstInt.push_back(7);
	lstInt.push_back(9);
	lstInt.pop_front();
	lstInt.pop_front();
	lstInt.push_front(11);
	lstInt.push_front(13);
	lstInt.pop_back();
	lstInt.pop_back();
// lstInt    {13,11,5}
```



### 四、list的数据存取

list.front();  //返回第一个元素。

list.back(); //返回最后一个元素。

```cpp
	list<int> lstInt;
	lstInt.push_back(1);
	lstInt.push_back(5);
	lstInt.push_back(9);

	int iFront = lstInt.front();	//1
	int iBack = lstInt.back();		//9
```



### 五、list与迭代器

list.begin();           //返回容器中第一个元素的迭代器。

list.end();            //返回容器中最后一个元素之后的迭代器。

list.rbegin();     //返回容器中倒数第一个元素的迭代器。

list.rend();     //返回容器中倒数最后一个元素的后面的迭代器。

```cpp
for (list<int>::iterator it=lstInt.begin(); it!=lstInt.end(); ++it)	{
		cout << *it<<cout << " ";
	}
```



### 六、list对象的带参数构造

list(beg,end);  //构造函数将[beg, end)区间中的元素拷贝给本身。注意该区间是左闭右开的区间。

list(n,elem);  //构造函数将n个elem拷贝给本身。

list(const list &lst); //拷贝构造函数。 

```cpp
	list<int> mlist1;
	list<int> mlist2(10, 10); //有参构造
	list<int> mlist3(mlist2);//拷贝构造
	list<int> mlist4(mlist2.begin(), mlist2.end());

	for (list<int>::iterator it = mlist4.begin(); it != mlist4.end(); it++) {
		cout << *it << " ";
	}
	cout << endl;
/*
结果：
10 10 10 10 10 10 10 10 10 10
*/
```



### 七、list的赋值

list.assign(beg,end);  //将[beg, end)区间中的数据拷贝赋值给本身。注意该区间是左闭右开的区间。

list.assign(n,elem); //将n个elem拷贝赋值给本身。

list& operator=(const list &lst); //重载等号操作符

list.swap(lst); // 将lst与本身的元素互换。

```cpp
	list<int> lstIntA,lstIntB,lstIntC,lstIntD;
	lstIntA.push_back(1);
	lstIntA.push_back(5);
	lstIntA.push_back(9);

	lstIntB.assign(lstIntA.begin(),lstIntA.end());		//1 5 9
	lstIntC.assign(5,8);							//8 8 8 8 8
	lstIntD = lstIntA;							//1 5 9
	lstIntC.swap(lstIntD);						//互换
```

 

### 八、list的大小

list.size();    //返回容器中元素的个数

list.empty();      //判断容器是否为空

list.resize(num);  //重新指定容器的长度为num，若容器变长，则以默认值填充新位置。如果容器变短，则末尾超出容器长度的元素被删除。

list.resize(num, elem); //重新指定容器的长度为num，若容器变长，则以elem值填充新位置。如果容器变短，则末尾超出容器长度的元素被删除。

```cpp
	list<int> lstIntA;
	lstIntA.push_back(11);
	lstIntA.push_back(33);
	lstIntA.push_back(55);

	if (!lstIntA.empty())
	{
		int iSize = lstIntA.size();		//3
		lstIntA.resize(5);			//11 33 55 0 0
		lstIntA.resize(7,1);			//11 33 55 0 0 1 1
		lstIntA.resize(2);			//11 33
	}
```



### 九、list的插入

list.insert(pos,elem);  //在pos位置插入一个elem元素的拷贝，返回新数据的位置。

list.insert(pos,n,elem);  //在pos位置插入n个elem数据，无返回值。

list.insert(pos,beg,end);  //在pos位置插入[beg,end)区间的数据，无返回值。

```cpp
	list<int> lstA;
	list<int> lstB;

	lstA.push_back(1);
	lstA.push_back(5);
	lstA.push_back(9);

	lstB.push_back(2);
	lstB.push_back(6);

	lstA.insert(lstA.begin(), 11);		//{11, 1, 5, 9}
	lstA.insert(++lstA.begin(),2,33);		//{11,33,33,1,5,9}
	lstA.insert(lstA.begin() , lstB.begin() , lstB.end() );	//{2,6,11,33,33,1,5,9}
```



### 十、list的删除

list.clear();     //移除容器的所有数据

list.erase(beg,end); //**删除[beg,end)**区间的数据，返回下一个数据的位置。

list.erase(pos);  //删除pos位置的数据，返回下一个数据的位置。

lst.remove(elem);  //删除容器中所有与elem值匹配的元素。

```cpp
//删除区间内的元素
//lstInt是用list<int>声明的容器，现已包含按顺序的1,3,5,6,9元素。
list<int>::iterator itBegin=lstInt.begin();
++ itBegin;
list<int>::iterator itEnd=lstInt.begin();
++ itEnd;
++ itEnd;
++ itEnd;
lstInt.erase(itBegin,itEnd);
//此时容器lstInt包含按顺序的1,6,9三个元素。

//假设 lstInt 包含1,3,2,3,3,3,4,3,5,3，删除容器中等于3的元素的方法一
for(list<int>::iterator it=lstInt.being(); it!=lstInt.end(); )    //小括号里不需写  ++it
{
   if(*it == 3){
        it  =  lstInt.erase(it);       //以迭代器为参数，删除元素3，并把数据删除后的下一个元素位置返回给迭代器。
         //此时，不执行  ++it；  
   }
   else{
       ++it;
   }
}

//删除容器中等于3的元素的方法二
lstInt.remove(3);

//删除lstInt的所有元素
lstInt.clear();			//容器为空
```



### 十一、list的反序排列

lst.reverse();   //反转链表  

```cpp
	list<int> lstA;
	
	lstA.push_back(1);
	lstA.push_back(3);
	lstA.push_back(5);
	lstA.push_back(7);
	lstA.push_back(9);

	lstA.reverse();			//9 7 5 3 1
```

