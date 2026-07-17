---
title: STL综述
date: 2026-07-11 14:24:59
categories:
  -算法
tags:
---

# STL（标准模板库）总述

STL（Standard Template Library）是 C++ 标准库的核心组成部分，它提供了一系列通用的**容器**、**算法**和**迭代器**，极大地提高了开发效率。

**STL 的六大组件：**
1. **容器（Containers）**：用于存储数据，如 `vector`、`list`、`map`、`set` 等。
2. **算法（Algorithms）**：用于操作数据，如 `sort()`、`find()`、`reverse()` 等。
3. **迭代器（Iterators）**：连接容器和算法，类似于指针。
4. **仿函数（Functors）**：行为类似于函数的对象。
5. **适配器（Adapters）**：修改容器或函数接口，如 `stack`、`queue`。
6. **分配器（Allocators）**：管理内存分配。

**学习 STL 的建议：**
- 先掌握最常用的容器：`string`、`vector`、`queue`、`map`、`stack`、`set`。
- 配合算法（如 `sort`、`find`）一起使用，效果翻倍。
- 刷题时优先用 STL 容器，避免手写数据结构。

---

## 1. string 的基础用法

C 风格字符串（以空字符结尾的字符数组）太过复杂，难以掌握，不适合大程序的开发。因此 C++ 标准库定义了一种 `string` 类，定义在头文件 `<string>` 中。

string 和 C 风格字符串对比：
- `char*` 是一个指针，`string` 是一个类，封装了 `char` 数组，是一个字符容器。
- `string` 封装了大量实用的成员方法：查找 `find`，拷贝 `copy`，删除 `erase`，替换 `replace`，插入 `insert` 等。
- 不用考虑内存释放和越界问题（但 `string` 实际有长度限制，最大为 65535，特殊场景下仍需使用 `char*`）。

 1）大小和容量：`size()` 和 `length()`
返回 `string` 对象的字符个数，两者效果相同。
```cpp
string str = "hello";
int len = str.size();  // 或 str.length()
cout << len << endl;   // 输出 5
```

2）字符串比较

按字符的 ASCII 值比较。

```cpp
bool leftBiggerThanRight = (str1 > str2);
```

3）插入：push_back() 和 insert()

```cpp
string str = "abc";
str.push_back('a');   // 末尾添加一个字符，str 变为 "abca"
str.insert(2, "ad");  // 在下标 2 处插入字符串 "ad"，str 变为 "abadc"
```

4）拼接：append 和 +

```cpp
string str = "hello";
str += " world";      // 直接用 + 拼接
str.append(" !");     // 或使用 append
```

5）大小写转换

可以使用 STL 的 transform 算法：

```cpp
#include <algorithm>
#include <cctype>

transform(str.begin(), str.end(), str.begin(), ::tolower);
transform(str.begin(), str.end(), str.begin(), ::toupper);
```

6）遍历

string 可以看作 char 类型的数组。

```cpp
string str = "abc";
for (int i = 0; i < str.size(); i++) {
    cout << str[i] << " ";  // 输出 a b c
}
```

str[0] 的类型是 char，不是 string。

7）查找：find()

```cpp
string str = "hello world";
int pos = str.find("world"); // 返回子串起始位置，找不到返回 -1
int pos2 = str.find("o", 5); // 从下标 5 开始查找
```

8）排序

```cpp
sort(str.begin(), str.end());
```

---

## 2. vector 的基础用法

vector 是动态数组，空间可自动扩充，与固定大小的 array 相比更灵活。

1）定义方式

```cpp
vector<int> a;          // 空的一维数组
vector<int> b(n);       // 长度为 n 的一维数组
vector<int> c(n, 2);    // 长度为 n，所有元素初始化为 2
vector<vector<int>> c[n]; // 二维数组，每行都是一个空的一维数组
```

2）尾部插入：push_back()

```cpp
vector<int> a;
a.push_back(1);   // a = [1]
```

3）尾部删除：pop_back()

```cpp
vector<int> a = {1, 2, 3};
a.pop_back();     // a = [1, 2]
```

4）常用函数：size()、empty()、clear()

```cpp
vector<int> a;
// size 返回元素个数
cout << a.size() << "\n";
for (int i = 0; i < a.size(); i++) {
    cout << a[i] << "\n";
}

// empty 返回是否为空
bool isEmpty = a.empty();
while (!a.empty()) {
    a.pop_back();
}

// clear 清空所有元素
a.clear();
```

---

## 3. queue 的基础用法

queue 遵循 先进先出（FIFO） 原则，只能在队头取出元素，在队尾插入元素。

```cpp
queue<int> que;
```

常用操作：

· push()：在队尾插入一个元素。
· pop()：移除队头元素（无返回值）。
· front()：返回队头元素，但不移除。
· back()：返回队尾元素，但不移除。
· empty()：检查是否为空。
· size()：返回元素个数。

---

## 4. map 的基础用法

map 是键值对集合，所有元素根据键值自动排序，键不可重复。

```cpp
map<string, int> mp;
```

插入与访问

```cpp
mp["会长"] = "帅哥";
mp["怀舟"] = "丑哥";
cout << mp["会长"] << " " << mp["怀舟"] << endl; // 输出：帅哥 丑哥
```

查找元素是否存在

· count(key)：返回 0 或 1。
· find(key)：返回迭代器，若未找到则返回 end()。

```cpp
int cnt = mp.count("ppp");
auto it = mp.find("ppp");
if (it != mp.end()) {
    cout << it->second << endl;
}
```

补充：unordered_map

· 底层是哈希表，查找时间复杂度 O(1)。
· 不自动排序，适合用于判断元素是否出现过（如 unordered_map<int, bool> vis;）。

---

## 5. stack 的基础用法

stack 遵循 先进后出（LIFO） 原则。

```cpp
stack<int> st;
```

常用操作：

· push()：压入栈顶。
· pop()：弹出栈顶（无返回值）。
· top()：返回栈顶元素，但不弹出。
· empty()：检查是否为空。
· size()：返回元素个数。

---

## 6. set 的基础用法

set 是集合，元素自动排序且不重复。

```cpp
set<int> s;
```

常用操作：

· size()：返回容器中元素的个数。
· empty()：检查是否为空。
· swap()：与另一个容器交换内容。
· insert(val)：插入元素。
· erase(val)：删除值为 val 的元素。
· clear()：删除所有元素。
· lower_bound(val)：返回第一个 ≥ val 的迭代器。
· upper_bound(val)：返回第一个 > val 的迭代器。

```cpp
set<int> s = {1, 2, 3, 5};
auto it = s.lower_bound(3); // 指向 3
auto it2 = s.upper_bound(3); // 指向 5
```

---

## 总结

容器 特点 常用场景
string 字符串处理，支持查找、插入、拼接 文本处理、输入输出
vector 动态数组，尾部操作高效 存储序列数据、代替普通数组
queue 先进先出（FIFO） BFS、任务队列
map 键值对，自动排序 字典、计数、映射
stack 先进后出（LIFO） DFS、表达式求值
set 集合，元素唯一且有序 去重、有序存储

```
