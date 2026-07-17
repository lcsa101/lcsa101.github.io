---
title: stack
date: 2026-07-13 14:46:03
categories:
  -算法
tags:
---

# stack栈详解

头文件：`#include <stack>`
通过二次封装双端队列`deque`容器，实现先进后出的栈的数据结构

## 常用方法

 -构造      stack<类型> sta
 -进栈      x.push(元素)
 -出栈      x.pop(元素)
 -取栈顶    x.top()
 -查看大小  x.size()
 -判空      x.empty()
*注：stack无`clear()`清空*

---

## 适用情况

如果题目无限制，则可以使用`stack`

另外，`vector`也可以作为栈使用
如：
```cpp
vector<int> vec;
vec.push_back(1);
vec.push_back(2);
cout << vec.back() << endl;
//此时相当于反过来的栈，输出最后一元素相当与取栈顶
```

---

## 注意事项

`stack`不可访问内部元素，只可以压栈或出栈，不可对内部元素进行操作

队列`queue`使用方法与`stack`类似，但队列先进先出，栈为先进后出
 -访问队首    x.front()
 -访问队尾    x.back()