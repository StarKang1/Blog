---
title: C++核心编程(一)
abbrlink: 33962
date: 2022-03-31 00:06:21
tags: 
  - C++
categories:	
  - 学习
  - 笔记
cover: https://picsum.photos/id/802/300/300

---

# C++核心编程

本阶段主要针对C++面向对象编程技术做详细讲解，探讨C++中的核心和精髓。

## 1内存分区模型

C++程序在执行时，将内存大方向划分为4个区域

a.代码区：存放函数体的二进制代码，由操作系统进行管理的
b.全局区：存放全局变量和静态变量以及常量
栈区：由编译器自动分配释放，存放函数的参数值，局部变量等
c.堆区：由程序员分配和释放，若程序员不释放，程序结束时由操作系统回收

**内存四区意义：**
不同区域存放的数据，赋予不同的生命周期，给我们更大的灵活编程

### 1.1程序运行前

在程序编译后，生成了exe可执行程序，未执行该程序前分为两个区域
*代码区：*
存放CPU执行的机器指令
代码区是共享的，共享的目的是对于频繁被执行的程序，只需要在内存中有一份代码即可
代码区是只读的，使其只读的原因是防止程序意外地修改了它的指令
*全局存储区：*
全局变量、静态变量以及
全局区还包含了常量区，字符串常量是和其他常量也存放在此
该区域的数据在程序结束后由操作系统释放。

### 1.2程序运行后

*栈区：*

由编译器自动分配释放，存放函数的参数值，局部变量等

注意事项：局部变量的地址在函数执行结束后会自动释放掉。不要放回局部变量的地址，栈区开辟的数据由编译器自动释放

**代码实验**

```
int *func()

{

  int a = 10;

  return &a;

}
```

输出结果：

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/GV$L}QIH0_}CNS1U3D2VU44.png)



*堆区*

由程序员分配释放，若程序员不释放，程序结束时由操作系统收回

在C++中主要利用new在堆区开辟内存

利用new关键字，可以将数据开辟到堆区

指针 本质上也是局部变量，放在栈上，指针保存的数据是放在堆区的

**代码实验**

```
#include <iostream>
using namespace std;
int c ;
int * func()
{
	int *a = new int(10);
	return a;
}
int main(int argc, char *argv[])
{
	int *b = func();
	int a =10;
	int *p = &a;
	int *x = &c;
	*x = 10;
	cout << *b<< endl;
	cout << *b<< endl;
	cout << *b<< endl;
	cout << *b<< endl;
	cout << x << endl;
	cout << b << endl;
	cout << p << endl;
}
```

**输出结果：**

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/uTools_1648645563992.png)

讲到这里，我去搜了一下什么是全局变量、局部变量、静态局部变量以及静态全局变量。

首先，得知道什么是全局、静态、局部

全局：具有文件作用域的变量

静态：具有静态存储器或内部链接性质

局部：具有函数或块作用域的变量

那么

局部变量：函数或块作用域的变量

静态局部变量：函数或块作用域，静态存储期

全局变量：具有文件作用域的变量

静态全局变量：内部链接属性的，具有文件作用域的变量



**代码实验**

```
#include <iostream>
using namespace std;
int a = 10;
static int b = 10;
const int e = 20;
int main(int argc, char *argv[])
{
	int c = 10;
	static int temp = 10;
	const int d = 10;
	cout <<&a << endl;
	cout <<&b << endl;
	cout <<&c << endl;
	cout <<&temp << endl;
	cout << &"hello world" <<endl;
	cout <<&d << endl;
	cout <<&e << endl;
//结果说明全局变量、const修饰的全局变量、静态全局变量、静态局部变量以及字符串常量都是在全局存储区
//而局部变量、const修饰的局部变量在栈区
}

```

具有文件作用域的变量具有静态存储期，并且具有链接属性

不希望其他文件访问的文件作用域变量最好用static修饰

尽可能不使用全局变量，因为它可能带来变量被以为修改

栈内存响应比动态内存快，但是栈内存有限

### 1.3 new操作符

C++中利用new操作符在堆区开辟数据

堆区开辟的数据，由程序员手动开辟，手动释放，释放利用操作符delete

*语法：*new数据类型

利用new创建的数据，会返回该数据对应的类型的指针

**代码实验**

```
#include <iostream>
using namespace std;
int * func()
{
	int* p = new int(10);//new开辟堆区间
	return p;
}
int main(int argc, char *argv[])
{
	int *a = func(); //
	cout << *a << endl;
	cout << a << endl;
	delete a; //手动释放
	cout << *a << endl;
	cout << a << endl;
}
```

**输出结果：**

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/uTools_1648649204694.png)

## 2.引用

### 2.1 引用的基本使用

**作用：**给变量起别名

**语法：**数据类型 &别名 = 原名

**代码实验**

```
#include <iostream>
using namespace std;
//引用的本质是给某个变量取别名
int main(int argc, char *argv[])
{
	int a = 10;
	int &b = a; //给a取别名为b
	cout << a << endl;
	//这里a和b的地址是一样的
	//说明a b指向的地址是一样的，所以保存的数据也是一样的,我是这么理解的qAq
	cout << &a << endl;
	cout << &b << endl;
	cout << b << endl;
	b = 100;
	cout << a << endl;
	cout << b << endl;
}
```

**输出结果：**

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/uTools_1648650774020.png)

### 2.2引用注意事项

引用必须初始化

引用在初始化后，不可以改变

**代码实验：**

```
int main(){
	int a = 10;
	int c =10;
	// int &b; // 错误，引用必须初始化
	int &b = a; //一旦初始化，不可重复初始化
	// int &b = c;报错： redeclaration of ‘int& b’ 重复声明
	c = b; //赋值操作，并不是初始化
	cout << a << endl;
	cout << b << endl;
	cout << c << endl;
	cout << &a << endl;
	cout << &b << endl;
	cout << &c << endl;
}

```

输出结果：

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/uTools_1648651363188.png)

说明赋值并不是引用

### 引用做函数参数

**代码实验**

