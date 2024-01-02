---
title: C++实战-通讯录
abbrlink: 17216
date: 2022-03-27 00:36:10
tags:
  -	C++
categories:
  - 学习	
  - 笔记
cover: https://picsum.photos/id/223/300/300
---

这个通讯录是我学习C++差不多一个月以来，第一次去尝试写一个完整的可以说是项目吧，确确实实是我一边画图，一个功能一个功能实现的，也很感谢B站黑马程序员的教程，从本来什么都不会，到现在可以独立思考写代码，虽然代码还是有很多bug，但是没有关系，能够进步我就很知足了

由于刚开始学习C++ ，写的不是很好

但是基本功能实现了

希望可以不断练习来提高自己代码水平

以下是菜鸟写的一部分代码

```
#include <iostream>
#include <string>
using namespace std;
#define Person_Max 1000
// 通讯录是一个可以记录亲人、好友信息的工具。
// 本教程主要利用C++来实现一个通讯录管理系统
// 系统中需要实现的功能如下：
// 添加联系人：向通讯录中添加新人，信息包括（姓名、性别、年龄、联系电话、家庭住址）最多记录1000人
// 显示联系人：显示通讯录中所有联系人信息
// 删除联系人：按照姓名进行删除指定联系人
// 查找联系人：按照姓名查看指定联系人信息
// 修改联系人：按照姓名重新修改指定联系人
// 清空联系人：清空通讯录中所有信息
// 退出通讯录：退出当前使用的通讯录
// 第一个功能 菜单显示功能
void showMenu()
{
	cout << "************"<< "1.添加联系人" << "************" <<endl;
	cout << "************"<< "2.显示联系人" << "************" <<endl;
	cout << "************"<< "3.删除联系人" << "************" <<endl;
	cout << "************"<< "4.查找联系人" << "************" <<endl;
	cout << "************"<< "5.修改联系人" << "************" <<endl;
	cout << "************"<< "6.清空联系人" << "************" <<endl;
	cout << "************"<< "7.退出通讯录" << "************" <<endl;
}
//联系人结构体
struct PersonList
{
	string name;
	string sex;
	int ages;
	long int phone;
	string address;
};
//通讯录结构体
struct AddressPerson
{
	struct PersonList Person[Person_Max];
	int m_size;
};
//添加联系人功能
void AddPerson (AddressPerson *abs)
{ 
	if (abs->m_size < 1000)
	{
		/* code */
		cout << "输入需要添加的联系人的姓名" << endl;
		cin >> abs ->Person[abs->m_size].name;
		cout << "输入需要添加的联系人的性别" << endl;
		cin >> abs ->Person[abs->m_size].sex;
		if(abs ->Person[abs->m_size].sex == "男" || abs ->Person[abs->m_size].sex == "女"){
		}
		else{
			cout << "输入有误,重新输入：" << endl;
			cin >> abs ->Person[abs->m_size].sex;
		}
		cout << "输入需要添加的联系人的年龄" << endl;
		cin >> abs ->Person[abs->m_size].ages;
		cout << "输入需要添加的联系人的家庭地址" << endl;
		cin >> abs ->Person[abs->m_size].address;
		cout << "输入需要添加的联系人的联系电话" << endl;
		cin >> abs ->Person[abs->m_size].phone;
		cout << "添加成功" << endl;
	}
	else
	{
		cout << "通讯录已满" <<endl;
	}
	abs->m_size+=1;
	getchar();
}
//判断联系人列表是否存在此联系人
void FindPerson(AddressPerson *abs)
{
	string name;
	cout << "请输入要找的人的名字" ;
	cin >> name;
	for (size_t i = 0; i <= abs->m_size; i++)
	{
		/* code */
		if (abs->Person[i].name == name)
		{
			cout << "联系人姓名： "<< abs->Person[i].name << " ";
			cout << "联系人性别： "<< abs->Person[i].sex << " ";
			cout << "联系人年龄： "<< abs->Person[i].ages << " ";
			cout << "联系人电话： "<< abs->Person[i].phone << " ";
			cout << "联系人家庭住址： "<< abs->Person[i].address << endl;
			break;
		}
		else
		{
			cout << "查无此人 请重新输入"<< endl;
			cin >> name;
		}
	}
}
//显示联系人
void ShowPerson(AddressPerson *abs)
{
	for (size_t i = 0; i <= abs->m_size; i++)
	{
		/* code */
		cout << "联系人姓名"<< abs->Person[i].name << " ";
		cout << "联系人性别"<< abs->Person[i].sex << " ";
		cout << "联系人年龄"<< abs->Person[i].ages << " ";
		cout << "联系人电话"<< abs->Person[i].phone << " ";
		cout << "联系人家庭住址"<< abs->Person[i].address << endl;
	}
	
}
//删除联系人
void DeletePerson(AddressPerson *abs)
{
	string name;
	int ret;
	cout << "请输入要删除联系人的名字： " ;
	cin >> name;
	for (size_t i = 0; i <= abs->m_size; i++)
	{
		/* code */
		if (abs->Person[i].name == name)
		{
			ret = i;
			break;
		}
		else
		{
			cout << "查无此人 请重新输入"<< endl;
			ret = -1;
		}
	}
	if(ret != -1)
	{
		for (size_t j = ret; j < abs->m_size; j++)
		{
			/* code */
			abs->Person[j] = abs->Person[j+1];
		}
		abs->m_size--;
	}
}
//修改联系人信息
void ModifyPerson(AddressPerson *abs)
{
	string name;
	string option;
	int ret = 0;
	cout << "请输入要修改的联系人的名字： " ;
	cin >> name;
	for (size_t i = 0; i <= abs->m_size; i++)
	{
		/* code */
		if (abs->Person[i].name == name)
		{
			ret = i;
			break;
		}
		else
		{
			cout << "查无此人 请重新输入"<< endl;
			ret = -1;
		}
	}
	if(ret != -1)
	{
		cout << "请输入要修改的部分" << endl;
		cin >> option;
	    if(option == "姓名")
		{
			cout << "输入你要修改的姓名： " << endl;
			cin >> abs->Person[ret].name;
		}
		else if (option == "性别")
		{
			cout << "输入你要修改的性别： " << endl;
			cin >> abs->Person[ret].sex;
		}
		else if (option == "年龄")
		{
			cout << "输入你要修改的年龄： " << endl;
			cin >> abs->Person[ret].ages;
		}
		else if (option == "电话")
		{
			cout << "输入你要修改的电话： " << endl;
			cin >> abs->Person[ret].phone;
		}
		else if (option == "家庭住址")
		{
			cout << "输入你要修改的家庭住址： " << endl;
			cin >> abs->Person[ret].address;
		}
		else{
			cout << "输入信息有误，请重新输入" <<endl;
			cin >> option;
		}	
	}
}
//清空联系人
void cls(AddressPerson *abs)
{
	cout << "清空联系人"<<endl;
	abs->m_size = 0;
	abs->Person[abs->m_size] = {};
}
int main(int argc, char *argv[])
{
	AddressPerson abs;
	abs.m_size = 0;
	int Select = 0;
	while(true)
	{
		//通讯录选项
		showMenu();
		cout << "选择你要做的选项(1~7):" ;
		cin >> Select;
		switch (Select)
		{
			case 1:
			AddPerson(&abs);
			  //添加联系人
				break;
			case 2: 
			ShowPerson(&abs); //显示联系人
				break;
			case 3:  
			DeletePerson(&abs);//删除联系人
				break;
			case 4:  
			 FindPerson(&abs);//查找联系人
				break;
			case 5: 
			ModifyPerson(&abs); //修改联系人
				break;
			case 6: 
			cls(&abs); //清空联系人
				break;
			case 7: 
			cout << "欢迎下次使用" << endl;//退出通讯录
			return 0;
				break;
			default: 
				cout <<"输入选项有误"<< endl;
				break;
		}
    }  
	
}
```

