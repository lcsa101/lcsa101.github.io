---
title: vector
date: 2026-07-11 16:50:54
categories:
  -算法
tags:
---

# vector动态数组详解

头文件：#include<vector>
连续的顺序储存结构，但是长度可变。

## vector的构造（语法）

vector<类型>arr(长度，[初值])
注：小括号内填写其构造函数

时间复杂度为：O(n)

**实例**
```cpp
#include <bits/stdc++.h>//万能头文件
using namespace std;
int main()
{
    vector<int> vec;//不传入构造函数为无参构造
    vector<double> vec2(100);//长度为100
    vector<int> vec3(100,1);//长度为100且初始值为1

}
```

扩展1. 如何用vector构造二维数组
```cpp
#include <bits/stdc++.h>
using namespace std;
int main()
{
    vector<vector<int>> dp(5,vector<int>(6,1));
}
```
上面代码意味：创建二维数组`dp`，其行数为5，列数为6，且初始值为1
由此类推

扩展2. 三维数组
```cpp
vector<vector<vector<int>>> dp(5,vector<vector<int>>(6,vector<int>(4)));
//其在用法上等价于
int dp1[5][6][4];
```

---

## vector的尾接与尾删

1.尾接（在数组后加入元素）
```cpp
vector<int> arr;
arr.push_back(1);//在arr后加入元素1
```

2.尾删（弹出数组最后的元素）
```cpp
arr.pop_back();
```

---

## vector获取长度

```cpp
arr.size();
```
可返回当前arr数组长度

---

## vector数组的清空

1.vector的清空
注：vector数组可以不用逐一的pop_back，可利用clear直接清空数组
```cpp
arr.clear();
```

2.vector的判空
使用`arr.empty()`
注：返回值为布尔类型，若数组为空返回`true`，否则返回`false`

---

## 如何给vector数组改变长度

通过调用`resize()`函数，括号内为新的长度
```cpp
vector<int> arr(10);
arr.resize(50,1);//括号内第二个数为初值
```

同样，通过`resize()`，也可以将数组的长度变短
注：数组增长时，其新增元素自带初值，而将数组长度缩短时则是直接删除了多余的元素

---

## vector的适用情形

一般来说`vector`可替代普通数组，除非特殊情况（题目要求运用常规数组）
另外，`vector`储存在堆空间中，不会爆栈

---

## 注意事项

1.提前指定长度
如果题目提前指定长度，则应在构造函数中直接指定长度，而不是一个个`push_back`，因为`vector`内存耗尽后重分配有时间开销，直接设定长度则可避免
如：
```cpp
//优化前：522ms
vector<int> a;
for(int i=0;i<1e8;i++)
{
    a.push_back(i);
}
//优化后：259ms
vector<int> b(1e8);
for(int i=0;i<b.size(),i++)
{
    b[i]=i;
}
```

2.当心size_t溢出
`vector`获取长度方法`x.size()`返回值类型为`size_t`通常OJ为32位编译器，故该类型的范围为[0,2^32]
如：
```cpp
vector<int> a(65536);
long long re = a.size() * a.size();//溢出，re为0
```