```
#include <iostream>
using namespace std;
//演示 值传递 地址传递 引用传递的不同
//值传递数值交换 地址随机分配内存， 形参不修饰实参 地址发生改变
void swap1(int a ,int b)
{
	int temp = a;
	a = b;
	b = temp;
	cout << "值传递后的值"<< endl;
	cout << "a = " << a << "  *a= " << &a << endl;
	cout << "b = " << b << "  *a= " << &b << endl;
}
//地址传递 地址和数值都交换了 
void swap2(int * a,int * b)
{
	int temp = *a;
	*a = *b ;
	*b = temp;
	cout << "地址传递后的值"<< endl;
	cout << "a = " << *a << "  *a= " << a << endl;
	cout << "b = " << *b << "  *b= " << b << endl;
}
//引用传递,地址没有交换，数值交换了
void swap3(int &a,int &b)
{
	int temp = a;
	a = b;
	b = temp;
	cout << "引用传递后的值"<< endl;
	cout << "a = " << a << "  *a= " << &a << endl;
	cout << "b = " << b << "  *b= " << &b << endl;
}
int main(int argc, char *argv[])
{
	int a = 10;
	int b = 30;
	cout << "未交换前的实参的值"<< endl;
	cout << "a = " << a << "  *a= " << &a << endl;
	cout << "b = " << b << "  *b= " << &b << endl;
	swap1(a,b);
	swap2(&a,&b);
	swap3(a,b);

}
```
输出结果：
![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/uTools_1648709199204.png)

值传递属于是形参不修饰实参，没有修饰符，可以发现值传递的值交换了，地址是随机分配的

地址传递和引用传递属于是形参修饰实参，地址传递的值交换了，地址没有交换，
引用传递的值发生了交换，地址没有发生交换，也就是相当于给变量取了别的名字，这个名字所赋的值也会跟随过来，简化指针修改实参。

### 2.4 引用做函数返回值

作用：引用是可以作为函数的返回值存在的

注意： 不要返回局部变量

用法： 函数调用作为左值

**代码实验：**

```
#include <iostream>
using namespace std;
int &num()
{
	int a = 10;
	return a;
}
int main()
{
	int &ref = num();
	cout << ref << endl;
}
```

**输出结果：**

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/uTools_1648713008951.png)

**结论：**局部变量不能作为返回值，局部变量的数据保存在栈区，在函数或是块作用域执行结束后内存释放，因此不能作为返回值。

**代码实验：**

```
#include <iostream>
using namespace std;
int &num()
{
	static int a = 10;
	return a;
}
int main()
{
	int &ref = num();
	cout << ref << endl;
}

```

**输出结果：**

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/uTools_1648713277009.png)

**结论：** 静态局部变量的数据保存在全局区，程序结束后内存释放，所以可以作为返回值。

### 2.5引用的本质

**本质：** 引用的本质在C++内部实现是一个指针常量

即int &a  本质是 int * const a; 

指向的地址不可以改变，地址内部的数据是可以修改和查看的

**代码实验：**

```
#include <iostream>
using namespace std;
void func(int &ref)
{
	ref = 100;
}

int main(int argc, char *argv[])
{
	int a = 10;
	int &ref = a;
	ref = 20;
	cout << a << endl;
	cout << ref << endl;
	func(a);
	cout << a << endl;
	cout << ref << endl;	
}
```

**输出结果：**

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/uTools_1648715456921.png)

**结论：** 从上面的代码可以看出，引用本质是改名，修改变量的名字，对其进行赋值。

### 2.3常量引用

作用：常量引用用于修饰形参,防止误操作

在函数参数列表里，可以加上const修饰形参，防止形参改变实参。

```
#include <iostream>
using namespace std;

void showValue(const int &val) //当你不希望形参改变实参的时候可以用这个，相当于即修饰指针又修饰常量
{
	val = 1000;//当你尝试修改变量的值的时候就会报错
	cout << "val = " << val << endl;
}

int main(int argc, char *argv[])
{
	int a = 10;
	showValue(a); 
	cout << "a = " << a <<  endl;
}
```

## 3.函数提高

### 3.1函数默认参数

在C++中，函数的形参列表中的形象是可以有默认值的

语法：返回值类型 函数名 （参数 = 默认值）{ }

**注意事项** 如果函数某个位置已经有参数了，那么从这个位置往后都必须有参数

**代码实验：** 

```
#include <iostream>
using namespace std;
int func(int a, int b = 10 ,int c = 20)
{
	return a+b+c;
}
int main(int argc, char *argv[])
{
	int a = 10;
	cout << func(10) << endl;
}
```

### 3.2函数占位参数

C++中函数的形参列表里可以有占位参数，用来做占位，调用函数时必须填补该位置。

语法： 返回值类型 函数名 （数据类型） {}

在现阶段函数的占位参数意义不大，但是后面的课程中会用到该技术。

**代码实验：**

```
#include <iostream>
using namespace std;

int func(int a ,int)
{
	cout << "This is a function" << endl;
	return 0;
}
int main(int argc, char *argv[])
{
	func(10,10);
}
```



### 3.3函数重载

#### 3.3.1函数重载概述

**作用：** 函数名可以相同，提高复用性

**函数重载满足条件：**

**1.在同一个作用域下**

**2.函数名称相同**

**3.函数参数类型不同或者个数不同或者顺序不同**

**注意:** 函数返回值不可以作为函数重载的条件

**代码实验：** 

```
#include <iostream>
using namespace std;
//函数重载
//**1.在同一个作用域下**
// **2.函数名称相同**
// **3.函数参数类型不同或者个数不同或者顺序不同**
int func(int a)
{
	int b = a;
	cout << "函数复用！" << endl;
	cout << a << b << endl;
	return a,b;

}
int func(int b ,int a)
{
	a = b;
	cout << "函数复用！！" << endl;
	cout << a << b << endl;
	return a,b;
}

int main(int argc, char *argv[])
{
	int a=20 ,b = 10;
	func(a);
	func(a,b);
}
```

### 3.3.2函数重载注意事项

· 引用作为重载条件

· 函数重载碰到函数默认参数 

## 4.类和对象

C++面向对象的三大特性：封装、继承、多态

C++认为万事万物都是对象，对象有其属性和行为

### 4.1封装

#### 4.1.1 封装的意义

封装是C++面向对象三大特性之一

封装的意义：

将属性和行为作为一个整体，表现生活中的事物

将属性和行为加以权限控制

封装意义一：

在设计类的时候，属性和行为写在一起，表现生活中的事物

语法：class 类名{访问权限：属性/行为}；

示例：设计一个圆类，，求圆的周长

```
#include <iostream>
using namespace std;
//设计一个圆类，求圆的周长
//圆的周长公式：2*pi*r
const double pi = 3.14;
class Circle 
{
	//访问权限
	//公共权限
	public:
	//属性
	//半径
	int r;
	//行为
	//获取圆的周长
	double Caculate(int &r)
	{
		double ZC = 2*pi*r;
		return ZC;
	}

};
int main(int argc, char *argv[])
{
	Circle cl;
	cl.r = 10;
	double ZC = cl.Caculate(cl.r);
	cout << ZC << endl;	
}
```

