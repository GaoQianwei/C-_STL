# STL_算法基础

### 一、算法概述

算法部分主要由头文件\<algorithm>，\<numeric>和\<functional>组成。

\<algorithm>是所有STL头文件中最大的一个，其中常用到的功能范围涉及到比较、交换、查找、遍历操作、复制、修改、反转、排序、合并等等。

\<numeric>体积很小，只包括几个在序列上面进行简单数学运算的模板函数，包括加法和乘法在序列上的一些操作。

\<functional>中则定义了一些模板类，用以声明函数对象。

STL提供了大量实现算法的模版函数，只要我们熟悉了STL之后，许多代码可以被大大的化简，只需要通过调用一两个算法模板，就可以完成所需要的功能，从而大大地提升效率。

#include \<algorithm>

#include \<numeric>

#include \<functional>

### 二、STL中算法分类

- 操作对象 

- - 直接改变容器的内容
  - 将原容器的内容复制一份,修改其副本,然后传回该副本

- 功能: 

- - 非可变序列算法 指不直接修改其所操作的容器内容的算法

  - - 计数算法     count、count_if
    - 搜索算法     search、find、find_if、find_first_of、…
    - 比较算法     equal、mismatch、lexicographical_compare

  - 可变序列算法 指可以修改它们所操作的容器内容的算法

  - - 删除算法     remove、remove_if、remove_copy、…
    - 修改算法     for_each、transform
    - 排序算法     sort、stable_sort、partial_sort、

  - 排序算法 包括对序列进行排序和合并的算法、搜索算法以及有序序列上的集合操作

  - 数值算法 对容器内容进行数值计算

### 三、常用算法汇总

常用的**查找**算法：adjacent_find()（ adjacent 是邻近的意思）,binary_search(),count(),count_if(),equal_range(),find(),find_if()。

常用的**排序**算法：merge(),sort(),random_shuffle()（shuffle是洗牌的意思） ,reverse()。

常用的**拷贝和替换**算法：copy(), replace(),replace_if(),swap()

常用的**算术和生成**算法：accumulate()（ accumulate 是求和的意思）,fill(),。

常用的**集合**算法：set_union(),set_intersection(),set_difference()。

常用的**遍历**算法：for_each(), transform()（ transform 是变换的意思）。