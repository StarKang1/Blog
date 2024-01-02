---
title: C++核心编程(三)
tags: C++
categories:
  - 学习
  - 笔记
cover: 'https://picsum.photos/id/100/300/300'
abbrlink: 46393
date: 2022-04-12 22:21:31
---

### 4.3 多态

#### 4.7.1 多态的基本概念

多态是C++面向对象三大特性之一

多态分为两类

·静态多态：函数重载  和 运算符重载属于静态多态，复用函数名

·动态多态：派生类和虚函数实现运行时多态

静态多态和动态多态区别：

·静态多态的函数地址早绑定，编译阶段确定函数地址

·动态多态的函数地址晚绑定，运行阶段确定函数地址

```
#include <iostream>
using namespace std;
//多态 
//动物类
class Animal
{
private:
	/* data */
public:
	virtual void speak();
	Animal(/* args */);
	~Animal();
};
void Animal::speak()
{
	cout << "动物在说话" << endl;
}
Animal::Animal(/* args */)
{
}

Animal::~Animal()
{
}
class Cat:public Animal
{
public:
	 void speak();
};
void Cat::speak()
{
	cout << "小猫在说话" << endl;
}
void doSpeak(Animal &Animal)
{
	Animal.speak();
}
void test()
{
	Cat cat;
	doSpeak(cat);//这时候调用的是父类中的speak函数
	//函数地址早绑定，在编译器编译过程中绑定，地址绑定在了父类的speak函数
	//对父类的speak函数做虚函数处理，实现地址晚绑定
}
int main(int argc, char *argv[])
{
	test();
}
//动态多态满足条件
//1.有继承关系
//2.子类重写父类的虚函数
```

#### 4.7.2 多态案例-计算器类

案例描述：

分别利用普通写法和多态写法，设计实现两个操作数进行运算的计算器类。

多态的优点：

·代码组织结构清晰

·可读性强

·利于前期和后期的扩展以及维护

**代码实验：**

```
#include <iostream>
using namespace std;
//案例计算器
//开发中 提倡 开闭原则
//开闭原则：对扩展进行开发，对修改进行关闭
class Caculator
{
private:
	/* data */
public:
	virtual float getResult()
	{
		return 0;
	}
	float m_Num1;
	float m_Num2;
	Caculator(/* args */);
	~Caculator();
};

Caculator::Caculator(/* args */)
{
}

Caculator::~Caculator()
{
}
//加法计算器
class AddCaculator:public Caculator
{
public:
	float getResult()
	{
		return m_Num1+m_Num2;
	}
};
//减法计算器
class SubtractiveCalculator:public Caculator
{
public:
	float getResult()
	{
		return m_Num1-m_Num2;
	}
};
// 乘法计算器
class MultiplicationCalculator:public Caculator
{
public:
	float getResult()
	{
		return m_Num1*m_Num2;
	}
};
//除法计算器
class DivisionCalculator:public Caculator
{
public:
	float getResult()
	{
		return m_Num1/m_Num2;
	}
};
void caculate(float num,char ch)
{
	if(ch == '+')
	{
		Caculator * add = new AddCaculator;
		add ->m_Num1 = num;
		cin >> add ->m_Num2;
		cout << "结果为"<< add->getResult() << endl;
		delete add;
	}
	else if(ch == '-')
	{
		Caculator * sub = new SubtractiveCalculator;
		sub->m_Num1 = num;
		cin >> sub->m_Num2;
		cout<< "结果为"<< sub->getResult() << endl;
		delete sub;
	}
	else if(ch == '*')
	{
		Caculator * mul = new MultiplicationCalculator;
		mul->m_Num1 = num;
		cin >> mul->m_Num2;
		cout << "结果为" << mul->getResult() << endl;
		delete mul;
	}
	else if(ch == '/')
	{
		Caculator * div = new DivisionCalculator;
		div->m_Num1 = num;
		cin >> div->m_Num2;
		if (div->m_Num2 == 0)
		{
			cout << "error! Input again" << endl;
			cin >> div->m_Num2;
		}
		cout << "结果为" << div->getResult() << endl;
		delete div;
	}
}
int main(int argc, char *argv[])
{
	float num=0;
	cin >> num;
	char ch;
	cin >> ch;
	caculate(num,ch);
}
```

