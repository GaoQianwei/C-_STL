# STL_函数对象、谓词、预定义函数对象、函数适配器

### 一、函数对象

重载函数调用操作符的类，其对象常称为函数对象（function object），即它们是行为类似函数的对象，也叫仿函数(functor),其实就是重载“()”操作符，使得类对象可以像函数那样调用。

注意:

1. 函数对象(仿函数)是一个类，不是一个函数。
2. 函数对象(仿函数)重载了”() ”操作符使得它可以像函数一样调用。

分类:假定某个类有一个重载的operator()，而且重载的operator()要求获取一个参数，我们就将这个类称为“一元仿函数”（unary functor）；相反，如果重载的operator()要求获取两个参数，就将这个类称为“二元仿函数”（binary functor）。

函数对象的作用:

STL提供的算法往往都有两个版本，其中一个版本表现出最常用的某种运算，另一版本则允许用户通过template参数的形式来指定所要采取的策略。

“在标准库中，函数对象被广泛地使用以获得弹性”，标准库中的很多算法都可以使用函数对象或者函数来作为自定的回调行为。

```cpp
#define _CRT_SECURE_NO_WARNINGS
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

struct MyPrint {
	MyPrint() {
		mNum = 0;
	}
	void operator()(int val) {
		mNum++;
		cout << val << endl;
	}
public:
	int mNum;
};

int num = 0; //真正开发中，尽量避免去使用全局变量，加锁解锁繁琐
void MyPrint02(int val) {
	num++;
	cout << val << endl;
}

void test01() {

	MyPrint print;
	print(10);
	//函数对象可以像普通函数一样调用
	//函数对象可以像普通函数那样接收参数
	//函数对象超出了函数的概念，函数对象可以保存函数调用的状态，避免使用全局变量
}

void test02() {

	vector<int> v;
	v.push_back(10);
	v.push_back(20);
	v.push_back(30);
	v.push_back(40);

	//计算函数调用次数
#if 0
	MyPrint02(10);
	MyPrint02(20);
	cout << num << endl;

	MyPrint print;
	print(10);
	print(20);
	cout << print.mNum << endl;
#endif

	MyPrint print;
	MyPrint print02=for_each(v.begin(), v.end(), print);

	cout << "print调用次数:" << print.mNum << endl;
	cout << "print调用次数:" << print02.mNum << endl;
}

int main(void) {
	test02();
	return 0;
}
/*
结果：
10
20
30
40
print调用次数:0
print调用次数:4
*/
```

### 二、谓词

谓词是指普通函数或重载的operator()返回值是bool类型的函数对象(仿函数)。如果operator接受一个参数，那么叫做一元谓词,如果接受两个参数，那么叫做二元谓词，谓词可作为一个判断式。

```cpp
//一元谓词函数举例如下
//1，判断给出的string对象的长度是否小于6
bool GT6(const string &s)
{
return s.size() >= 6;
}
//2,判断给出的int是否在3到8之间
bool Compare( int i )
{
return ( i >= 3 && i <= 8 );
}
//二元谓词举例如下
//1，比较两个string对象，返回一个bool值，指出第一个string是否比第二个短
bool isShorter(const string &s1, const string &s2)
{
return s1.size() < s2.size();
}
```

### 三、预定义函数对象

##### 1）预定义函数对象基本概念：

标准模板库STL提前定义了很多预定义函数对象，#include \<functional> 必须包含。

```cpp
//使用预定义函数对象：
//类模板plus<> 的实现了： 不同类型的数据进行加法运算
void main41()
{
    plus<int> intAdd;
    int x = 10;
    int y = 20;
    int z = intAdd(x, y); //等价于 x + y 
    cout << z << endl;

    plus<string> stringAdd;
    string myc = stringAdd("aaa", "bbb");
    cout << myc << endl;

    vector<string> v1;
    v1.push_back("bbb");
    v1.push_back("aaa");
    v1.push_back("ccc");
    v1.push_back("zzzz");
 
   //缺省情况下，sort()用底层元素类型的小于操作符以升序排列容器的元素。
   //为了降序，可以传递预定义的类模板greater,它调用底层元素类型的大于操作符：

	cout << "sort()函数排序" << endl;
    sort(v1.begin(), v1.end(), greater<string>() ); //从大到小
    for (vector<string>::iterator it=v1.begin(); it!=v1.end(); it++ )
    {
         cout << *it << endl;
    }
}
```

##### 2）算术函数对象

预定义的函数对象支持加、减、乘、除、求余和取反。调用的操作符是与type相关联的实例

加法：plus\<Types>

plus\<string> stringAdd;

sres = stringAdd(sva1,sva2);

减法：minus\<Types>

乘法：multiplies\<Types>

除法divides\<Tpye>

求余：modulus\<Tpye>

取反：negate\<Type>

negate\<int> intNegate;

ires = intNegate(ires);

Ires= UnaryFunc(negate\<int>(),Ival1);

 

##### 3）关系函数对象

等于equal_to\<Tpye>

equal_to\<string> stringEqual;

sres = stringEqual(sval1,sval2);

不等于not_equal_to\<Type>

大于 greater\<Type>

大于等于greater_equal\<Type>

小于 less\<Type>

小于等于less_equal\<Type>

```cpp
void main42()
{
    vector<string> v1;
    v1.push_back("bbb");
    v1.push_back("aaa");
    v1.push_back("ccc");
    v1.push_back("zzzz");
    v1.push_back("ccc");
    string s1 = "ccc";
    //int num = count_if(v1.begin(),v1.end(), equal_to<string>(),s1);
    int num = count_if(v1.begin(),v1.end(),bind2nd(equal_to<string>(), s1));
    cout << num << endl;
} 
```

 

##### 4）逻辑函数对象

逻辑与 logical_and\<Type>

