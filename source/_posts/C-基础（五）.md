---
title: C++基础（五）
tags:
  - C++
  - 指针
categories:
  - 学习
  - 笔记
cover: 'https://picsum.photos/id/352/300/300'
abbrlink: 51798
date: 2022-03-24 13:21:13
---
### 指针

**作用**

通过指针间接访问内存（指针就是一个地址）

内存编号是从0开始记录的，一般用十六进制数字表示
可以利用指针变量保存地址

#### 指针的使用
*定义的语法*
数据类型 * 指针变量
如 int *p;

//怎么使用指针
//通过解引用的方式来找到指针指向的地址
//指针前加*代表解引用，找到指针指向的内存中的数据

**指针所占的空间**
指针也是种数据类型，那么这种数据类型占用多少内存空间
在32位操作系统下，占用4个字节
在64位操作系统下，占用8个字节

**空指针**
空指针：指针变量指内存中编号为0的空间
用途： 初始化指针变量
注意：空指针指向的内存是不可以访问的
0~255之间的内存编号是系统占用的因此是不可以访问的
也就是空指针是不可以对其地址内部的数据进行修改

**野指针**
指针变量指向非法的内存空间

**const修饰指针**
```
1.const 修饰指针 --- 常量指针
2.const 修饰常量 --- 指针常量
3.const即修饰指针，又修饰常量
常量指针：const int * p = &a;
特点：指针的指向可以修改
但是指针指向的值不可以修改
例如 *p = 20;这是错的
p = &b;这是对的
指针常量：int * const p = &a;
特点：指针的指向不可以修改
指针指向的值可以修改
例如 *p = 20;这是对的
p = &b;这是错的
即修饰指针，又修饰常量: const int * const p = &a;
特点：指针的指向和指向的值都不可以修改
```
#### 指针和数组
利用指针访问数组中的元素
案例：利用指针遍历数组中每一个元素
```
int arr[] = {1,2,3,4,5,6,7,8,9,10};
int * x = arr;
for (size_t i = 0; i < 9; i++)
{
    /* code */
    cout << "利用指针指向数组的第"<<i<<"个元素"<<*x <<endl;
    x++;
}
```
#### 指针和函数
**指针和函数**
案例描述：封装一个函数，利用冒泡排序，实现整型数组的升序排列
例如数组：int arr[10] = {4,3,6,9,1,2,10,8,7,5};

```
void bubbleSort(int *arr, int len )
{
	for (int i = 0; i < len-1; i++)
	{
		/* code */
		for (int j = 0; j < len-i-1; j++)
		{
			/* code */
			if (arr[j] > arr[j+1])
			{
				int temp = arr[j];
				arr[j] = arr[j+1];
				arr[j+1] = temp;
			}
		}	
	}	
		for (size_t i = 0; i < 10; i++)
	{
		/* code */
		cout << "arr["<< i <<"]="<<arr[i] << endl;
	}
}

```

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/冒泡排序封装.png)