---
title: C++核心编程(二)
tags: C+=
categories:
  - 笔记
  - 学习
cover: 'https://picsum.photos/id/345/300/300'
abbrlink: 9627
date: 2022-04-12 00:11:39
---

#### 4.6 继承

继承是面向对象三大特性之一

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/屏幕截图 2022-04-12 124718.png)

下级别的成员拥有上一级的共性，还有自己的共性

这时候就可以用继承的方式，减少重复代码

#### 4.6.1继承的基本语法

例如我们看到很多网站中，都有公共的头部，公共的底部，公共的侧边栏。

**普通实现：**

```
#include <iostream>
using namespace std;
//继承基本语法
//普通实现页面

//BasePage页面
class BasePage
{
private:
	/* data */
public:
	void header();
	void footer();
	void left();
	void separator();
	BasePage(/* args */);
	~BasePage();
};
void BasePage::header()
{
	cout << "首页、公开课、登录、注册...()" << endl;
}
void BasePage::footer()
{
	cout << "帮助中心、交流合作、站内地图...(公共底部)" << endl;
}
void BasePage::left()
{
	cout << "Java、Python、C++...（公共分类列表）" << endl;
}
void BasePage::separator()
{
	cout << "------------------------------" << endl;
}
BasePage::BasePage()
{
		void header()
;
}
BasePage::~BasePage()
{
}
//Python页面
// class Python
// {
// private:
// 	/* data */
// public:
// 	void header();
// 	void footer();
// 	void left();
// 	void content();
// 	Python(/* args */);
// 	~Python();
// };
// void Python::header()
// {
// 	cout << "首页、公开课、登录、注册...()" << endl;
// }
// void Python::footer()
// {
// 	cout << "帮助中心、交流合作、站内地图...(公共底部)" << endl;
// }
// void Python::left()
// {
// 	cout << "BasePage、Python、C++...（公共分类列表）" << endl;
// }
// void Python::content()
// {
// 	cout << "BasePage学科视频" << endl;
// }

// Python::Python(/* args */)
// {
// }

// Python::~Python()
// {
// }
//Java页
class Java:public BasePage
{
public:
	void content();
};
void Java::content()
{
	cout << "Java学科视频 "<< endl;
};
class Python:public BasePage
{
public:
	void content();
};
void Python::content()
{
	cout << "Python学科视频" << endl;
}
class Cplusplus:public BasePage
{
public:
	void content();
};
void Cplusplus::content()
{
	cout << "C++学科视频" << endl;
}
void test()
{
    Java ja;
	ja.header();
	ja.footer();
	ja.left();
	ja.content();
	ja.separator();
	Python py;
	py.header();
	py.footer();
	py.left();
	py.content();
	py.separator();
    Cplusplus cpp;
	cpp.header();
	cpp.footer();
	cpp.left();
	cpp.content();
	cpp.separator();
}

int main(int argc, char *argv[])
{
	test();
}
```

结论：继承可以减少不必要的重复代码.

语法：class 子类：public 父类

#### 4.6.2继承方式

**继承的语法：** class **子类**：继承方式 **父类**

继承方式：

·公共继承：在父类中公共部分的内容还是公共部分的内容，保护部分的内容依然是保护部分的内容。

·保护继承：在父类中公共的内容和保护的内容在子类中都是保护的内容。

·私有继承：在父类中公共部分的内容和保护部分的内容都变为子类私有部分的内容。

注意事项：父类中私有权限的内容，子类不管是哪种继承方式，都无法访问

保护继承的特性是类内可以访问，类外无法访问

**代码实验：**

```
#include <iostream>
using namespace std;
//继承方式 ：公共继承 保护继承 私有继承
class Base
{
private:
	/* data */
	string m_Lover;
public:
	string m_House;
	string m_Car;
	Base(/* args */);
	~Base();
protected:
	int m_Money;
	
};

Base::Base(/* args */)
{
}

Base::~Base()
{
}
//公共继承
class FirstSon:public Base
{
public:
	void func()
	{
		m_Car = "法拉利";//父类中的公共权限成员，到子类中依然是公共权限
		m_Money = 100;//父类中的保护权限成员，依然是保护权限
	}
protected:
	void func2()
	{
		m_Money = 1000;
	}
};
//保护继承
class SecondSon:protected Base
{
public:
	void func()
	{
		m_Car = "兰博基尼";
		m_Money = 10000;
	}

};
class ThirdDaughter:private Base
{
public:
	void func()
	{
		m_Car = "劳斯莱斯";
		m_Money = 10000;
	}

};
void test()
{
	FirstSon one;
	SecondSon two;
	ThirdDaughter three;
	// cout << two.m_Car << endl;保护继承后父类中公共权限下的内容变为子类中的保护权限的内容
	//类外不可以访问
	//cout << three.m_Car << endl; //私有继承后父类中的公共权限和保护权限下的内容都变为子类中
	//私有权限下的内容，因此不能访问
}
int main(int argc, char *argv[])
{
	test();
}
```

