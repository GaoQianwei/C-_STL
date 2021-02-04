# STL_常用的算法

### 一、常用的查找算法

#### adjacent_find()

adjacent_find(iterator beg, iterator end, _callback);

在iterator对标识元素范围内，查找一对相邻重复元素，找到则返回指向这对元素的第一个元素的迭代器。

```cpp
	vector<int> vecInt;
	vecInt.push_back(1);
	vecInt.push_back(2);
    vecInt.push_back(2);
    vecInt.push_back(4);
    vecInt.push_back(5);
	vecInt.push_back(5);
	vector<int>::iterator it = adjacent_find(vecInt.begin(), vecInt.end()); 
    //*it = 2
```



#### binary_search（）

bool binary_search(iterator beg, iterator end, value);

在有序序列中查找value,找到则返回true。注意：在无序序列中，不可使用。

```cpp
	set<int> setInt;
	setInt.insert(3);
    setInt.insert(1);
	setInt.insert(7);
	setInt.insert(5);
	setInt.insert(9);
	bool bFind = binary_search(setInt.begin(), setInt.end(), 5);//nFind=true
```



#### count() 

count(iterator beg, iterator end, value);

利用等于操作符，把标志范围内的元素与输入值比较，返回相等的个数。

```cpp
vector<int> vecInt;
vecInt.push_back(1);
vecInt.push_back(2);
vecInt.push_back(2);
vecInt.push_back(4);
vecInt.push_back(2);
vecInt.push_back(5);
int iCount = count(vecInt.begin(),vecInt.end(),2);  //iCount==3
```

​    

#### count_if() 

count_if(首迭代器，未迭代器，搜索值（要比较的值的结果）)(条件计数)

```cpp
//假设vector<int> vecIntA，vecIntA包含1,3,5,7,9元素

//先定义比较函数
bool GreaterThree(int iNum){
     if(iNum>=3){
     	return true;
     }
     else{
	    return false;
     }
} 

int iCount = count_if(vecIntA.begin(), vecIntA.end(), GreaterThree);
//此时iCount == 4
```



#### find() 

find(iterator beg, iterator end, value)

find: 利用底层元素的等于操作符，对指定范围内的元素与输入值进行比较。当匹配时，结束搜索，返回该元素的迭代器。 

```cpp
vector<int> vecInt;
vecInt.push_back(1);
vecInt.push_back(3);
vecInt.push_back(5);
vecInt.push_back(7);
vecInt.push_back(9);

vector<int>::iterator it = find(vecInt.begin(), vecInt.end(), 5);        //*it == 5
```



#### find_if() 

find_if(iterator beg, iterator end, _callback);（条件查找）

find_if:  使用输入的函数代替等于操作符执行find。返回被找到的元素的迭代器。

```cpp
//假设vector<int> vecIntA，vecIntA包含1,3,5,3,9元素 
vector<int>::it = find_if(vecInt.begin(),vecInt.end(),GreaterThree);
//此时 *it==3, *(it+1)==5, *(it+2)==3, *(it+3)==9 
```



### 二、常用的排序算法

#### merge() 

以下是排序和通用算法：提供元素排序策略

merge:  合并两个有序序列，存放到另一个序列。

```cpp
//例如：vecIntA,vecIntB,vecIntC是用vector\<int>声明的容器，vecIntA已包含1,3,5,7,9元素，vecIntB已包含2,4,6,8元素
vecIntC.resize(9); //扩大容量
merge(vecIntA.begin(),vecIntA.end(),vecIntB.begin(),vecIntB.end(),vecIntC.begin());
//此时vecIntC就存放了按顺序的1,2,3,4,5,6,7,8,9九个元素
```



#### sort() 

sort: 以默认升序的方式重新排列指定范围内的元素。若要改排序规则，可以输入比较函数。

