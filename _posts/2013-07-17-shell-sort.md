---
layout: post
title: 希尔排序
description: 
category: 面试笔试题
tags: [每日一题, 排序]
---
{% include JB/setup %}

### 题目
使用希尔排序对数组进行排序

### 解答
希尔排序是**插入排序**的一种高速而稳定的版本。

希尔排序在插入排序的基础上加入了变步长的方式对序列进行多次排序。比如数组：
  
	1，2，5，1，3，3

写成步长为3的形式为
	
	1，2，5，
	1，3，3

对该长度为3的步长进行插入排序，结果为

	1，2，3，
	1，3，5

然后使用步长为1进行插入排序，即一般的插入排序，结果为
	
	1，1，2，3，3，5

### 复杂度



-  时间复杂度：根据步长选择的变化而变化，最好可以达到`O（n * logn * logn）`




### 代码
	#include <iostream>
	using namespace std;

	void shellSort(int *arr, int n)
	{
		if(arr == NULL || n == 1)
			return;
		//这里的步长最大设置为长度的一半，然后依次除以2
		for(int gap = n / 2; gap > 0; gap /= 2)
		{
			for(int i = gap; i < n; i++)
			{
				int key = arr[i];
				while(i - gap >= 0 && arr[i - gap] > key)
				{
					arr[i] = arr[i - gap];
					i -= gap;
				}
				arr[i] = key;
			}
		}
	}

	int main()
	{
		int arr[10] = {1, 2, 4, 6, 3, 5, 9, 8, 2, 10};
		shellSort(arr, 10);
		for(int i = 0; i < 10; i++)
		{
			cout << arr[i] << endl;
		}
		return 0;
	}