从上面的代码来看，感觉类和结构体有点相似，都包含了属性，不同的点是，类有访问权限和行为。

案例2：创建一个学生类，属性有姓名和学号，给学生的姓名和学号赋值，可以显示学生的姓名和学号；

```
#include <iostream>
#include <string>
using namespace std;
//设计一个学生类，属性有姓名和学号
//可以给学生的姓名和学号赋值，可以显示学生的姓名和学号
class Student
{
	//访问权限
	public:
	//属性有姓名和学号
	string s_Name;
	long s_Numble;
	//行为是显示学生的姓名和学号
	void displayStudent(string &s_Name,long &s_Numble)
	{
		cout << "学生的姓名是 " << s_Name << endl;
		cout << "学生的学号是 " << s_Numble <<endl;
	}


};
int main(int argc, char *argv[])
{
	Student stu;
	stu.s_Name = "Michael";
	stu.s_Numble = 1805130334;
	stu.displayStudent(stu.s_Name,stu.s_Numble);
}
```

输出结果：

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/uTools_1649077374818.png)

封装意义二：

类在设计时，可以把属性和行为放在不同的权限下，加以控制

访问权限有三种：

1.public 公共权限  类内可以访问 类外可以访问

2.protected 保护权限 类内可以访问 类外不可以访问

3.private 私有权限 类内可以访问 类外不可以访问

```
#include <iostream>
#include <string>
using namespace std;
//公共权限 public 类内可以访问 类外可以访问
//保护权限 protected 类内可以访问 类外不可以访问 子类可以访问父类
//私有权限 private 类内可以访问 类外不可以访问
//案例：创建一个人的类 姓名为公共权限 车为保护权限 银行卡密码为私有权限
class person{
	public:
	string p_Name;
	protected:
	string p_Car;
	private:
	int p_Passwad;
};
int main(int argc, char *argv[])
{
	person zs;
	zs.p_Name = "WayJay";
}


```

在实验过程中，可以发现除了姓名可以访问，其他都不能访问，也就是类内可以访问私有和保护权限下的属性，类外不可以访问私有和保护权限。

#### 4.1.2 struct 和class 的区别

在C++中struct 和class唯一的区别就在于默认的访问权限不同

区别：

struct默认权限为公共；

class默认权限为私有；

```
#include <iostream>
using namespace std;
struct C1
{
	string C_Name;
};
class C2
{
	string C_Name;
};


int main(int argc, char *argv[])
{ 
	C1 str;
	C2 cla;
	str.C_Name = "张三";
}
```

当我们想要访问class内部的属性时，发现是访问不了的。

#### 4.1.3成员属性设置为私有

优点1：将所有成员属性设置为私有，可以自己控制读写权限

优点2：对于写权限，可以检测数据的有效性

示例：设置一个人类，属性包括姓名，年龄，情人

设置姓名为可读可写，年龄为只读，情人为只写

```
#include <iostream>
#include <string>
using namespace std;
//成员属性私有化
//可以控制读写权限
//检测数据的有效性

//设置一个人类
class person
{
	public:
	//设置姓名 可读可写
	void setName(string name)
	{
		p_Name = name;
	}
	string getName()
	{
		return p_Name;
	}
	//获取年龄 只读
	int getAges()
	{
		p_Ages = 15;
		return p_Ages;
	}
	//设置情人 只写
	void setLover(string lover)
	{
		p_Lover =lover;
	}
	//姓名 可读可写
	string p_Name;
	//年龄 只读
	int p_Ages;
	//情人， 只写 笑死，为什么会有情人这个属性
	string p_Lover;
};
int main(int argc, char *argv[])
{
	person a;
	string name = "WayJay";
	a.setName(name);
	cout << a.getName() << endl;
	cout << a.getAges() << endl;
	string lover = "小花";
	a.setLover(lover);
}
```

**练习案例1:设计立方体**

设计立方体

求出立方体的面积和体积

分别用全局函数和成员函数判断两个立方体是否相等

```
#include <iostream>
#include <string>
using namespace std;
//先设置一个立方体类
class Cube
{
	private:
	float c_L;
	float c_W;
	float c_H;
	public:
	//设置长
	void setL(float L)
	{
		c_L = L;
	}
	//获取长
	float getL()
	{
		return c_L;
	}
	//设置宽
	void setW(float W)
	{
		c_W = W;
	}
	//获取宽
	float getW()
	{
		return c_W;
	}
	//设置高
	void setH(float H)
	{
		c_H = H;
	}
	//获取高
	float getH()
	{
		return c_H;
	}
	//计算其体积
	double volume()
	{
		return c_L*c_W*c_H;
	}
	//计算其面积
	double area()
	{
		double area = c_L*c_W*2+c_L*c_H*2+c_W*c_H*2;
		return area;
	}
};
//全局函数判断两个立方体是否相等,老师的想法也是一样，用布尔类型来判断
bool judgeCube(Cube &c1,Cube &c2)
{
	if(c1.getL() == c2.getL() && c1.getW() == c2.getW() && c1.getH() == c2.getH())
	{
		return true;
	}
	else
	return false;
}
int main(int argc, char *argv[])
{
	float L1 =10.5;
	float W1 =5.5;
	float H1 =8.5;
	float L2 =10.5;
	float W2 =6.5;
	float H2 =8.5;
	Cube lft1;
	Cube lft2;
	lft1.setL(L1);
	lft1.setW(W1);
	lft1.setH(H1);
	lft2.setL(L2);
	lft2.setW(W2);
	lft2.setH(H2);
	cout << "立方体1的体积是" << lft1.volume() << endl;
	cout << "立方体1的面积是" << lft1.area() << endl;
	cout << "立方体2的体积是" << lft2.volume() << endl;
	cout << "立方体2的面积是" << lft2.area() << endl;
	bool ret = judgeCube(lft1,lft2);
	if(ret)
	{
		cout << "这两个立方体是同一个" <<endl;
	}
	else
	cout << "这两个立方体不是同一个" <<endl;
}
```

**练习案例：** 设置一个圆类，设置一个点类

判断他们之间的位置关系