```cpp
//学生类
Class CStudent:
{
public:
    CStudent(int iID, string strName)
    {
		m_iID=iID; 
		m_strName=strName; 
	}
public:      
    int m_iID;
    string m_strName;
}

//学号比较函数
bool Compare(const CStudent &stuA,const CStudent &stuB)
{
	return (stuA.m_iID<strB.m_iID);
}
void main()
{
    vector<CStudent> vecStu;
    vecStu.push_back(CStudent(2,"老二"));
	vecStu.push_back(CStudent(1,"老大"));
	vecStu.push_back(CStudent(3,"老三"));
	vecStu.push_back(CStudent(4,"老四"));
	sort(vecStu.begin(),vecStu.end(),Compare);
	// 此时，vecStu容器包含了按顺序的"老大对象","老二对象","老三对象","老四对象"
}
```



#### random_shuffle() 

random_shuffle:   对指定范围内的元素随机调整次序。

```cpp
srand(time(0));             //设置随机种子
vector<int> vecInt;
vecInt.push_back(1);
vecInt.push_back(3);
vecInt.push_back(5);
vecInt.push_back(7);
vecInt.push_back(9);
string str("itcastitcast ");
random_shuffle(vecInt.begin(), vecInt.end());  //随机排序，结果比如：9,7,1,5,3
random_shuffle(str.begin(), str.end());        //随机排序，结果比如：" itstcasticat "
```



#### reverse()

reverse：反转指定范围的元素

```cpp
vector<int> vecInt;
vecInt.push_back(1);
vecInt.push_back(3);
vecInt.push_back(5);
vecInt.push_back(7);
vecInt.push_back(9);
reverse(vecInt.begin(), vecInt.end());       //{9,7,5,3,1}
```



### 三、常用的拷贝和替换算法

#### copy() 

copy算法 将容器内指定范围的元素拷贝到另一容器中

```cpp
vector<int> vecIntA;
vecIntA.push_back(1);
vecIntA.push_back(3);
vecIntA.push_back(5);
vecIntA.push_back(7);
vecIntA.push_back(9);
vector<int> vecIntB;
vecIntB.resize(5);           //扩大空间
copy(vecIntA.begin(), vecIntA.end(), vecIntB.begin());  //vecIntB: {1,3,5,7,9}
```



#### replace() 

replace(beg,end,oldValue,newValue):  将指定范围内的所有等于oldValue的元素替换成newValue。

```cpp
vector<int> vecIntA;
vecIntA.push_back(1);
vecIntA.push_back(3);
vecIntA.push_back(5);
vecIntA.push_back(3);
vecIntA.push_back(9);
replace(vecIntA.begin(), vecIntA.end(), 3, 8);     //{1,8,5,8,9}
```



#### replace_if() 

```cpp
/*
	replace_if算法 将容器内指定范围满足条件的元素替换为新元素
	@param beg 容器开始迭代器
	@param end 容器结束迭代器
	@param callback函数回调或者谓词(返回Bool类型的函数对象)
	@param oldvalue 新元素
*/
replace_if(iterator beg, iterator end, _callback, newvalue)
```

replace_if : 将指定范围内所有操作结果为true的元素用新值替换。

```cpp
//把大于等于3的元素替换成8
vector<int> vecIntA;
vecIntA.push_back(1);
vecIntA.push_back(3);
vecIntA.push_back(5);
vecIntA.push_back(3);
vecIntA.push_back(9);
replace_if(vecIntA.begin(), vecIntA.end(), GreaterThree, 8);     // GreaterThree的定义在上面。
```



#### swap() 

swap:  交换两个容器的元素

```cpp
vector<int> vecIntA;
vecIntA.push_back(1);
vecIntA.push_back(3);
vecIntA.push_back(5);
vector<int> vecIntB;
vecIntB.push_back(2);
vecIntB.push_back(4);
swap(vecIntA, vecIntB); //交换
```



### 四、常用的算术和生成算法

#### accumulate() 

accumulate: 对指定范围内的元素求和，然后结果再加上一个由val指定的初始值。

#include\<numeric>