#### 4.6.3 继承中的对象模型

```
#include <iostream>
using namespace std;
//继承中对象模型
class Base
{
private:
	int m_A;
	/* data */
public:
	int m_B;
	Base(/* args */);
	~Base();
protected:
	int m_C;
};

Base::Base(/* args */)
{
}

Base::~Base()
{
}
class Son:public Base
{
public:
	int m_D;
};
void test()
{
	Son s;
	cout << sizeof(s)  << endl;//16
	//父类中所有非静态成员属性都会被子类继承下去
	//父类中私有成员属性是被编译器给隐藏了，
	//虽然访问不到，但是确确实实被继承下来了

int main(int argc, char *argv[])
{
	test();
}
```

**结论：** 父类中所有非静态成员属性都会被子类继承下去，父类中私有成员属性是被编译器给隐藏了，虽然访问不到，但是确确实实被继承下来了

#### 4.6.4 继承中构造和析构顺序

子类继承父类后，当创建子类对象，也会调用父类的构造函数

问题：父类和子类的构造和析构顺序是谁先谁后？

**代码实验：** 

```
#include <iostream>
using namespace std;
//继承中构造和析构顺序
class Base
{
private:
	/* data */
public:
	Base(/* args */);
	~Base();
};

Base::Base(/* args */)
{
	cout << "父类中构造函数调用" << endl;
}

Base::~Base()
{
	cout << "父类中析构函数调用" << endl;
}
class Son:public Base
{
public:
	Son();
	~Son();
};
Son::Son()
{
	cout << "子类中构造函数调用" << endl;
}
Son::~Son()
{
	cout << "子类中析构函数调用" << endl;
}
void test()
{
	Son s;
}
int main(int argc, char *argv[])
{
	test();
}
```

输出结果：

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/屏幕截图 2022-04-12 151648.png)



结论：构造函数是父类先调用，子类再调用；父类的析构函数在子类的析构函数释放结束后再释放

#### 4.6.5继承同名成员处理方式

:dark_sunglasses:问题： 当子类于父类出现同名的成员，如何通过子类，访问到子类或父类同名的数据呢？

:scissors:   访问子类同名成员 直接访问即可

:scissors:   反问父类同名成员 需要加作用域

```
#include <iostream>
using namespace std;
//继承中同名成员的访问
class Base
{
private:
	/* data */
public:
	int m_A  = 10000;
	void func();
	void func(int);
	Base(/* args */);
	~Base();
};
void Base::func()
{
	cout << "Base的func函数调用" << endl;
}
void Base::func(int)
{
	cout << "父类中另一func函数调用" << endl;
}
Base::Base(/* args */)
{
}

Base::~Base()
{
}
class Son:public Base
{
public:
	int m_A;
	void func()
	{
		cout << "Son的func函数调用" << endl;
	}
};
//同名成员属性处理
void test()
{
	Son s;
	s.m_A = 100;
	cout  << "s.m_A = " << s.m_A << endl;//当子类和父类中的同名成员，子类中是直接访问的
	cout  << "Base.m_A = " << s.Base::m_A << endl;//当需要访问父类中的成员，需要加上作用域
}
//同名成员函数处理
void test02()
{
	Son s;
	s.func();//子类的同名成员函数直接调用
	s.Base::func();//父类的同名成员函数通过作用域调用
	// s.func(10);//子类同名成员函数隐藏了父类中同名成员函数重载
	s.Base::func(10);//需要加作用域才能访问
}
int main(int argc, char *argv[])
{
	test();
	test02();
}
```

输出结果;