```
#include <iostream>
#include <string>
using namespace std;
//练习案例2
//设计一个圆类（circle），设计一个点类（point），计算点和圆的关系
//那么点和圆有什么关系呢，点在圆上？点在圆内，点在圆外？
//怎么判断呢，利用坐标关系
//设置一个点类，属性有x和y坐标
class Point
{
	private:
	int p_X;
	int p_Y;
	public:
	//设置x坐标
	void setX(int x)
	{
		p_X = x;
	}
	//获取x坐标
	int getX()
	{
		return p_X;
	}
	//设置y坐标
	void setY(int y)
	{
		p_Y = y;
	}
	//获取Y坐标
	int getY()
	{
		return p_Y;
	}
};
//设置一个圆类。属性有圆心，半径
//行为有设置获取半径，设置获取圆心
class Circle
{
	private:
	Point c_Center;
	int c_R;
	public:
	void setR(int R)
	{
		c_R = R;
	}
	int getR()
	{
		return c_R;
	}
	//设置圆心坐标
	void setCenter(Point center)
	{
		c_Center = center;
	}
	//获取圆心坐标
	Point getCenter()
	{
		return c_Center;
	}
};
//全局函数判断，圆和点之间关系
void isCenter(Circle &c,Point &p)
{
	int distance =
	(c.getCenter().getX()-p.getX())*(c.getCenter().getX()-p.getX())
	+(c.getCenter().getY() - p.getY())*(c.getCenter().getY() - p.getY());
	int R2 = c.getR()*c.getR();
	if(distance == R2)
	cout << "点在圆上" << endl;
	else if(distance > R2)
	cout << "点在圆外" << endl;
	else
	cout << "点在圆内" << endl;
}

int main(int argc, char *argv[])
{
	//圆、点实例化
	Circle c;
	Point p;
	Point center;
	int centerX =0;
	int centerY=0;
	cout << "请输入圆心的X坐标 ";
	cin >> centerX;
	cout << "请输入圆心的Y坐标 ";
	cin >> centerY;
	center.setX(centerX);
	center.setY(centerY);
	//设置圆心坐标、半径
	int r;
	cout << "请输入圆心的半径 ";
	cin >> r;
	c.setR(r);
	//设置圆心坐标
	c.setCenter(center);
	//设置点的坐标
	int p_X ;
	int p_Y ;
	cout << "请输入点的X坐标 ";
	cin >> p_X;
	cout << "请输入点的Y坐标 ";
	cin >> p_Y;
	p.setX(p_X);
	p.setY(p_Y);
	isCenter(c,p);
}
```

这个案例的难点就是这个圆的属性圆心包含了点的属性坐标，这样子就需要创建一个新的定义类型，有点类似于嵌套的结构体。

### 4.2对象的初始化和清理

·生活中我们买的电子产品都基本会有出厂设置，在某一天我们不用时也会删除一些自己信息数据保证安全

·c++中的面向对象来源于生活，每个对象也都会有初始设置以及对象销毁前的清理数据的设置。

#### 4.2.1构造函数和析构函数

对象的初始化和清理时两个非常重要的安全问题

一个对象或者变量没有初始状态，对其使用后果是未知

同样的使用完一个对象或变量，没有及时清理，也会造成一定的安全问题。

c++利用了构造函数和析构函数解决上述问题，这两个函数将会被编译器自动调用，完成对象初始化和清理工作。对象的初始化和清理工作是编译器强制要我们做的事情，因此如果我们不提析造和析构，编译器会提供编译器提供的构造函数和析构函数是空实现。

·构造函数：主要作用在于创建对象时为对象的成员属性赋值，构造函数有编译器自动调用，无须手动调用。

·析构函数：主要作用在于对象销毁前系统自动调用，执行一些清理工作。

构造函数语法：类名{}

1.构造函数，没有返回值也不写void

2.函数名称与类名相同

3.构造函数可以有参数，因此可以发生重载

4.程序在调用对象时候会自动调用构造。无须手动调用，而且只会调用一次。

析构函数语法：~类名(){}

1.析构函数，没有返回值也不写void

2.函数名称与类名相同，在名称前加上符号

3.析构函数不可以有参数，因此不可以发生重载

4.程序在对象销毁前会自动调用析构，无须手动调用，而且只会调用一次

```
#include <iostream>
using namespace std;
//构造函数和析构函数
//对象的初始化和清理
class Person
{
public:
//构造函数 进行初始化操作
	Person()
	{
		cout << "peson构造函数的调用" << endl;
	}
//析构函数 进行清理的操作
	~Person()
	{
		cout << "person析构函数的调用" << endl; // 析构函数只有在释放后再清理
		//相比在主函数中，需要在程序结束后才会调用
	}
};
void test21()
{
	Person p;
}

int main(int argc, char *argv[])
{ 
	test21();

	std::cout << "Hello world!" << std::endl;
}
```

#### 4.2.2构造函数的分类及调用

两种分类方式：

按参数分为：有参构造和无参构造

按类型分为：普通构造和拷贝构造

三种调用方式：

括号法：

注意事项1：在调用默认构造函数时，不要加()

如果加了(),编译器会认为这是一个函数的声明

类似于void func();这是一个函数的声明

注意事项2：不要利用拷贝构造函数 初始化匿名对象 编译器会认为 Person(p3) == Person p3 ，就是认为这是对象的实例化，就是创建一个对象。

显示法：

	//显示法调用无参构造函数
	 Person p1;
	//用显示法调用有参构造函数
	 Person p2 = Person(10);
	//用显示法调用拷贝函数
	 Person p3 = Person(p2);

隐式转换法：

	Person p4 = 10; //隐式转换法，调用有参构造函数
	Person p5 = p4;//隐式转换法 调用拷贝构造函数

```
#include <iostream>
using namespace std;
//构造函数的分类及调用
class Person
{
public:
//无参构造函数 也叫默认构造函数
	Person ()
	{
		cout << "无参构造函数" << endl;
	}
	Person(int a)
	{
		cout << "有参构造函数" <<endl;
	}
	//拷贝构造函数
	Person(const Person &p)
	{
		//将传入的人身上的所有属性，拷贝到我身上
		age = p.age;
		cout << "拷贝构造函数" << endl;
	}
	~Person()
	{
		cout << "析构函数" << endl;
	}
	int age;
};
//怎么调用呢
void test01()
{
	//1.括号法
	// Person p1; //默认构造函数的调用
	// Person p2(10); //调用有参构造函数
	// Person p3(p2);
	// //注意事项
	// //在调用默认构造函数的时候，不要加（）
	// cout << "p2的年龄 " << p2.age << endl;
	// cout << "p3的年龄 "  << p3.age <<endl;
	//2.显示法
	//用显示法调用无参或者是默认调用函数
	// Person p1;
	// //用显示法调用有参构造函数
	// Person p2 = Person(10);
	// //用显示法调用拷贝函数
	// Person p3 = Person(p2);
	// Person(10); //匿名对象，当前行执行结束后，
	//             //系统会立即回收掉匿名对象
	//注意事项，不要利用拷贝构造函数 初始化匿名对象 编译器会认为 Person(p3) == Person p3;
	//3.隐式转换法
	Person p4 = 10; //隐式转换法，调用有参构造函数
	Person p5 = p4;//隐式转换法 调用拷贝构造函数
	
}
int main(int argc, char *argv[])
{
	test01();

}
```

