# STL_queue容器

### 一、queue简介

queue所有元素的进出都必须符合”先进先出”的条件，只有queue的顶端元素，才有机会被外界取用。queue不提供遍历功能，也不提供迭代器。

queue是简单地装饰deque容器而成为另外的一种容器。

#include \<queue> 

<img src="C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210124200423195.png" alt="image-20210124200423195" style="zoom:50%;" />

### 二、queue对象的默认构造

queue采用模板类实现，queue对象的默认构造形式：queue\<T> queT; 

```cpp
queue<int> queInt;      //一个存放int的queue容器。
queue<float> queFloat;   //一个存放float的queue容器。
queue<string> queString;   //一个存放string的queue容器。
//尖括号内还可以设置指针类型或自定义类型。          
```

 

### 三、queue的push()与pop()方法

queue.push(elem);  //往队尾添加元素

queue.pop();  //从队头移除第一个元素 

```cpp
queue<int> queInt;

queInt.push(1);
queInt.push(3);
queInt.push(5);
queInt.push(7);
queInt.push(9);
queInt.pop();
queInt.pop();
//此时queInt存放的元素是5,7,9
```



### 四、queue对象的拷贝构造与赋值

queue(const queue &que);          //拷贝构造函数

queue& operator=(const queue &que); //重载等号操作符		

```cpp
queue<int> queIntA;
queIntA.push(1);
queIntA.push(3); 
queue<int> queIntB(queIntA);    //拷贝构造
queue<int> queIntC;
queIntC = queIntA;              //赋值
```



### 五、queue的数据存取

queue.back();  //返回最后一个元素

queue.front();  //返回第一个元素        

```cpp
queue<int> queIntA;
queIntA.push(1);
queIntA.push(3);
queIntA.push(5);
queIntA.push(7);
queIntA.push(9);
int iFront = queIntA.front();       //1
int iBack = queIntA.back();       //9
```

 

### 六、queue的大小

queue.empty();  //判断队列是否为空

queue.size();      //返回队列的大小         

```cpp
queue<int> queIntA;    
queIntA.push(1);      
queIntA.push(3);      
queIntA.push(5);       
queIntA.push(7);       
queIntA.push(9);       
if (!queIntA.empty()){
   int iSize = queIntA.size();     //5
}
```