```cpp
vector<int> vecIntA;
vecIntA.push_back(1);
vecIntA.push_back(3);
vecIntA.push_back(5);
vecIntA.push_back(7);
vecIntA.push_back(9);
int iSum = accumulate(vecIntA.begin(), vecIntA.end(), 100);     //iSum==125
```



#### fill() 

fill:  将输入值赋给标志范围内的所有元素。

```cpp
vector<int> vecIntA;
vecIntA.push_back(1);
vecIntA.push_back(3);
vecIntA.push_back(5);
vecIntA.push_back(7);
vecIntA.push_back(9);
fill(vecIntA.begin(), vecIntA.end(), 8);       //8, 8, 8, 8, 8
```



### 五、常用的集合算法

#### set_union(),set_intersection(),set_difference()

set_union: 构造一个有序序列，包含两个有序序列的并集。

set_intersection: 构造一个有序序列，包含两个有序序列的交集。

set_difference: 构造一个有序序列，该序列保留第一个有序序列中存在而第二个有序序列中不存在的元素。

```cpp
vector<int> vecIntA;
vecIntA.push_back(1);
vecIntA.push_back(3);
vecIntA.push_back(5);
vecIntA.push_back(7);
vecIntA.push_back(9);
 
vector<int> vecIntB;
vecIntB.push_back(1);
vecIntB.push_back(3);
vecIntB.push_back(5);
vecIntB.push_back(6);
vecIntB.push_back(8);

vector<int> vecIntC;
vecIntC.resize(10);

//并集
set_union(vecIntA.begin(), vecIntA.end(), vecIntB.begin(), vecIntB.end(), vecIntC.begin());       
//vecIntC : {1,3,5,6,7,8,9,0,0,0}

//交集
fill(vecIntC.begin(),vecIntC.end(),0);
set_intersection(vecIntA.begin(), vecIntA.end(), vecIntB.begin(), vecIntB.end(), vecIntC.begin());   
//vecIntC: {1,3,5,0,0,0,0,0,0,0}

//差集
fill(vecIntC.begin(),vecIntC.end(),0);
set_difference(vecIntA.begin(), vecIntA.end(), vecIntB.begin(), vecIntB.end(), vecIntC.begin());     
//vecIntC: {7,9,0,0,0,0,0,0,0,0}
```



### 六、常用的遍历算法 

#### for_each() 

```cpp
/*
    遍历算法 遍历容器元素
	@param beg 开始迭代器
	@param end 结束迭代器
	@param _callback  函数回调或者函数对象
	@return 函数对象
*/
for_each(iterator beg, iterator end, _callback);
```

for_each: 用指定函数依次对指定范围内所有元素进行迭代访问。该函数不得修改序列中的元素。

```cpp
void show(const int &iItem){
    cout << iItem;
}

main()
{
    int iArray[] = {0,1,2,3,4};
    vector<int> vecInt(iArray,iArray+sizeof(iArray)/sizeof(iArray[0]));
	for_each(vecInt.begin(), vecInt.end(), show);
//结果打印出0 1 2 3 4
} 
```



#### transform() 

```cpp
/*
	transform算法 将指定容器区间元素搬运到另一容器中
	注意 : transform 不会给目标容器分配内存，所以需要我们提前分配好内存
	@param beg1 源容器开始迭代器
	@param end1 源容器结束迭代器
	@param beg2 目标容器开始迭代器
	@param _cakkback 回调函数或者函数对象
	@return 返回目标容器迭代器
*/
transform(iterator beg1, iterator end1, iterator beg2, _callbakc)
```

transform:  与for_each类似，遍历所有元素，但可对容器的元素进行修改

```cpp
int increase (int i){ 
    return i+1;  
} 
main()
{
	vector<int> vecIntA;
    vecIntA.push_back(1)；
    vecIntA.push_back(3);
	vecIntA.push_back(5);
    vecIntA.push_back(7);
    vecIntA.push_back(9);

    transform(vecIntA.begin(),vecIntA.end(),vecIntA.begin(),increase);   
    //vecIntA : {2,4,6,8,10}
}
```

 