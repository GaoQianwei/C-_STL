# STL_stack容器

### 一、stack简介

stack是一种先进后出(First In Last Out,FILO)的数据结构，它只有一个出口。stack容器允许新增元素，移除元素，取得栈顶元素，但是除了最顶端外，没有任何其他方法可以存取stack的其他元素。换言之，stack不允许有遍历行为。

- 有元素推入栈的操作称为:push
- 将元素推出stack的操作称为pop

stack是简单地装饰deque容器而成为另外的一种容器。

#include\<stack> 

<img src="C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210124200437495.png" alt="image-20210124200437495" style="zoom:50%;" />

### 二、stack对象的默认构造

stack采用模板类实现， stack对象的默认构造形式： stack <T> stkT; 

```cpp
stack <int> stkInt;      //一个存放int的stack容器。
stack <float> stkFloat;   //一个存放float的stack容器。
stack <string> stkString;   //一个存放string的stack容器。
//尖括号内还可以设置指针类型或自定义类型。
```



### 三、stack的push()与pop()方法

stack.push(elem);  //往栈头添加元素

stack.pop();  //从栈头移除第一个元素 

```cpp
stack<int> stkInt;  

stkInt.push(1);
stkInt.push(3);
stkInt.pop();  
//此时stkInt存放的元素是1
```



### 四、stack对象的拷贝构造与赋值

stack(const stack &stk);         //拷贝构造函数

stack& operator=(const stack &stk);    //重载等号操作符         

```cpp
stack<int> stkIntA;
stkIntA.push(9);
stack<int> stkIntB(stkIntA);       //拷贝构造
stack<int> stkIntC;
stkIntC = stkIntA;               //赋值
```



### 五、stack的数据存取

stack.top();  //返回最后一个压入栈元素，即栈顶元素        

```cpp
stack<int> stkIntA;
stkIntA.push(1);
stkIntA.push(7);
stkIntA.push(9); 
int iTop = stkIntA.top();      //9
```

  

### 六、stack的大小

stack.empty();  //判断堆栈是否为空

stack.size();       //返回堆栈的大小         

```cpp
stack<int> stkIntA;
stkIntA.push(1);
stkIntA.push(3);
if (!stkIntA.empty()){
	int iSize = stkIntA.size();      //2
   }
```

 