#### 4.2.3拷贝构造函数调用时机

C++中拷贝构造函数调用时机通常有三种情况：

·使用一个已经创建完毕的对象来初始化一个新对象

·值传递的方式给函数参数传值

·以值方式返回局部对象

```
#include <iostream>
using namespace std;
//拷贝构造函数调用时机
//使用一个已经创建完毕的对象来初始化一个新对象
// 值传递的方式给函数参数传值
// 以值方式返回局部对象
//先创建一个类
//无参构造函数 有参构造函数 拷贝构造函数

class Person
{
public:
	Person()
	{
		cout << "无参构造函数" << endl; 
	}
	Person(int a)
	{
		age = a;
		cout << "有参构造函数" <<endl;
	}
	Person(const Person &p)
	{
		age = p.age;
		cout << "拷贝构造函数" << endl;
	}
	~Person()
	{
		cout <<"析构函数" << endl;
	}
	int age;
};
//使用一个已经创建完毕的对象来初始化一个新对象
void test01()
{
	Person p1;
	Person p2(10);
	Person p3(p2);
	cout << p3.age <<endl;
}
// 值传递的方式给函数参数传值
void doWork(Person p)
{

}

void test02()
{
	Person p;//默认构造函数调用
	doWork(p); //Person p = p;相当于上次学的隐式转换法
}
//值方式返回局部对象
Person doWork2()
{
	Person p1;
	return p1;
}
void test03()
{
	Person p = doWork2();
}

int main(int argc, char *argv[])
{
	// test01();
	// test02();
	test03(); //输出无参构造函数，拷贝构造函数，析构函数，析构函数
}
```

听完这节课有一点点懵逼，大概就是拷贝构造函数的两种调用方法，一个是括号法，用于用一个已经创建完毕的对象来初始化一个新对象，一个是隐式转换法，用于值传递的方式给函数参数传值，以值方式返回局部对象，这两种的调用方法都类似于隐式转换法的

```
Person p4;
Person p = p4;
```

#### 4.2.4构造函数调用规则

默认情况下，C++编译器至少给一个类添加至少三个函数

**1.**默认构造函数（无参，函数体为空）

**2.**默认析构函数（无参，函数体为空）

**3.**默认拷贝函数，对属性进行拷贝

析构函数调用规则如下;

·如果用户定义有参构造函数，C++不在提供默认无参构造函数，但是会提供默认拷贝函数

·如果用户定义拷贝构造函数，C++不会再提供其他构造函数

```
#include <iostream>
using namespace std;
//构造函数调用规则
//默认构造函数（无参 函数体为空）
//默认析构函数（无参 函数体为空）
//默认拷贝构造函数，对属性进行值拷贝
//第一步 创建一个结构体
//如果我们写了有参构造函数，编译器就不再提供默认构造，
//依然提供拷贝，大概就是如果你写了有参构造函数，那么默认的无参构造函数就没有了
//这时你去调用无参构造函数，编译器就会报错，但是编译器默认的拷贝构造函数依然存在，
//编译器不会报错
//当我们写了拷贝构造函数，编译器就不会再提供默认构造函数和有参构造函数了
//当自己写了高级构造函数后，那么低级的构造函数，编译器就不会再提供
class Person
{
public:
	Person ()
	{
		cout << "默认构造函数调用" << endl;
	}
	//析构函数调用
	Person (int age)
	{
		m_age = age;
		cout << "有参函数调用" << endl;
	}
	//拷贝构造函数，对属性进行值传递
	// Person(const Person & p)
	// {
	// 	m_age = p.m_age;
	// }
	//构造函数
	~Person()
	{
		cout << "析构函数调用" << endl;
	}
	int m_age;

};
void test01()
{
	Person p;
	p.m_age = 18;
	Person p2(p); // 将拷贝构造函数注释掉，并不会报错
	cout << "p2的年龄为" << p2.m_age << endl;
}
void test02()
{
	Person p(28);
	Person p1(p);
}
int main(int argc, char *argv[])
{
	test02();
}
```

结论：编译器会自动提供三种函数：默认构造函数、析构函数、拷贝函数

如果我们自己定义了有参构造哈数，那么编译器不会再提供默认构造函数

如果我们自己定义了拷贝构造函数，那么编译器不会再提供默认构造函数和有参构造函数

#### 4.2.5 深拷贝和浅拷贝

深浅拷贝是面试经典问题，也是一个常见的坑

浅拷贝：：简单的赋值拷贝操作

深拷贝：在堆区重新申请空间，进行拷贝操作

```
#include <iostream>
#include <string>
using namespace std;
//深拷贝和浅拷贝
class Person
{
public:
	Person()
	{
		cout << "默认构造函数" <<endl;
	}
	Person(int age,int height)
	{
		m_age = age;
		m_Height = new int (height);
		cout << "有参构造函数" <<endl;
	}
	Person(const Person & p)
	{
		m_age = p.m_age;
		// m_Height = p.m_Height;//编译器默认实现的代码
		m_Height =  new int (*p.m_Height); //为p.Height重新new一个堆区，这样就不会重复释放同一个堆区了
	}
	~Person()
	{
		//这里会出现一个问题，就是堆区的数据会被二次释放，这就是浅拷贝的一个问题所在
		//free(): double free detected in tcache 2 Aborted
		//怎么解决呢，利用深拷贝来解决
		//自己实现拷贝构造函数，解决浅拷贝带来的问题
		//析构代码，将堆区开辟数据做释放操作
		if(m_Height != NULL)
		delete m_Height;
		m_Height = NULL; //
		cout << "析构函数" << endl;
	}
	int m_age;
	int *m_Height;
};
void test01()
{
	Person p(18,160);
	Person p2(p);
	cout << "p2的年龄" << p2.m_age<< endl ;
	cout << "p2的身高" << *p2.m_Height<< endl ;
}
int main(int argc, char *argv[])
{
	test01();
}
```

结论：利用深拷贝解决浅拷贝的值传递在堆区重复释放的问题

#### 4.2.6 初始化列表