![](https://cdn.jsdelivr.net/gh/StarKang1/picgopicture/img/继承同名成员.png)

#### 4.6.6继承同名静态成员处理方式

问题：继承中的静态成员在子类对象上如何进行访问

静态成员和非静态成员出现同名，处理方式一致

·访问子类同名成员 直接访问即可

·访问父类同名成 需要加作用域

```
#include <iostream>
using namespace std;
//继承同名静态成员处理方式
//创建一个父类
class Base
{
private:
	/* data */
public:
	static int m_A;
	static void func();
	Base(/* args */);
	~Base();
};
int Base::m_A = 100;
void Base::func()
{
	cout << "Base的func函数调用" << endl;
}
Base::Base(/* args */)
{
}

Base::~Base()
{
}
//创建一个子类继承父类
class Son:public Base
{
public:
	static int m_A;
	static void func();
};
int Son::m_A = 1000;
void Son::func()
{
	cout << "Son的func函数调用" << endl;
}
//同名静态成员属性测试
void test()
{
	Son s;
	// s.m_A = 100;
	// s.Base::m_A = 1000;
	cout << "s.m_A = " << s.m_A << endl;
	cout << "Base.m_A = " << s.Base::m_A << endl;
}
//同名静态成员函数测试
void test2()
{
	Son s;
	s.func();
	s.Base::func();
}
int main(int argc, char *argv[])
{
	test();
	test2();
}
```

结论：同名静态成员处理方式和同名成员处理方式一样

#### 4.6.7 多继承语法

C++允许一个类继承多个类

语法：class 子类：继承 父类1 ， 继承方式  父类2...

多继承可能会引发父类有同名成员出现，需要加作用域区分

C++实际开发中不建议用多继承

```
#include <iostream>
using namespace std;
//多继承语法
//设置两个父类
class Base
{
private:
	/* data */
public:
	int m_A;
	Base(/* args */);
	~Base();
};

Base::Base(/* args */)
{
}

Base::~Base()
{
}
class Base2
{
private:
	/* data */
public:
	int m_B;
	Base2(/* args */);
	~Base2();
};

Base2::Base2(/* args */)
{
}

Base2::~Base2()
{
}
//创建一个子类 继承两个父类
class Son:public Base ,public Base2
{
public:
	int m_C;
};
//测试，子类是否可以调用父类中的成员属性
void test()
{
	Son s;
	s.m_A = 100;
	s.m_B = 10;
	s.m_C = 1;
	cout << "s.m_A = " << s.m_A << endl;
	cout << "s.m_B = " << s.m_B << endl;
	cout << "s.m_C = " << s.m_C << endl;
	cout << "sizeof = " << sizeof(s) << endl;
}
int main(int argc, char *argv[])
{
	test();
}
```

结论：子类继承父类，会将多个父类的所有成员属性都继承，因此sizeof（s） = 12；

#### 4.6.8 菱形继承

菱形继承概念：

两个派生类同时继承同一个基类

又有某个类同时继承着两个派生类

这种继承被称为菱形继承

```
#include <iostream>
using namespace std;
//菱形继承
//先创建一个父类
class Animal
{
private:
	/* data */
public:
	int m_Num;
	Animal(/* args */);
	~Animal();
};

Animal::Animal(/* args */)
{
}

Animal::~Animal()
{
}
//创建两个子类继承父类
//利用虚继承 解决菱形继承的问题
//继承之前 加上关键字 virtual 变为虚继承
//Animal类称为虚基类
//创建一个羊类
class Sheep:virtual public Animal
{
public:
	// Sheep();
	// ~Sheep();


};
//创建一个骆驼类
class Camel:virtual public Animal
{
public:
	// Camel();
	// ~Camel();

};
//最后创建一个子类继承羊和骆驼--羊驼
class Alpaca:public Sheep ,public Camel
{
public:
	// Alpaca();
	// ~Alpaca();

};
//测试
void test()
{
	Alpaca al;
	al.Sheep::m_Num = 1000;
	al.Camel::m_Num = 10000;
	cout << "al.Sheep::m_Num = " << al.Sheep::m_Num << endl;
	cout << "al.Camel::m_Num = " << al.Camel::m_Num <<endl;
	cout << "al.m_Num = " << al.m_Num <<endl;
}
int main(int argc, char *argv[])
{
	test();
}
```

结论：在继承之前加上virtual后，保留一份数据，不会导致资源浪费
