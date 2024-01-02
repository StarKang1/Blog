---
title: 初识C++
tags: C/C++
categories: 学习
abbrlink: 43028
date: 2022-02-24 13:07:41
cover: https://picsum.photos/id/513/300/300
---

# C++课程学习笔记

## 第一阶段：C++基础语法入门

### 1.变量

存在的意义：方便管理内存空间

变量创建的语法： 数据类型 变量名 =变量初始值

例如 int a =10；//变量初始化

### 2.常量

作用：用于记录程序中不可更改的数据

1.#define宏常量

2.const修饰的变量

### 3.关键字

如int float long double 

变量取名要避免与关键字重复

### 4.标识符命名规则

作用：C++ 规定给标识符（变量、常量）命名时，有一套规则

**1.**标识符不能是关键字

**2.**第一个标识符必须为字母或下划线

**3.**标识符字母区分大小写

建议取名采用驼峰命名法

### 5.数据类型

#### 1.整型

![](https://gitee.com/xu-weijian/pic-go/raw/master/img/~0QM3$CQ$8VTDRU~E5TO7EL.png)

可以利用size of求出数据类型占用内存多大

例如short num1 =10；

cout << "short占用内存空间为： " << sizeof(num) << end1;

![](https://gitee.com/xu-weijian/pic-go/raw/master/img/RAK9VEVYUUW{H}_3NWA8[GL.png)

#### 2.实型

1.单精度实型float

2.双精度实型double

![](https://gitee.com/xu-weijian/pic-go/raw/master/img/9~((LDI%5BSC6E%7D%7D5JT)@$GSG.png)

#### 3.字符型

作用：字符型变量用于显示单个字符

语法：char ch = 'a';

C和C++中字符型变量☞占用1个字节

字符型变量不是把字符本身放到内存存储，而是将对应的ASCIII编码放入到存储单元

char只占一个字节

![](https://gitee.com/xu-weijian/pic-go/raw/master/img/BHFG18ESC2MTWZ@U@CGF~4Y.png)

ASCII码表

| 二进制   | 十进制 | 十六进制 | 字符/缩写                                    |
| -------- | ------ | -------- | -------------------------------------------- |
| 00000000 | 0      | 00       | NUL (NULL)                                   |
| 00000001 | 1      | 01       | SOH (Start Of Headling)                      |
| 00000010 | 2      | 02       | STX (Start Of Text)                          |
| 00000011 | 3      | 03       | ETX (End Of Text)                            |
| 00000100 | 4      | 04       | EOT (End Of Transmission)                    |
| 00000101 | 5      | 05       | ENQ (Enquiry)                                |
| 00000110 | 6      | 06       | ACK (Acknowledge)                            |
| 00000111 | 7      | 07       | BEL (Bell)                                   |
| 00001000 | 8      | 08       | BS (Backspace)                               |
| 00001001 | 9      | 09       | HT (Horizontal Tab)                          |
| 00001010 | 10     | 0A       | LF/NL(Line Feed/New Line)                    |
| 00001011 | 11     | 0B       | VT (Vertical Tab)                            |
| 00001100 | 12     | 0C       | FF/NP (Form Feed/New Page)                   |
| 00001101 | 13     | 0D       | CR (Carriage Return)                         |
| 00001110 | 14     | 0E       | SO (Shift Out)                               |
| 00001111 | 15     | 0F       | SI (Shift In)                                |
| 00010000 | 16     | 10       | DLE (Data Link Escape)                       |
| 00010001 | 17     | 11       | DC1/XON (Device Control 1/Transmission On)   |
| 00010010 | 18     | 12       | DC2 (Device Control 2)                       |
| 00010011 | 19     | 13       | DC3/XOFF (Device Control 3/Transmission Off) |
| 00010100 | 20     | 14       | DC4 (Device Control 4)                       |
| 00010101 | 21     | 15       | NAK (Negative Acknowledge)                   |
| 00010110 | 22     | 16       | SYN (Synchronous Idle)                       |
| 00010111 | 23     | 17       | ETB (End of Transmission Block)              |
| 00011000 | 24     | 18       | CAN (Cancel)                                 |
| 00011001 | 25     | 19       | EM (End of Medium)                           |
| 00011010 | 26     | 1A       | SUB (Substitute)                             |
| 00011011 | 27     | 1B       | ESC (Escape)                                 |
| 00011100 | 28     | 1C       | FS (File Separator)                          |
| 00011101 | 29     | 1D       | GS (Group Separator)                         |
| 00011110 | 30     | 1E       | RS (Record Separator)                        |
| 00011111 | 31     | 1F       | US (Unit Separator)                          |
| 00100000 | 32     | 20       | (Space)                                      |
| 00100001 | 33     | 21       | !                                            |
| 00100010 | 34     | 22       | "                                            |
| 00100011 | 35     | 23       | #                                            |
| 00100100 | 36     | 24       | $                                            |
| 00100101 | 37     | 25       | %                                            |
| 00100110 | 38     | 26       | &                                            |
| 00100111 | 39     | 27       | '                                            |
| 00101000 | 40     | 28       | (                                            |
| 00101001 | 41     | 29       | )                                            |
| 00101010 | 42     | 2A       | *                                            |
| 00101011 | 43     | 2B       | +                                            |
| 00101100 | 44     | 2C       | ,                                            |
| 00101101 | 45     | 2D       | -                                            |
| 00101110 | 46     | 2E       | .                                            |
| 00101111 | 47     | 2F       | /                                            |
| 00110000 | 48     | 30       | 0                                            |
| 00110001 | 49     | 31       | 1                                            |
| 00110010 | 50     | 32       | 2                                            |
| 00110011 | 51     | 33       | 3                                            |
| 00110100 | 52     | 34       | 4                                            |
| 00110101 | 53     | 35       | 5                                            |
| 00110110 | 54     | 36       | 6                                            |
| 00110111 | 55     | 37       | 7                                            |
| 00111000 | 56     | 38       | 8                                            |
| 00111001 | 57     | 39       | 9                                            |
| 00111010 | 58     | 3A       | :                                            |
| 00111011 | 59     | 3B       | ;                                            |
| 00111100 | 60     | 3C       | <                                            |
| 00111101 | 61     | 3D       | =                                            |
| 00111110 | 62     | 3E       | >                                            |
| 00111111 | 63     | 3F       | ?                                            |
| 01000000 | 64     | 40       | @                                            |
| 01000001 | 65     | 41       | A                                            |
| 01000010 | 66     | 42       | B                                            |
| 01000011 | 67     | 43       | C                                            |
| 01000100 | 68     | 44       | D                                            |
| 01000101 | 69     | 45       | E                                            |
| 01000110 | 70     | 46       | F                                            |
| 01000111 | 71     | 47       | G                                            |
| 01001000 | 72     | 48       | H                                            |
| 01001001 | 73     | 49       | I                                            |
| 01001010 | 74     | 4A       | J                                            |
| 01001011 | 75     | 4B       | K                                            |
| 01001100 | 76     | 4C       | L                                            |
| 01001101 | 77     | 4D       | M                                            |
| 01001110 | 78     | 4E       | N                                            |
| 01001111 | 79     | 4F       | O                                            |
| 01010000 | 80     | 50       | P                                            |
| 01010001 | 81     | 51       | Q                                            |
| 01010010 | 82     | 52       | R                                            |
| 01010011 | 83     | 53       | S                                            |
| 01010100 | 84     | 54       | T                                            |
| 01010101 | 85     | 55       | U                                            |
| 01010110 | 86     | 56       | V                                            |
| 01010111 | 87     | 57       | W                                            |
| 01011000 | 88     | 58       | X                                            |
| 01011001 | 89     | 59       | Y                                            |
| 01011010 | 90     | 5A       | Z                                            |
| 01011011 | 91     | 5B       | [                                            |
| 01011100 | 92     | 5C       | \                                            |
| 01011101 | 93     | 5D       | ]                                            |
| 01011110 | 94     | 5E       | ^                                            |
| 01011111 | 95     | 5F       | _                                            |
| 01100000 | 96     | 60       | `                                            |
| 01100001 | 97     | 61       | a                                            |
| 1100010 | 98   | 62   | b             |
| ------- | ---- | ---- | ------------- |
| 1100011 | 99   | 63   | c             |
| 1100100 | 100  | 64   | d             |
| 1100101 | 101  | 65   | e             |
| 1100110 | 102  | 66   | f             |
| 1100111 | 103  | 67   | g             |
| 1101000 | 104  | 68   | h             |
| 1101001 | 105  | 69   | i             |
| 1101010 | 106  | 6A   | j             |
| 1101011 | 107  | 6B   | k             |
| 1101100 | 108  | 6C   | l             |
| 1101101 | 109  | 6D   | m             |
| 1101110 | 110  | 6E   | n             |
| 1101111 | 111  | 6F   | o             |
| 1110000 | 112  | 70   | p             |
| 1110001 | 113  | 71   | q             |
| 1110010 | 114  | 72   | r             |
| 1110011 | 115  | 73   | s             |
| 1110100 | 116  | 74   | t             |
| 1110101 | 117  | 75   | u             |
| 1110110 | 118  | 76   | v             |
| 1110111 | 119  | 77   | w             |
| 1111000 | 120  | 78   | x             |
| 1111001 | 121  | 79   | y             |
| 1111010 | 122  | 7A   | z             |
| 1111011 | 123  | 7B   | {             |
| 1111100 | 124  | 7C   | \|            |
| 1111101 | 125  | 7D   | }             |
| 1111110 | 126  | 7E   | ~             |
| 1111111 | 127  | 7F   | DEL  (Delete) |

#### 4.转义字符

**1./n 换行**

**2.// 输出一个/**

**3./t 水平等距离输出数据**

#### 6.字符串型

作用：用于表示一串字符

两种风格

1.C风格 char 变量名[] = "字符串值"

![image-20220224213546763](C:/Users/ASUS/AppData/Roaming/Typora/typora-user-images/image-20220224213546763.png)

输出

![image-20220224213614563](C:/Users/ASUS/AppData/Roaming/Typora/typora-user-images/image-20220224213614563.png)

2.C++风格字符串 : string 变量名 = “字符串值”  （需添加头文件#include<string>）

![image-20220224214232301](C:/Users/ASUS/AppData/Roaming/Typora/typora-user-images/image-20220224214232301.png)

结构与char风格输出结果一样

#### 7.布尔类型

作用： 布尔数据类型代表真或假的值

bool类型只有两个值：true 、false

当赋值为true时，为1

反之则为0

#### 8.数据的输入

作用： 用于键盘获取数据

关键字： cin >> 变量

例如

```
  int a = 0 ;

  cout << "请输入数据" << endl ;

  cin >> a;

  cout << "输出数据为: " << a << endl;
```

输出a=100

### 1.运算符

#### 1.算术运算符

作用： 用于处理四则运算

![image-20220227205652572](C:/Users/ASUS/AppData/Roaming/Typora/typora-user-images/image-20220227205652572.png)

#### 2.赋值运算符

+=  ； - = ； /= ； * =； % = ；

#### 3.比较运算符

== ; ! = ;  >; < ; > = ; < =;

#### 4.逻辑运算符

作用： 根据表达式返回真或者假

![image-20220227212109250](C:/Users/ASUS/AppData/Roaming/Typora/typora-user-images/image-20220227212109250.png)

#### 5.程序流程结构

三种程序运行结构： 顺序结构、 选择结构 、循环结构

##### 1.顺序结构： 程序按顺序执行，不发生跳转

##### 2. 选择结构: 依据条件是否满足，有选择的执行相应功能

###### 2.1if 语句

单行 多行 多条件 嵌套

  /*案例需求： 

  提示用户输入一个高考分数，根据分数提示如下判断

  分数如果大于600分则视为考上一本，大于500则视为考上二本，大于400则视为考上三本，其余视为未考上本科；

  在一本分数中，如果大于700分，考入北大，大于650则考入清华，大于600则考入人大

```
  */

  int score = 0;

  cout << "请输入你的高考分数" << endl ;

  cin >> score ;

  cout << "你输入的高考分数为"<< score << endl ;

  if (score >= 600 && score <= 750)

  {

​    if (score >= 700)

​    {

​      cout << "恭喜你考上北大"  << endl; 

​    }

​    else if (score >= 650 && score <= 700)

​    {

​      cout << "恭喜你考上清华大学" << endl;   

​    }

​    else{

​      cout << "恭喜考上人大" << endl ;

​    }

  }

  else if (score >= 500 && score <= 600)

  {

​    cout << "恭喜你考上二本大学" << endl;

  }

  else if (score >= 400 && score <=500)

  {

​    cout << "恭喜你考上三本大学" << endl ;

  }

  else if (score >= 750 )

  {

​    cout << "你输入的分数有误" << endl ;

  }

  else{

​    cout << "很遗憾你没有考上大学" << endl ; 

  }

  system ("pause");

  return 0 ;



}
```

```
  // 三只小猪称重

  //有三只小猪ABC，请分别输入三只小猪的体重，并判断哪只小猪最重

  float Pig_One = 0 ;

  float Pig_Two = 0 ;

  float Pig_Three = 0;

  cout << "请输入第一只小猪的体重" << endl ;

  cin >> Pig_One;

  cout << "输入第一只小猪的体重为"<<Pig_One<< endl;

  cout << "请输入第二只小猪的体重" << endl ;

  cin >> Pig_Two;

  cout << "输入第二只小猪的体重为"<<Pig_Two<< endl;

  cout << "请输入第三只小猪的体重" << endl ;

  cin >> Pig_Three;

  cout << "输入第三只小猪的体重为"<<Pig_Three<< endl;

  if (Pig_One > Pig_Two)

  {

​    if (Pig_One > Pig_Three)

​    {

​      cout << "第一只小猪最重" << endl ;

​    }

​    else {

​      cout << "第三只小猪最重" << endl ;

​    }

  }

  else

  {

​    if (Pig_Two > Pig_Three )

​    {

​      cout << "第二只小猪最重" << endl ;

​    }

​    else

​    {

​      cout << "第三只小猪最重" << endl ;

​    }

  }

  system ("pause") ;

  

}
```



###### 2.2三目运算符

语句；表达式1 ？ 表达式2 ： 表达式3

 ![image-20220227230457721](C:/Users/ASUS/AppData/Roaming/Typora/typora-user-images/image-20220227230457721.png)

![image-20220227230528736](C:/Users/ASUS/AppData/Roaming/Typora/typora-user-images/image-20220227230528736.png)

2.3switch

```
  //使用switch给电影打分

  //9~10为经典

  //8~7非常好

  //6~5一般

  //5分以下 烂片

  int Movie_Score= 0 ;

  cout << "请给电影打0~10分" << endl ;

  cin >> Movie_Score;

  cout << "你给电影打的分为" << Movie_Score << endl ;

  switch(Movie_Score)

  {

​    case 10:

​    case 9 :

​    cout << "您认为该电影是经典电影" << endl ;

​    break;

​    case 8:

​    case 7:

​    cout << "您认为该电影非常好" << endl ;

​    break;

​    case 6: 

​    case 5:

​    cout << "您认为该电影一般" << endl ;

​    break;

​    case 4:

​    case 3:

​    case 2:

​    case 1:

​    case 0:

​    cout << "您认为该电影是烂片" << endl ;

​    break;

​    default:

​    cout <<"您的评分超出给定范围" << endl;

  }

  system ("pause");

  return 0 ;
```

![image-20220227233056599](C:/Users/ASUS/AppData/Roaming/Typora/typora-user-images/image-20220227233056599.png)

##### 3.循环结构： 依据条件是否满足，循环多次执行某段代码

###### 3.1while循环语句

作用：满足循环解雇，执行循环结构

语法：while（循环条件）{循环的语句}

###### 3.2do...while

作用：满足循环条件，执行循环结构

语法：do（循环语句）while（循环条件）

注意：与while的区别在于do...while会先执行一次循环再判断循环条件

 

```
 //案例：水仙花数是指一个三位数，他的每个位上的数字三次幂之和等于他本身

  //例如：1^3+5^3+3^3=153

  //请利用do while循环语句，求出所有三位数的水仙花数

  int num = 100;

  do{

​    

​    int a =0;//

​    int b =0;//

​    int c =0;//



​    a=num%10;

​    b=num/10%10;

​    c=num/100;



​    if(a*a*a + b*b*b + c*c*c == num)

​    {

​      cout << "该数为水仙花数" << num <<  endl;

​    }

​    num++;

  }while(num<1000);



  system("pause");

  return 0;
```

![image-20220228165343361](C:/Users/ASUS/AppData/Roaming/Typora/typora-user-images/image-20220228165343361.png)

###### 3.3for 循环语句

作用：满足循环条件，执行循环语句

语法：for（起始表达式；条件表达式；末尾循环体）{循环语句}；

  //练习案例 ：敲桌子

  //案例描述：从1开始数到数字100，如果数字个位有7，或者 数字十位有7，或者该数字是7的倍数

  //我们打印敲桌子，其余数字直接打印输出

```
  int num;

  for (num=1; num <=100; num++)

  {

​    /* code */

​    int a =0;

​    int b =0;

​    int c=0;



​    a = num%10;

​    b= num/10;

​    c= num%7; // 若c=0，则为7的倍数



​    if(a==7 || b == 7 || c == 0)

​    {

​      cout<< "该数字为："<< num << endl;

​      cout<< "敲桌子"<< endl;

​    }

​    else{

​      cout<< "该数字既不是的倍数，且十位个位不包含七:" <<  num  <<  endl ;

​    }



  }

  system("pause");

  return 0;
```



###### 3.4嵌套循环

  //嵌套循环，生成10*10的星阵

```
#if 1

  char str= '*';

  int y;

  int x;

  for (y=0;y<10;y++)

  {

​    for (x = 0; x < 10; x++)

​    {

​      cout << str ; 

​    }

​    cout << endl;

  }

#endif

  system("pause");

  return 0;
```

```
嵌套循环，生成九九乘法表

  int x = 0;

  int y = 0;

  for (x = 1; x <=9; x++)

  {

​    for (y = 1; y<= x; y++)

​    {

​      cout << x << "X" <<y << "="<< x*y << " " ;

​      

​    }

​    cout << endl;

  }
```



##### 4.跳转语句

###### 4.1break语句

作用：用于跳出循环结构或者选择结构

使用时机：

1.出现在switch条件语句中，终止case跳出switch

2.出现在循环语句中，作用：跳出当前循环

3.出现在嵌套循环中，跳出最近的内层循环语句

###### 4.2continue语句

作用：在循环语句中，跳过本次循环中余下尚未执行的语句，继续执行下一次循环

###### 4.3goto语句

作用：可以无条件跳转语句

学着学着就突然发现

[菜鸟教程]:[C++ 数据类型 | 菜鸟教程 (runoob.com)](https://www.runoob.com/cplusplus/cpp-data-types.html)

上面都有