**作用：** C++提供了初始化列表语法，用来初始化属性

**语法：** 构造函数():属性1（值1），属性2（值2）...（）

```
#include <iostream>
using namespace std;
class Person
{
public:
//传统初始化操作
	// Person(int A,int B,int C)
	// {
	// 	m_A = A;
	// 	m_B = B;
	// 	m_C = C;
	// }
	int m_A;
	int m_B;
	int m_C;
//初始化列表初始化属性
	Person():m_A(10),m_B(20),m_C(30)
	{

	}
//另一种语法:
   Person(int A,int B,int C):m_A(A),m_B(B),m_C(C)
   {

   }

};
void test01()
{
	Person p(10,20,30);
	cout << p.m_A<< endl;
	cout << p.m_B<< endl;
	cout << p.m_C<< endl;
}
void test02()
{
	Person p2;
	cout << p2.m_A<< endl;
	cout << p2.m_B<< endl;
	cout << p2.m_C<< endl;
}
int main(int argc, char *argv[])
{
	test01();
	// test02();
}
```

结论：用最后一种语法，可以在初始化时赋不同的值

```
   Person(int A,int B,int C):m_A(A),m_B(B),m_C(C)
   {

   }
```

#### 4.2.7 类对象作为类成员

C++类种的成员可以是另一个类的对象，称该成员为对象成员

```
#include <iostream>
#include <string>
using namespace std;
//类对象作为类成员

//手机类
class Phone
{
public:
	//品牌
	//赋值操作
    Phone(string pname)
	{
		p_Brand = pname;
		cout <<"phone的函数调用"<<endl;
	}
	~Phone()
	{
		cout <<"phone的析构函数调用"<<endl;
	}
	string p_Brand;
};
//人类
class Person
{
public:
	//姓名
	//person m_phone - pname;//隐式转换法
	Person(string name,string pname):m_Name(name),m_Phone(pname)
	{
		cout <<"person的函数调用"<<endl;
	}
	~Person()
	{
		cout <<"person的析构函数调用"<<endl;
	}
	string m_Name;
	//手机
	Phone m_Phone;
	//使用上节课学到的初始化列表来初始化
};
void test02()
{
	Person p2("李四","三星");
	cout <<p2.m_Name<< "手机的品牌是" << p2.m_Phone.p_Brand<<endl; 
}
int main(int argc, char *argv[])
{
	// string brand = "华为";
	// string name = "张三";
	// Person p;
	// p.m_Name = name;
	// p.m_Phone.p_Brand = brand;
	test02();
	Person p("张三","华为");
	cout <<p.m_Name<< "手机的品牌是" << p.m_Phone.p_Brand<<endl;
} 
```

输出结果：

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/类对象及成员.png)

结论：可以看出在函数调用过程中，当类中成员是其他类时，我们称该成员为对象成员，构造的顺序时：先调用对象成员的构造，再调用本类构造

析构的顺序是：先调用本类析构，再调用对象成员析构

#### 4.2.8 静态成员

静态成员就是再成员变量和成员函数前加上关键字static，称为静态成员

静态成员分为：

·所有对象共享同一份数据

·在编译阶段分配内存

·类内声明，类外初始化

静态成员函数

·所有对象共享一个函数

·静态成员函数只能访问静态成员变量

```
#include <iostream>
using namespace std;
//静态成员函数
//所有对象共享同一个函数
//静态成员函数只能访问静态成员变量
class Person
{
public:
//静态成员函数
	static void func()
	{
		m_A = 100;//静态成员变量是共享的
		// m_B = 100; //非静态成员变量，静态成员函数调用不了
		// 无法区分是哪个对象的m_B
		cout << "static void func调用"<< endl;
	}
	//静态成员变量
	static int m_A;
	int m_B;
};
void test()
{
	Person p;
	// 两种调用方式
	//通过对象访问
	p.func();
	//通过类名访问
	Person::func();

}
int main(int argc, char *argv[])
{
	test();
}
```

结论：静态成员函数的调用有两种方式：1.过类名访问

2.通过对象访问

静态成员函数只能调用静态成员变量

### 4.3 C++对象模型和this指针

#### 4.3.1 成员变量和成员函数分开存储

在C++中，类内的成员变量和成员函数是分开存储的

只有非静态成员变量才属于类的对象上

```
#include <iostream>
using namespace std;
//成员变量和成员函数 分开存储的
//先创建一个类
class Person
{
public:

};
class People
{
public:
	int m_A; //非静态成员变量，属于类的对象上
	static int m_B;//静态成员变量，不属于类的对象上
	void func()//非静态成员函数，和非静态成员变量是分开存储的
	{}
};
void test01()
{
	Person p;
	//空对象占用内存空间为：1
	//C++编译器会给每个空对象也分配一个字节空间
	//是为了区分空对象占内存的位置
	//每个空对象都应该有自己的一个内存位置
	cout << sizeof(p) <<endl;
}
void test02()
{
	People p;
	cout << sizeof(p) <<endl;
}

int main(int argc, char *argv[])
{
	test01();
	test02();
}
```

结论：只有非静态成员变量属于类的对象上，非静态成员变量和非静态成员函数是分开存储的

#### 4.3.2 this指针概念

通过4.3.1，在c++中成员变量和成员函数是分开存储的

每一个非静态成员函数只会诞生一份函数实例，也就是说多个同类型的对象会共用一块代码？

那么这一块代码是如何区分哪个对象调用自己的呢？

c++通过提供特殊的对象指针，this指针，解决上述问题，this指针指向被调用成员函数所属的对象

this指针式隐含每一个非静态成员函数内的一种指针

this指针不需要定义，直接使用即可

**this指针的用途** 

·当形参和成员变量同名时，可以用this指针区分

·在类的非静态成员函数中返回对象本身，可使用return *this

```
#include <iostream>
using namespace std;
//this指针用途
//1.解决名称冲突
//2.返回对象本身用*this
class Person
{
public:
	Person(int ages)
	{
		//this指针指向的时被调用的成员函数p所属的对象
		//解决了重名冲突
		this->ages= ages;
	}
	Person &PersonAddAge(Person &p)
	{
		this->ages += p.ages;
		return *this;//返回对象本身，例如我们现在调用的p2，那么返回就是p2
	}
	int ages;
};
void test01()
{
	Person p1(18);
	cout << p1.ages <<endl;
}
void test02()
{
	Person p2(18);
	//链式编程思想
	//返回person类型本身，再次调用person类内的行为或者属性
	p2.PersonAddAge(p2).PersonAddAge(p2);
	cout << p2.ages <<endl;
}
int main(int argc, char *argv[])
{
	test02();
}
```

