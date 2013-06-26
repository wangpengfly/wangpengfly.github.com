---
layout: post
title: 循环右移数组
description: 
category: 面试笔试题
tags: [每日一题, 数组]
---
{% include JB/setup %}

## 题目
设计算法，实现一个对数组循环右移k个元素的函数，要求时间复杂度为`O(n)`

## 解答
第一反应想到的是保存要右移的K个元素，然后将右边的N - K个元素左移，这样也可以做到`O(n)`的时间复杂度，但是空间复杂度是`O(k)`。这个方法符合题意，但是不够好。
在有些题目中，对空间复杂度有进一步要求：只允许使用两个附加变量。这个时候，就只能使用下面代码的思路了，这个在编程珠矶里面有讲。

思路为：对一个数组循环右移K位（这里设`K<N`）可以用以下三步完成

* 反转0到K-1位数组
* 反转k到N-1位数组
* 反转0到N-1位数组

例如数组为1，2，3，4，5，循环右移三位，则经过三步为

* 3，2，1，4，5
* 3，2，1，5，4
* 4，5，1，2，3

## 注意几点

* K可能大于N，则K = K % N
* 代码实现的循环右移K位，循环左移K位可以转换成右移N - K % N位

## 代码

	#include <iostream>  
	using namespace std;  
  
	void reverse(int *a, int beginIndex, int endIndex)  
	{  
    	if(beginIndex >= endIndex)  
    	    return;  
    	while(beginIndex < endIndex)  
    	{  
        	int temp = a[beginIndex];  
        	a[beginIndex] = a[endIndex];  
        	a[endIndex] = temp;  
        	beginIndex++;  
        	endIndex--;  
    	}  
	}  
  
	bool shiftKElements(int *a, int n, int k)  
	{  
    	if(a == 0) return false;  
    	if(k == 0 || n == 0) return false;  
    	k = k % n;  
    	reverse(a, 0, k - 1);  
    	reverse(a, k, n - 1);  
    	reverse(a, 0, n - 1);  
    	return true;  
	}  
  
	int main()  
	{  
    	int a[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};  
    	if(shiftKElements(a, 10, 5))  
    	    for(int i = 0; i < 10; i++)  
        	    cout << a[i] << " ";  
    	cout << endl;  
    	return 0;  
	} 

