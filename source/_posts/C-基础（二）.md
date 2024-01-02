---
title: C++基础（二）
tags:
  - C++
  - 一维数组
categories: 笔记
cover: 'https://picsum.photos/id/345/300'
abbrlink: 27216
date: 2022-03-21 16:47:03
---
### 数组的使用

#### 一维数组

**数值特点**：连续的内存空间
              相同数据类型
**定义方式**：
        1.数据类型  数据名[数据长度]
        int array[5]
        2.数据类型  数据组[数据长度] = {值1.....值n}
        int array[5]={0,1,2,3,4};
        3.数据类型  数据名[] = {值1...值n}
        int array[]={0,1,2,3,4};

**一维数组名称用途**
        1.统计整个数组在内存中的长度
        2.获取数组在内存中的首地址

```
cout << sizeof(array) << endl; //获取整个数组所占的内存长度
cout << sizeof(array[0]) << endl; //获取整个数组中某个元素所占的内存长度
cout << array << endl; //查看数组首地址
cout << &array[0] << endl; //查看第一个元素的地址
cout << &array[1] << endl; //查看第二个元素的地址
```

输出结果
![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/array.png)
可以看出第一个元素和第二个元素的内存地址相差四个字节，说明数组的内存空间是线性连续的

#### 练习案例1

**五只小猪称体重**
在一个数组中记录了五只小猪的体重，如：int arr[5] = {300,350,200,40,250};找出并打印最重的小猪体重

```
 int arr[5] = {300,350,200,400,250};
 int weight_Max = 0;
 for (size_t i = 0; i <= 4; i++)
 {
  /* code */
  if (arr[i] > weight_Max)
  {
   weight_Max = arr[i];
  }
  else{
   weight_Max = weight_Max;
  }  
 }
 std::cout << "其中最重的小猪体重为" << weight_Max  << std::endl;
 return 0;

```

输出结果

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/五只小猪.png)

#### 练习案例2

**数组元素逆置**

案例描述：声明一个数组arr[5]={1,2,3,5,4}
逆置后输出arr[5]={4,5,3,2,1}

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/交换排序.png)

输出结果

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/元素逆置.png)

**冒泡排序**
对于冒泡排序，我是这样理解的，每一轮我要选出最大的值，而每一轮之间都要进行比较，比较次数等于数组元素个数-该轮数-1，轮数等于该数组元素个数-1，我们可以大概理解为比较几轮是外循环，如何将每轮比较次数作为内循环，这样子就大概可以列出：

```
for (size_t i = 0; i < sizeof(arr)/sizeof(arr[0])-1; i++)
{
    for (size_t j = 0; j < sizeof(arr)/sizeof(arr[0])-i-1 ; j++)
    {
    }
}
```

如何每轮选出最大值，可以两两比较，将较大的值往后排，将较小的数往前排
我们可以定义一个中间值temp，用于存贮较大的值

```
if(arr[j] > arr [j+1])
{
    temp = arr[j];
    arr[j] = arr[j+1];
    arr[j+1] = temp;
```

然后再上述的if语句填入内循环
我们就可以得到递增的一组数字了

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/冒泡排序.png)
