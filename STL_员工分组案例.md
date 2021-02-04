# STL_员工分组案例

公司今天招聘了 5 个员工， 5 名员工进入公司之后，需要指派员工在那个部门工作

- 人员信息有: 姓名 年龄 电话 工资等组成
- 通过 Multimap 进行信息的插入 保存 显示
- 分部门显示员工信息 显示全部员工信息

```cpp
//main.cpp文件
#include "worker.h"
#include "manager.h"

int main()
{
	manager m;
	m.show();
	return 0;
}
```

```cpp
//work.h文件
#pragma once
#include <string>
#include <map>
#include <vector>
#include <map>
using namespace std;

class worker
{
public:
	string getName();
	void setName(string name);

	string getTelephone();
	void setTelephone(string telephone);

	int getAge();
	void setAge(int age);

	float getSalary();
	void setSalary(float salary);

private:
	string name;
	int age;
	string telephone;
	float salary;
};
```

```cpp
//work.cpp文件
#include "worker.h"
#include <string>
using namespace std;

string worker::getName() {
	return this->name;
}

void worker::setName(string name) {
	this->name = name;
}

string worker::getTelephone() {
	return this->telephone;
}

void worker::setTelephone(string telephone) {
	this->telephone = telephone;
}

int worker::getAge() {
	return this->age;
}

void worker::setAge(int age) {
	this->age = age;
}

float worker::getSalary() {
	return this->salary;
}

void worker::setSalary(float salary) {
	this->salary = salary;
}
```

```cpp
//manager.h文件
#pragma once

#define WORKER_NUMBER 5

#define SALE_DEPATMENT 1 //销售部门
#define DEVELOP_DEPATMENT 2 //研发部门
#define FINACIAL_DEPATMENT 3 //财务部门

#include <string>
#include <map>
#include <vector>
#include <map>
#include "worker.h"
using namespace std;
class manager
{
public:
	void create_worker();
	void divide_worker();
	void print_worker(int departID);
	void print_worker_by_group();
	void show();
private:
	vector<worker> worker_vector;
	multimap<int, worker> worker_group;
};
```

```cpp
//manager.cpp文件
#include "worker.h"
#include "manager.h"
#include <string>
#include <map>
#include <vector>
#include <iostream>
#include <map>
#include <time.h>
using namespace std;

void manager::create_worker() {

	string name_seed = "ABCDE";

	for (int i = 0; i < WORKER_NUMBER; i++) {

		worker worker;
		string tmp = name_seed.substr(i, 1);
		worker.setName("选手" + tmp);
		worker.setAge(rand() % 15 + 20);
		worker.setTelephone("010-88888888");
		worker.setSalary(rand()%10000+1000.00);

		this->worker_vector.push_back(worker);
	}
}

void manager::divide_worker() {
	srand(time(NULL));
	for (vector<worker>::iterator it = this->worker_vector.begin() ; it !=this->worker_vector.end(); it++) {

		int departID = rand() % 3 + 1;
		switch (departID) {

			case SALE_DEPATMENT:
				this->worker_group.insert(make_pair(SALE_DEPATMENT, *it));
				break;
			case DEVELOP_DEPATMENT:
				this->worker_group.insert(make_pair(DEVELOP_DEPATMENT, *it));
				break;
			case FINACIAL_DEPATMENT:
				this->worker_group.insert(make_pair(FINACIAL_DEPATMENT, *it));
				break;
			default:
				break;
		}
	}
}

void manager::print_worker(int departID) {
	
	multimap<int, worker>::iterator it = this->worker_group.find(departID);
	
	int DepartCount = this->worker_group.count(departID);
	int num = 0;
	for (multimap<int, worker>::iterator pos = it; it != this->worker_group.end() && num < DepartCount; pos++, num++) {
		cout << "姓名:" << pos->second.getName()<< " 年龄:" << pos->second.getAge() << " 电话:" << pos->second.getTelephone() << " 工资:" << pos->second.getSalary() << endl;
	}
}

//打印每一部分员工信息
void manager::print_worker_by_group() {

	//显示销售部门
	cout << "销售部门:" << endl;
	this->print_worker(SALE_DEPATMENT);
	//显示开发部门
	cout << "研发部门:" << endl;
	this->print_worker(DEVELOP_DEPATMENT);
	//显示财务部门
	cout << "财务部门:" << endl;
	this->print_worker(FINACIAL_DEPATMENT);
}

void manager::show() {
	this->create_worker();
	this->divide_worker();
	this->print_worker_by_group();
}
```