#### 4.3.3 空指针访问成员函数

C++中空指针也是可以调用成员函数的，但是也要注意有没有用到this指针

如果用到this指针，需要加以判断保证代码的健壮性

**代码实验** 

```
class Person
{
	public:
	void showClassName()
	{
		cout << "this is Person class" << endl;
	}
	void showPersonAge()
	{

		cout << "Person's ages are" << m_Age <<endl;
	}
	int m_Age;
};
void test01()
{
	Person *p = NULL;
	p->showClassName();
	p->showPersonAge();
}
```

当调用函数showPersonAge时，报错

Segmentation fault （段错误）

报错指针是因为传入的指针为NULL，空指针不能指向m_Age这个对象

怎么解决呢

```
在showPersonAgeh函数中加入一个判断语句
if(this == NULL)
{
return;//空指针直接return
}
这样子就不会报错了
```

#### 4.3.4 const修饰成员函数

**常函数**： 

·成员函数后加const后，我们称中国函数为常函数 

·常函数内不可以修改成员属性

·成员属性声明加关键字mutable后，在常函数中依然可以修改

​	**常对象：**

·声明对象前加const称该对象为常对象

·常对象只能调用常函数

```
#include <iostream>
using namespace std;
//常函数
class Person
{
	public:
	Person()
	{

	}
	//this指针的本质 是指针常量 指针的指向是不可以修改的
	//类似于int * const p或者是Person const *this 修饰的是p和this的地址
	//当函数后加上const后，指针就类似于const Person * const p 指针的值和地址都不能被修改
	void showPerson() const
	{
		m_B = 100;
	}
	int m_A;
	mutable int m_B;//当加上mutable后，这就是一个特殊变量，常函数可以修改这个值
};
//常对象
void test01()
{
	const Person p;//在创建的对象前加上const就是常对象,这个对象的值也不能修改
	//若需要修改，需要在变量前加上mutable
	p.showPerson();//常对象只能调用常函数，不能调用其他函数
}
int main(int argc, char *argv[])
{
	std::cout << "Hello world!" << std::endl;
}

```

结论：常函数和常对象只能调用加上mutable的特殊变量，而且常对象只能调用常函数，不能调用其他函数。

### 4.4 友元

生活中你的家有客厅(Pubc),有你的卧室(Private)
客厅所有来的客人都可以进去，但是你的卧室是私有的，也就是说只有你能进去
但是呢，你也可以允许你的好闺蜜好基友进去。
在程序里，有些私有属性也想让类外特殊的一些函数或者类进行访问，就需要用到友元的技术

**友元的目的**就是让一个函数或者类访问另一个类中私有成员
友元的关键字为friend

**友元的三种实现**
·全局函数做友元
·类做友元
·成员函数做友元

**全局函数做友元**

```
#include <iostream>
using namespace std;
//友元
//全局函数做友元
//类做友元
//成员函数做友元
//房子类
class Building 
{
	friend void goodGay(Building &Building);//全局函数声明，让goodgay这个函数可以访问building类中的私有成员
public:
	Building()
	{
		m_BedRoom = "卧室";
		m_SittringRoom = "客厅";
	}
	string m_SittringRoom;//客厅
private:
	string m_BedRoom;//卧室，私有属性

};

//全局函数
void goodGay(Building &Building)
{
	cout << "好基友全局函数，正在访问： " << Building.m_BedRoom<< endl;
	cout << "好基友全局函数，正在访问： " << Building.m_SittringRoom<< endl;
}
void test01()
{
	Building building;
	goodGay(building);
}
int main(int argc, char *argv[])
{
	test01();
}
	
```

**类做友元**

```
#include <iostream>
using namespace std;
//类做友元
class Building
{
	friend class GoodGay;
public:
	Building();
	//属性有客厅和卧室 
	//卧室为私有的
	string m_SittingRoom;
private:
	string m_BedRoom;
};
class GoodGay
{
public:
	GoodGay();
	void visit();//参观函数， 访问Building中的属性
	Building * building;
};
//类外访问类内函数
Building::Building()
{
	m_SittingRoom  = "客厅";
	m_BedRoom = "卧室";
}	
GoodGay::GoodGay()
{
	//创建一个建筑物的对象
	building = new Building;//new一个Building
}
void GoodGay::visit()
{
	cout <<"好基友正在访问" << building->m_SittingRoom << endl;
	cout <<"好基友正在访问" <<building->m_BedRoom <<endl;
}
void test001()
{
	GoodGay gg;
	gg.visit();
}
int main(int argc, char *argv[])
{
	test001();
}
```

**成员函数做友元**

```
#include <iostream>
#include <string>
using namespace std;
//成员函数做友元
class Building;
class GoodGay
{
public:
	GoodGay();
	void visit();//让visit函数可以访问Building中私有成员
	void visit2();//让visit2不能访问Building中私有成员
	Building * building;
};
class Building
{
	friend void GoodGay::visit();
public:
	//属性：客厅 私有属性：卧室
	Building();
	string m_SittingRoom;
private:
	string m_BedRoom;
};
Building::Building()
{
	m_SittingRoom = "客厅";
	m_BedRoom = "卧室";
}
GoodGay::GoodGay()
{
	building = new Building;
}
void GoodGay::visit()
{
	cout << "你的好基友正在访问" << building->m_BedRoom << endl;
}
void GoodGay::visit2()
{
	cout << "你的朋友正在访问" << building->m_SittingRoom << endl;
}
void test01()
{
	GoodGay gg;
	gg.visit();
	gg.visit2();
}
int main(int argc, char *argv[])
{
	test01();
}
```

**结论：** 不论是哪种友元，只需要在你需要访问私有属性或者行为的类里，加上friend对这个函数进行声明即可。

### 4.5运算符重载

运算符重载概念：对已有的运算符重新进行定义，赋予其另一种功能，以适应不同的数据类型

#### 4.5.1加号运算符重载

作用：实现两个自定义数据类型相加的运算

怎么进行两个对象的相加再赋值给第三个对象，用重载+运算符operator+ 

代码实验：

```
#include <iostream>
using namespace std;
class Person
{
public:
	Person operator+(Person &p)
	{
	Person temp;
	temp.m_A = this->m_A + p.m_A;
	return temp;
	}
	int m_A;
};
Person operator+(Person & p,int a)
{
	Person temp;
	temp.m_A = p.m_A + a;
	return temp;
}
int main(int argc, char *argv[])
{
	Person p1;
	p1.m_A = 110;
	Person p2;
	p2.m_A = 20;
	Person p3 = p1 + p2;
	Person p4 = p3 + 100;
	cout << p3.m_A << endl;
	cout << p4.m_A << endl;
}
```

