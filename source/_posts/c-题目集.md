---
title: c++题目集
date: 2026-07-13 17:52:34
categories:
  -编程习题
tags:
---

# C++习题集

## 此集合记录一些普及/提高题型，包含基础，提高，竞赛真题，并提供我自己的题解以供参考

---

# P5738 【深基7.例4】歌唱比赛

题目描述

n(n<=100) 名同学参加歌唱比赛，并接受 m(m<=20) 名评委的评分，评分范围是 0 到 10 分。这名同学的得分就是这些评委给分中去掉一个最高分，去掉一个最低分，剩下 m-2 个评分的平均数。请问得分最高的同学分数是多少？评分保留 2 位小数。

输入格式

第一行两个整数 n,m。   
接下来 n 行，每行各 m 个整数，表示得分。

输出格式

输出分数最高的同学的分数，保留两位小数。

输入输出样例 #1

输入 #1

```
7 6
4 7 2 6 10 7
0 5 0 10 3 10
2 6 8 4 3 6
6 3 6 7 5 8
5 9 3 3 8 1
5 9 9 3 2 0
5 8 0 4 1 10

```

输出 #1

```
6.00
```

```cpp
#include<iostream>
using namespace std;

void swap(double* a,int n)
{
	for (int i = 0; i < n - 1; i++)
	{
		for (int j = 0; j < n - 1 - i; j++)
		{
			if (a[j] > a[j + 1])
			{
				double t;
				t = a[j];
				a[j] = a[j + 1];
				a[j + 1] = t;
			}
		}
	}
}
double pj(double *a,int n)
{
	swap(a, n);
	a[0] = 0;
	a[n - 1] = 0;
	double sum = 0;
	for (int i = 0; i < n; i++)
	{
		sum += a[i];
	}
	double f = sum / (n - 2) * 1.0;
	return f;
}
int main()
{
	int m, n;
	cin >> n >> m;
	double score[22] = { 0 };
	double mf[105] = { 0 };
	for (int j = 0; j < n; j++)
	{
		for (int i = 0; i < m; i++)
		{
			cin >> score[i];
		}
		mf[j] = pj(score, m);
		for (int k = 0; k < m; k++)
		{
			score[k] = 0;
		}
	}
	swap(mf, n);
	printf("%.2f", mf[n - 1]);
	return 0;
}
```

---

# P1152 欢乐的跳

题目描述

一个 n 个元素的整数数组，如果数组两个连续元素之间差的绝对值包括了 [1,n-1] 之间的所有整数，则称之符合“欢乐的跳”，如数组 {1,4,2,3} 符合“欢乐的跳”，因为差的绝对值分别为：3,2,1。

给定一个数组，你的任务是判断该数组是否符合“欢乐的跳”。

输入格式

每组测试数据第一行以一个整数 n(1 <= n <= 1000) 开始，接下来 n 个空格隔开的在 [-10^8,10^8] 之间的整数。

输出格式

对于每组测试数据，输出一行若该数组符合“欢乐的跳”则输出 `Jolly`，否则输出 `Not jolly`。

输入输出样例 #1

输入 #1

```
4 1 4 2 3

```

输出 #1

```
Jolly

```

输入输出样例 #2

输入 #2

```
5 1 4 2 -1 6
```

输出 #2

```
Not jolly
```

*说明/提示*

1 <= n <= 1000

```cpp
#include<iostream>
#include<algorithm>
#include<vector>
using namespace std;

int main()
{
	int n;
	cin >> n;
	vector<int> a(n);
	for (int i = 0; i < n; i++)
		cin >> a[i];
	if (n == 1)
	{
		cout << "Jolly";
		return 0;
	}
	vector<int> diff(n - 1);
	for (int i = 1; i < n; i++)
		diff[i - 1] = abs(a[i] - a[i - 1]);
	sort(diff.begin(), diff.end());
	bool is = true;
	for (int i = 0; i < n - 1; i++)
	{
		if (diff[i] != (i + 1))
		{
			is = false;
			break;
		}
	}
	cout << (is ? "Jolly" : "Not jolly");
	return 0;
}
```