#### 4.7.3 纯虚函数和抽象类

在多态中，通常父类中虚函数的实现是毫无意义的，主要都是调用子类重写的内容。

因此可以将虚函数改为纯虚函数

纯虚函数语法：virtual 返回值类型 函数名（参数列表）= 0；

当类中有了纯虚函数，这个类型也称为抽象类

**抽象类特点：**

·无法实例化对象

·子类必须重写抽象类中的纯虚函数

```
#include <iostream>
using namespace std;
//纯虚函数和抽象类
//语法 vitrual 返回值类型 函数名（参数列表）=0
class Base
{
private:
	/* data */
public:
	virtual int getResult() = 0;
	Base(/* args */);
	~Base();
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
	int getResult()//子类重写
	{
		int m_A=100;
		return m_A;
	}
};
void test()
{
	//Base b;//base内部有纯虚函数，该类为抽象类，无法实例化该对象
	Son s;
	cout << s.getResult() << endl;

}
int main(int argc, char *argv[])
{
	test();
}
```

#### 4.7.4 多态案例二-制作饮品

案例描述：制作饮品的大致流程为：煮水-冲泡 -  倒入杯中-加入辅料

利用多态技术实现本案例，提供抽象制作饮品基类，提供子类制作咖啡和茶叶

```
#include <iostream>
#include <string>
using namespace std;
//案例描述：制作饮品的大致流程为：煮水-冲泡 -  倒入杯中-加入辅料
//利用多态技术实现本案例，提供抽象制作饮品基类，提供子类制作咖啡和
class Drink
{
private:
	/* data */
public:
	//煮开水	
	virtual void boilWater() =0;
	//冲泡
	virtual void brew() = 0;
	//倒入杯中
	virtual void pourInCup() = 0;
	//加入辅料
	virtual void join() = 0;
	//制作饮品
	void makeDrink()
	{
		boilWater();
		brew();
		pourInCup();
		join();
	}
	Drink(/* args */);
	~Drink();
};
Drink::Drink(/* args */)
{
}
Drink::~Drink()
{
}
class Coffer:public Drink
{
public:
	virtual void boilWater()
	{
		cout << "烧开水" << endl;
	}
	virtual void brew()
	{
		cout << "冲泡咖啡" << endl; 
	}
	virtual void pourInCup() 
	{
		cout << "将开水倒入杯中" << endl;
	}
	virtual void join()
	{
		cout << "加入糖和咖啡" << endl;
	}
};
class Tea:public Drink
{
public:
	virtual void boilWater()
	{
		cout << "烧开水" << endl;
	}
	virtual void brew()
	{
		cout << "冲泡茶叶" << endl; 
	}
	virtual void pourInCup() 
	{
		cout << "将开水倒入杯中" << endl;
	}
	virtual void join()
	{
		cout << "加入柠檬" << endl;
	}
};
void make(Drink * drink)
{
	drink->makeDrink();
}
void switchDrink(string drink)
{
   if(drink == "茶")
   {
	   make(new Tea);
   }
   else if(drink == "咖啡")
   {
	   make(new Coffer);
   }
   else
   {
	   cout << "暂无该饮品,请重新选择" << endl;
   }
}

int main(int argc, char *argv[])
{
	string drink;
	cin >> drink;
	switchDrink(drink);
}
```

#### 4.7.5 虚析构和纯虚析构

多态使用时，如果子类中有属性开辟在堆区，那么父类指针在释放时无法调用到子类的析构代码

解决方式：将父类中的析构函数改为虚析构或者纯虚析构

虚析构和纯虚析构共性：

·可以解决父类指针释放子类对象

·都需要有具体的函数体现

虚析构和纯虚析构区别：

·如果时纯虚析构，该类属于抽象类，无法实例化对象