logical_and\<int> indAnd;

ires = intAnd(ival1,ival2);

dres=BinaryFunc( logical_and\<double>(),dval1,dval2);

逻辑或logical_or\<Type>

逻辑非logical_not\<Type>

logical_not\<int> IntNot;

Ires = IntNot(ival1);

Dres=UnaryFunc( logical_not\<double>,dval1);

### 四、函数适配器

标准库提供一组函数适配器，用来特殊化或者扩展一元和二元函数对象。常用适配器是：

- 绑定器（binder）: binder通过把二元函数对象的一个实参绑定到一个特殊的值上，将其转换成一元函数对象。C＋＋标准库提供两种预定义的binder适配器：bind1st和bind2nd，前者把值绑定到二元函数对象的第一个实参上，后者绑定在第二个实参上。
- 取反器(negator) : negator是一个将函数对象的值翻转的函数适配器。标准库提供两个预定义的ngeator适配器：not1翻转一元预定义函数对象的真值，而not2翻转二元谓词函数的真值。

常用函数适配器列表如下：

- bind1st(op, value)
- bind2nd(op, value)
- not1(op)
- not2(op)
- mem_fun_ref(op)
- mem_fun(op)
- ptr_fun(op)

##### 绑定器（binder）

```cpp
struct MyPrint : public binary_function<int, int, void> {
	void operator()(int v, int val) const {
		cout << "v:" << v << "   val:"<< val<< "   v+val:" << v + val << " " << endl;
		}
};

void test01() {

	vector<int> v;
	for (int i = 0; i < 3; i++) {
		v.push_back(i);
	}

	int addNum = 200;
	cout << "bind1st结果:" << endl;
	for_each(v.begin(), v.end(), bind1st(MyPrint(), addNum));//绑定适配器  将一个二元函数对象转变成一元函数对象
	cout << "bind2nd结果:" << endl;
	for_each(v.begin(), v.end(), bind2nd(MyPrint(), addNum));
	//bind1st bind2nd区别？
	//bind1st，将addNum绑定为函数对象的第一个参数
	//bind2nd，将addNum绑定为函数对象的第二个参数
}
/*
bind1st结果:
v:200   val:0   v+val:200
v:200   val:1   v+val:201
v:200   val:2   v+val:202
bind2nd结果:
v:0   val:200   v+val:200
v:1   val:200   v+val:201
v:2   val:200   v+val:202
*/
```

##### 取反器(negator) 

```cpp
struct MyPrint02 {
	void operator()(int v) {
		cout << v << " ";
	}
};

struct MyCompare : public binary_function<int, int, bool> {
	bool operator()(int v1, int v2) const {
		return v1 > v2;
	}
};

struct MyGreater5 : public binary_function<int, int, bool> {
	bool operator()(int v, int val) const {
		cout << "v:" << v << " val:" << val << endl;
		return v > val;
	}
};

//仿函数适配器 not1 not2 取反适配器
void test02() {

	vector<int> v;
	for (int i = 0; i < 10; i++) {
		v.push_back(rand()%100);
	}

	for_each(v.begin(), v.end(), MyPrint02()); 
	cout << endl;
	sort(v.begin(), v.end(), MyCompare());
	for_each(v.begin(), v.end(), MyPrint02());
	cout << endl;
	sort(v.begin(), v.end(), not2(MyCompare()));
	for_each(v.begin(), v.end(), MyPrint02());
	cout << endl;

	//not1 not2 
	//如果对二元谓词取反，用not2
	//如果对一元谓词取反，用not1
	vector<int>::iterator it = find_if(v.begin(), v.end(), not1(bind2nd(MyGreater5(), 10)));
	if (it == v.end()) {
		cout << "没有找到" << endl;
	}
	else {
		cout << *it << endl;
	}
}
```

##### ptr_fun(op)

```cpp
void MyPrint03(int val, int val2) {
	cout << "val1:" << val << "   val2:" << val2 << "   val + val2:"<<val + val2 << endl;
}
void test03() {

	vector<int> v;
	for (int i = 0; i < 5; i++) {
		v.push_back(i);
	}

	//ptr_func把普通函数转成函数对象
	for_each(v.begin(), v.end(), bind2nd(ptr_fun(MyPrint03), 10));
}
/*
结果：
val1:0   val2:10   val + val2:10
val1:1   val2:10   val + val2:11
val1:2   val2:10   val + val2:12
val1:3   val2:10   val + val2:13
val1:4   val2:10   val + val2:14
*/
```

##### 成员函数适配器：

mem_fun_ref、mem_fun

```cpp
class Person {
public:
	Person(int age, int id) :age(age), id(id) {}
	void show() {
		cout << "age:" << age << " id:" << id << " aaa" << endl;
	}
public:
	int age;
	int id;
};
void test04() {

	//如果容器中存放的对象或者对象指针，我们for_each算法打印的时候，调用类自己提供的打印函数

	vector<Person> v;
	Person p1(10, 20), p2(30, 40), p3(50, 60);
	v.push_back(p1);
	v.push_back(p2);
	v.push_back(p3);

	//格式: &类名::函数名
	for_each(v.begin(), v.end(), mem_fun_ref(&Person::show));

	vector<Person*> v1;
	v1.push_back(&p1);
	v1.push_back(&p2);
	v1.push_back(&p3);

	for_each(v1.begin(), v1.end(), mem_fun(&Person::show));
	//mem_fun_ref mem_fun区别?
	//如果存放的是对象指针 使用mem_fun
	//如果使用的是对象 使用mem_fun_ref
}
/*
结果：
age:10 id:20 aaa
age:30 id:40 aaa
age:50 id:60 aaa
age:10 id:20 aaa
age:30 id:40 aaa
age:50 id:60 aaa
*/
```