结论：运算符重载可以发生在成员函数，也可以发生在全局函数

还能发生函数重载。

#### 4.5.2 左移重载运算符

作用：可以输出自定义数据类型

```
#include <iostream>
using namespace std;
//左移运算符重载
class Person
{
public:
	Person operator<<(Person &p)
	{
		Person temp;
		temp.m_A = this->m_A << 1;
		return temp;
	}
	int m_A;
	int m_B;
};
Person operator<<(Person &p,int a)
{
	Person temp;
	temp.m_A = p.m_A << a;
	return temp;
}
ostream &operator<<(ostream &cout , Person &p)
{
	cout << "m_A=" << p.m_A << "m_B= " << p.m_B;
	return cout; //返回输出流类型，链式编程，可以连续调用
}
int main(int argc, char *argv[])
{
	Person p;
	p.m_A = 100;
	p.m_B = 10;
	cout << p << endl;
	Person x = p<<1;
	Person y = operator<<(p,3);
	cout << x.m_A << endl;
	cout << y.m_A << endl;
}
```

#### 4.5.3 递增递减运算符

**代码实验：**

递增实验：

```
#include <iostream>
using namespace std;
//递减运算符重载
class MyInteger
{
	friend ostream &operator<<(ostream &cout,MyInteger &&myint);
	friend ostream &operator<<(ostream &cout,MyInteger &myint);
private:
	/* data */
	int m_Num;
public:
	MyInteger(/* args */)
	{
		m_Num = 30;
	}
	//前置++运算符重载
	MyInteger &operator++()
	{
		m_Num++;
		return *this;
	}
	//后置++运算符重载
	MyInteger operator++(int)
	{
		MyInteger temp = *this;
		m_Num++;
		return temp;
	}
	~MyInteger()
	{}
};
ostream &operator<<(ostream &cout,MyInteger &myint)
{
	cout << myint.m_Num;
	return cout;
}
ostream &operator<<(ostream &cout,MyInteger &&myint)
{
	cout << myint.m_Num;
	return cout;
}
void test01()//测试前置++ //测试成功
{
	MyInteger myint;
	cout << ++(++myint) <<endl;
	cout << myint << endl;
}
void test02()
{
	MyInteger myint;
	cout << myint++ <<endl;
	cout << myint << endl;
}
int main(int argc, char *argv[])
{
	test01();
	test02();
}
```

递减实验：

```
#include <iostream>
using namespace std;
//递减运算符重载
class MyInteger
{
	friend ostream &operator<<(ostream &cout,MyInteger &&myint);
	friend ostream &operator<<(ostream &cout,MyInteger &myint);
private:
	/* data */
	int m_Num;
public:
	MyInteger(/* args */)
	{
		m_Num = 30;
	}
	//前置--运算符重载
	MyInteger &operator--()
	{
		m_Num--;
		return *this;
	}
	//后置--运算符重载
	MyInteger operator--(int)
	{
		MyInteger temp = *this;
		m_Num--;
		return temp;
	}
	~MyInteger()
	{}
};
ostream &operator<<(ostream &cout,MyInteger &myint)
{
	cout << myint.m_Num;
	return cout;
}
ostream &operator<<(ostream &cout,MyInteger &&myint)
{
	cout << myint.m_Num;
	return cout;
}
void test01()//测试前置-- //测试成功
{
	MyInteger myint;
	cout << --(--myint) <<endl;
	cout << myint << endl;
}
void test02()
{
	MyInteger myint;
	cout << myint-- <<endl;
	cout << myint << endl;
}
int main(int argc, char *argv[])
{
	test01();
	test02();
}
```

**结论：前置++（--）和后置++（--）的区别是，前置返回的是引用，后置返回的是一个MyInteger类型的值，在引用cout时也有区别，前置的参数是作为左值，后置的参数是作为右值**

#### 4.5.4赋值运算符重载

C++编译器至少给一个类添加4个函数

1.默认构造函数

2.默认析构函数

3.默认拷贝函数

4.赋值运算符operator = ，对属性进行值拷贝

如果类中有属性指向堆区，做赋值操作时也会出现深浅拷贝问题

```
#include <iostream>
using namespace std;
//又回到了深浅拷贝的问题
class Person
{
private:
	/* data */
public:
	int *m_Age;
	//写一个重载赋值运算符
	Person operator=(const Person &p);
	Person(int ages);
	// Person(const Person & p);
	~Person();
};
Person::Person(int ages)
{
	m_Age = new int(ages);
}
Person::~Person()
{
}
// 	//堆区需要手动释放
// 	if(m_Age != NULL)
// 	{
// 		delete m_Age;
// 		m_Age = NULL;
// 	}
// }
// Person::Person(const Person & p)
// {
// 	m_Age = new int(*p.m_Age);//深拷贝函数
// }
Person Person::operator=(const Person &p)
{
	//先判断是否有属性在堆区，如果有就先释放干净，然后再深拷贝
	if(m_Age != NULL)
	{
		delete m_Age;
		m_Age = NULL;
	}
	m_Age = new int(*p.m_Age);//深拷贝
	return *this;
}
void test01()
{
	Person p1(10);
	Person p2(20);
	Person p3(30);
	p2 = p1 = p3;//调用拷贝函数
	cout << *p1.m_Age << endl;
	cout << *p2.m_Age << endl;
	cout << *p3.m_Age << endl;
	cout << p1.m_Age << endl;
	cout << p2.m_Age << endl;
	cout << p3.m_Age << endl;
	
}
int main(int argc, char *argv[])
{
	test01();
}
```

#### 4.5.5 函数调用运算符重载

·函数调用运算符（）也考验重载

·由于重载后使用的方式非常像函数的调用，因此称为仿函数

·仿函数没有固定写法，非常灵活

```
#include <iostream>
using namespace std;
//函数调用运算符重载
//打印输出类
class Myprint
{
public:
	//重载运算符调用
	void operator()(string test);
	int operator()(int a, int b);

};
void Myprint::operator()(string test)
{
	cout << test << endl;
}
int Myprint::operator()(int a , int b)
{
	int temp = a + b;
	return temp;
}
void test()
{
	Myprint mp;
	mp("hello world！");
	cout << mp(10,20) << endl;
}
int main(int argc, char *argv[])
{
	test();
}
```