```
#include <iostream>
using namespace std;
//虚析构和纯虚析构
class Animal
{
private:
	/* data */
public:
	virtual void speak() = 0;
	Animal(/* args */);
	//利用虚析构可以解决 父类指针释放子类对象释放不完全的问题
	//virtual ~Animal();//将父类的析构改为虚析构，就可以调用子类中的析构函数
	//纯虚析构
	virtual ~Animal() = 0;//父类的析构有被调用到，所以需要在类外对其实现
};

Animal::Animal(/* args */)
{
	cout << "animal的构造函数调用" << endl;
}

Animal::~Animal()
{
	cout << "animal析构函数调用" << endl;
}
class Cat:public Animal
{
public:
	virtual void speak();
	Cat(string name)
	{
		cout << "cat的构造函数调用" << endl;
		m_Name = new string(name);
	}
	~Cat()
	{
		cout << "cat析构函数调用" << endl;
		if(m_Name != NULL)
		delete m_Name;
		m_Name = NULL;
	}
    string *m_Name;
};
void Cat::speak()
{
	cout << *m_Name << "小猫在说话" << endl;
}
void test()
{
	Animal * tom = new Cat("Tom");
	tom->speak();
//父类指针在析构时候 不会调用子类中析构函数 导致子类如果有堆区属性 出现内存泄漏情况
	delete tom;
}
int main(int argc, char *argv[])
{
	test();
}
```

#### 4.7.6 多态案例三-组装电脑

案例描述：

电脑主要组成部分为CPU（用于计算），显卡（用于显示），内存条（用于存储），将每个零件封装出抽象基类，并且提供不同的厂商生产不同的零件，例如intel厂商和lenovo厂商，创建电脑类提供让电脑工作的函数，并且调用每个零件的接口，测试时组装三台不同的电脑工作

```
#include <iostream>
using namespace std;
//电脑组装 三部分： CPU、显卡、内存条
class CPU
{
private:
	/* data */
public:
	virtual void calculate() = 0;
	CPU(/* args */);
	~CPU();
};

CPU::CPU(/* args */)
{
}

CPU::~CPU()
{
}
class GraphicsCard
{
private:
	/* data */
public:
	virtual void display() = 0;
	GraphicsCard(/* args */);
	~GraphicsCard();
};

GraphicsCard::GraphicsCard(/* args */)
{
}

GraphicsCard::~GraphicsCard()
{
}
class MermoryChips
{
private:
	/* data */
public:
	virtual void storage() = 0;
	MermoryChips(/* args */);
	~MermoryChips();
};

MermoryChips::MermoryChips(/* args */)
{
}

MermoryChips::~MermoryChips()
{
}
class Computer
{
private:
	CPU *m_Cpu;
	MermoryChips *m_Mermory;
	GraphicsCard *m_Card;
	/* data */
public:
//电脑的组装 零件的接口
	Computer(CPU* cpu , GraphicsCard *card,MermoryChips *mermory,int num)
	{
		cout << "Computer" << num << " is working normally"<< endl;
		m_Cpu = cpu;
		m_Mermory = mermory;
		m_Card = card;
	}
	//零件的工作
	void work()
	{
		m_Cpu->calculate();
		m_Card->display();
		m_Mermory->storage();
		cout << "------------------------" << endl;
	}
	Computer(/* args */);
	~Computer();
};

Computer::Computer(/* args */)
{
}

Computer::~Computer()
{
}
class Intel:public CPU , public GraphicsCard , public MermoryChips
{
private:
	/* data */
public:
	virtual void calculate()
	{
		cout << "Intel's CPU is working" << endl;
	}
	virtual void display()
	{
		cout << "Intel's GraphicsCard is working" << endl;
	}
	virtual void storage()
	{
		cout << "Intel's MermoryChips is working" << endl;
	}
};
class Lenovo:public CPU , public GraphicsCard , public MermoryChips
{
private:
	/* data */
public:
	virtual void calculate()
	{
		cout << "Lenovo's CPU is working" << endl;
	}
	virtual void display()
	{
		cout << "Lenovo's GraphicsCard is working" << endl;
	}
	virtual void storage()
	{
		cout << "Lenovo's MermoryChips is working" << endl;
	}
};
//组装三台电脑
void tasks()
{
	Computer * Computer1 = new Computer(new Lenovo,new Intel,new Intel,1);
	Computer1->work();
	delete Computer1;
	Computer * Computer2 = new Computer(new Lenovo,new Lenovo,new Lenovo,2);
	Computer2->work();
	delete Computer2;
	Computer * Computer3 = new Computer(new Intel,new Intel,new Intel,3);
	Computer3->work();
	delete Computer3;
}
int main(int argc, char *argv[])
{
	tasks();
}
```

