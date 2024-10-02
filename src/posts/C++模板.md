---
title: C++模板
tags: C++
data: 2023-7-31 16:40
cover: https://cdn.jsdelivr.net/gh/czlifetime/img/C++.jpg
tag:
  - C++
---

# 模板

## 模板的概念

模板就是建立<strong>通用的模具</strong>，大大<b>提高复用性</b>



模板的特点：

* 模板不可以直接使用，它只是一个框架
* 模板的通用并不是万能的



## 函数模板

* C++另一种编程思想称为 <mark>泛型编程</mark> ，主要利用的技术就是模板


* C++提供两种模板机制:<strong>函数模板</strong>和<strong>类模板</strong>

### 函数模板语法

函数模板作用：

建立一个通用函数，其函数返回值类型和形参类型可以不具体制定，用一个<strong>虚拟的类型</strong>来代表。

<strong>语法：</strong> 

```C++
template<typename T>
函数声明或定义
```

<strong>解释：</strong>

template  ---  声明创建模板

typename  --- 表面其后面的符号是一种数据类型，可以用class代替

T    ---   通用的数据类型，名称可以替换，通常为大写字母

<strong>示例：</strong>

```C++
//交换整型函数
void swapInt(int& a, int& b) {
	int temp = a;
	a = b;
	b = temp;
}

//交换浮点型函数
void swapDouble(double& a, double& b) {
	double temp = a;
	a = b;
	b = temp;
}

//利用模板提供通用的交换函数
template<typename T>
void mySwap(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;
}

void test01()
{
	int a = 10;
	int b = 20;
	
	//swapInt(a, b);

	//利用模板实现交换
	//1、自动类型推导
	mySwap(a, b);

	//2、显示指定类型
	mySwap<int>(a, b);

	cout << "a = " << a << endl;
	cout << "b = " << b << endl;

}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：

* 函数模板利用关键字 template
* 使用函数模板有两种方式：<mark>自动类型推导</mark>、<mark>显示指定类型</mark>
* 模板的目的是为了提高复用性，将类型参数化



### 函数模板注意事项

注意事项：

* 自动类型推导，必须推导出一致的数据类型T,才可以使用


* 模板必须要确定出T的数据类型，才可以使用



<strong>示例：</strong>

```C++
//利用模板提供通用的交换函数
template<class T>
void mySwap(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;
}


// 1、自动类型推导，必须推导出一致的数据类型T,才可以使用
void test01()
{
	int a = 10;
	int b = 20;
	char c = 'c';

	mySwap(a, b); // 正确，可以推导出一致的T
	//mySwap(a, c); // 错误，推导不出一致的T类型
}


// 2、模板必须要确定出T的数据类型，才可以使用
template<class T>
void func()
{
	cout << "func 调用" << endl;
}

void test02()
{
	//func(); //错误，模板不能独立使用，必须确定出T的类型
	func<int>(); //利用显示指定类型的方式，给T一个类型，才可以使用该模板
}

int main() {

	test01();
	test02();

	system("pause");

	return 0;
}
```

总结：

* 使用模板时必须确定出通用数据类型T，并且能够推导出一致的类型

### 函数模板案例

案例描述：

* 利用函数模板封装一个排序的函数，可以对<strong>不同数据类型数组</strong>进行排序
* 排序规则从大到小，排序算法为<strong>选择排序</strong>
* 分别利用<strong>char数组</strong>和<strong>int数组</strong>进行测试



示例：

```C++
//交换的函数模板
template<typename T>
void mySwap(T &a, T&b)
{
	T temp = a;
	a = b;
	b = temp;
}


template<class T> // 也可以替换成typename
//利用选择排序，进行对数组从大到小的排序
void mySort(T arr[], int len)
{
	for (int i = 0; i < len; i++)
	{
		int max = i; //最大数的下标
		for (int j = i + 1; j < len; j++)
		{
			if (arr[max] < arr[j])
			{
				max = j;
			}
		}
		if (max != i) //如果最大数的下标不是i，交换两者
		{
			mySwap(arr[max], arr[i]);
		}
	}
}
template<typename T>
void printArray(T arr[], int len) {

	for (int i = 0; i < len; i++) {
		cout << arr[i] << " ";
	}
	cout << endl;
}
void test01()
{
	//测试char数组
	char charArr[] = "bdcfeagh";
	int num = sizeof(charArr) / sizeof(char);
	mySort(charArr, num);
	printArray(charArr, num);
}

void test02()
{
	//测试int数组
	int intArr[] = { 7, 5, 8, 1, 3, 9, 2, 4, 6 };
	int num = sizeof(intArr) / sizeof(int);
	mySort(intArr, num);
	printArray(intArr, num);
}

int main() {

	test01();
	test02();

	system("pause");

	return 0;
}
```

总结：模板可以提高代码复用，需要熟练掌握





### 普通函数与函数模板的区别



<strong>普通函数与函数模板区别：</strong>

* <mark>普通函数调用时可以发生自动类型转换（隐式类型转换）</mark>
* 函数模板调用时，如果利用自动类型推导，不会发生隐式类型转换
* 如果利用显示指定类型的方式，可以发生隐式类型转换



<strong>示例：</strong>

```C++
//普通函数
int myAdd01(int a, int b)
{
	return a + b;
}

//函数模板
template<class T>
T myAdd02(T a, T b)  
{
	return a + b;
}

//使用函数模板时，如果用自动类型推导，不会发生自动类型转换,即隐式类型转换
void test01()
{
	int a = 10;
	int b = 20;
	char c = 'c';
	
	cout << myAdd01(a, c) << endl; //正确，将char类型的'c'隐式转换为int类型  'c' 对应 ASCII码 99

	//myAdd02(a, c); // 报错，使用自动类型推导时，不会发生隐式类型转换

	myAdd02<int>(a, c); //正确，如果用显示指定类型，可以发生隐式类型转换
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：建议使用显示指定类型的方式，调用函数模板，因为可以自己确定通用类型T





### 普通函数与函数模板的调用规则



调用规则如下：

1. <mark>如果函数模板和普通函数都可以实现，优先调用普通函数</mark>
2. 可以通过空模板参数列表来强制调用函数模板
3. 函数模板也可以发生重载
4. <mark>如果函数模板可以产生更好的匹配,优先调用函数模板</mark>





<strong>示例：</strong>

```C++
//普通函数与函数模板调用规则
void myPrint(int a, int b)
{
	cout << "调用的普通函数" << endl;
}

template<typename T>
void myPrint(T a, T b) 
{ 
	cout << "调用的模板" << endl;
}

template<typename T>
void myPrint(T a, T b, T c) 
{ 
	cout << "调用重载的模板" << endl; 
}

void test01()
{
	//1、如果函数模板和普通函数都可以实现，优先调用普通函数
	// 注意 如果告诉编译器  普通函数是有的，但只是声明没有实现，或者不在当前文件内实现，就会报错找不到
	int a = 10;
	int b = 20;
	myPrint(a, b); //调用普通函数

	//2、可以通过空模板参数列表来强制调用函数模板
	myPrint<>(a, b); //调用函数模板

	//3、函数模板也可以发生重载
	int c = 30;
	myPrint(a, b, c); //调用重载的函数模板

	//4、 如果函数模板可以产生更好的匹配,优先调用函数模板
	char c1 = 'a';
	char c2 = 'b';
	myPrint(c1, c2); //调用函数模板
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：<strong>既然提供了函数模板，最好就不要提供普通函数，否则容易出现二义性</strong>



### 模板的局限性

<strong>局限性：</strong>

* 模板的通用性并不是万能的



<strong>例如：</strong>

```C++
	template<class T>
	void f(T a, T b)
	{ 
    	a = b;
    }
```

在上述代码中提供的赋值操作，如果传入的a和b是一个数组，就无法实现了



再例如：

```C++
	template<class T>
	void f(T a, T b)
	{ 
    	if(a > b) { ... }
    }
```

在上述代码中，如果T的数据类型传入的是像Person这样的自定义数据类型，也无法正常运行



因此C++为了解决这种问题，提供模板的重载，可以为这些<strong>特定的类型</strong>提供<strong>具体化的模板</strong>



<strong>示例：</strong>

```C++
#include<iostream>
using namespace std;

#include <string>

class Person
{
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}
	string m_Name;
	int m_Age;
};

//普通函数模板
template<class T>
bool myCompare(T& a, T& b)
{
	if (a == b)
	{
		return true;
	}
	else
	{
		return false;
	}
}


//具体化，显示具体化的原型和定意思以template<>开头，并通过名称来指出类型
//具体化优先于常规模板
template<> bool myCompare(Person &p1, Person &p2)
{
	if ( p1.m_Name  == p2.m_Name && p1.m_Age == p2.m_Age)
	{
		return true;
	}
	else
	{
		return false;
	}
}

void test01()
{
	int a = 10;
	int b = 20;
	//内置数据类型可以直接使用通用的函数模板
	bool ret = myCompare(a, b);
	if (ret)
	{
		cout << "a == b " << endl;
	}
	else
	{
		cout << "a != b " << endl;
	}
}

void test02()
{
	Person p1("Tom", 10);
	Person p2("Tom", 10);
	//自定义数据类型，不会调用普通的函数模板
	//可以创建具体化的Person数据类型的模板，用于特殊处理这个类型
	bool ret = myCompare(p1, p2);
	if (ret)
	{
		cout << "p1 == p2 " << endl;
	}
	else
	{
		cout << "p1 != p2 " << endl;
	}
}

int main() {

	test01();

	test02();

	system("pause");

	return 0;
}
```

总结：

* 利用具体化的模板，可以解决自定义类型的通用化
* 学习模板并不是为了写模板，而是在STL能够运用系统提供的模板





## 类模板

### 类模板语法

类模板作用：

* 建立一个通用类，类中的成员 数据类型可以不具体制定，用一个<strong>虚拟的类型</strong>来代表。



<strong>语法：</strong> 

```c++
template<typename T>
类
```

<strong>解释：</strong>

template  ---  声明创建模板

typename  --- 表面其后面的符号是一种数据类型，可以用class代替

T    ---   通用的数据类型，名称可以替换，通常为大写字母



<strong>示例：</strong>

```C++
#include <string>
//类模板
template<class NameType, class AgeType> 
class Person
{
public:
	Person(NameType name, AgeType age)
	{
		this->mName = name;
		this->mAge = age;
	}
	void showPerson()
	{
		cout << "name: " << this->mName << " age: " << this->mAge << endl;
	}
public:
	NameType mName;
	AgeType mAge;
};

void test01()
{
	// 指定NameType 为string类型，AgeType 为 int类型
	Person<string, int>P1("孙悟空", 999);
	P1.showPerson();
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：类模板和函数模板语法相似，在声明模板template后面加类，此类称为类模板



### 类模板与函数模板区别



类模板与函数模板区别主要有两点：

1. 类模板没有自动类型推导的使用方式
2. 类模板在模板参数列表中可以有默认参数



<strong>示例：</strong>

```C++
#include <string>
//类模板
template<class NameType, class AgeType = int> 
class Person
{
public:
	Person(NameType name, AgeType age)
	{
		this->mName = name;
		this->mAge = age;
	}
	void showPerson()
	{
		cout << "name: " << this->mName << " age: " << this->mAge << endl;
	}
public:
	NameType mName;
	AgeType mAge;
};

//1、类模板没有自动类型推导的使用方式
void test01()
{
	// Person p("孙悟空", 1000); // 错误 类模板使用时候，不可以用自动类型推导
	Person <string ,int>p("孙悟空", 1000); //必须使用显示指定类型的方式，使用类模板
	p.showPerson();
}

//2、类模板在模板参数列表中可以有默认参数
void test02()
{
	Person <string> p("猪八戒", 999); //类模板中的模板参数列表 可以指定默认参数
	p.showPerson();
}

int main() {

	test01();

	test02();

	system("pause");

	return 0;
}
```

总结：

* 类模板使用只能用显示指定类型方式
* 类模板中的模板参数列表可以有默认参数



###  类模板中成员函数创建时机



类模板中成员函数和普通类中成员函数创建时机是有区别的：

* 普通类中的成员函数一开始就可以创建
* 类模板中的成员函数在调用时才创建





<strong>示例：</strong>

```C++
class Person1
{
public:
	void showPerson1()
	{
		cout << "Person1 show" << endl;
	}
};

class Person2
{
public:
	void showPerson2()
	{
		cout << "Person2 show" << endl;
	}
};

template<class T>
class MyClass
{
public:
	T obj;

	//类模板中的成员函数，并不是一开始就创建的，而是在模板调用时再生成

	void fun1() { obj.showPerson1(); }
	void fun2() { obj.showPerson2(); }

};

void test01()
{
	MyClass<Person1> m;
	
	m.fun1();

	//m.fun2();//编译会出错，说明函数调用才会去创建成员函数
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：类模板中的成员函数并不是一开始就创建的，在调用时才去创建





### 类模板与继承



当类模板碰到继承时，需要注意一下几点：

* 当子类继承的父类是一个类模板时，子类在声明的时候，要指定出父类中T的类型
* 如果不指定，编译器无法给子类分配内存
* 如果想灵活指定出父类中T的类型，子类也需变为类模板



<strong>示例：</strong>

```C++
template<class T>
class Base
{
	T m;
};

//class Son:public Base  //错误，c++编译需要给子类分配内存，必须知道父类中T的类型才可以向下继承
class Son :public Base<int> //必须指定一个类型
{
};
void test01()
{
	Son c;
}

//类模板继承类模板 ,可以用T2指定父类中的T类型
template<class T1, class T2>
class Son2 :public Base<T2>
{
public:
	Son2()
	{
		cout << typeid(T1).name() << endl;
		cout << typeid(T2).name() << endl;
	}
};

void test02()
{
	Son2<int, char> child1;
}


int main() {

	test01();

	test02();

	system("pause");

	return 0;
}
```

总结：如果父类是类模板，子类需要指定出父类中T的数据类型





### 类模板成员函数类外实现



学习目标：能够掌握类模板中的成员函数类外实现



<strong>示例：</strong>

```C++
#include <string>

//类模板中成员函数类外实现
template<class T1, class T2>
class Person {
public:
	//成员函数类内声明
	Person(T1 name, T2 age);
	void showPerson();

public:
	T1 m_Name;
	T2 m_Age;
};

//构造函数 类外实现
template<class T1, class T2>
Person<T1, T2>::Person(T1 name, T2 age) {
	this->m_Name = name;
	this->m_Age = age;
}

//成员函数 类外实现
template<class T1, class T2>
void Person<T1, T2>::showPerson() {
	cout << "姓名: " << this->m_Name << " 年龄:" << this->m_Age << endl;
}

void test01()
{
	Person<string, int> p("Tom", 20);
	p.showPerson();
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：类模板中成员函数类外实现时，需要加上模板参数列表





### 类模板分文件编写

学习目标：

* 掌握类模板成员函数分文件编写产生的问题以及解决方式



问题：

* 类模板中成员函数创建时机是在调用阶段，导致分文件编写时链接不到


解决：

* 解决方式1：直接包含.cpp源文件
* 解决方式2：将声明和实现写到同一个文件中，并更改后缀名为.hpp，hpp是约定的名称，并不是强制



<strong>示例：</strong>

person.hpp中代码：

```C++
#pragma once
#include <iostream>
using namespace std;
#include <string>

template<class T1, class T2>
class Person {
public:
	Person(T1 name, T2 age);
	void showPerson();
public:
	T1 m_Name;
	T2 m_Age;
};

//构造函数 类外实现
template<class T1, class T2>
Person<T1, T2>::Person(T1 name, T2 age) {
	this->m_Name = name;
	this->m_Age = age;
}

//成员函数 类外实现
template<class T1, class T2>
void Person<T1, T2>::showPerson() {
	cout << "姓名: " << this->m_Name << " 年龄:" << this->m_Age << endl;
}
```



类模板分文件编写.cpp中代码

```C++
#include<iostream>
using namespace std;

//#include "person.h"
#include "person.cpp" //解决方式1，包含cpp源文件

//解决方式2，将声明和实现写到一起，文件后缀名改为.hpp
#include "person.hpp"
void test01()
{
	Person<string, int> p("Tom", 10);
	p.showPerson();
}

int main() {

	test01();

	system("pause");

	return 0;
}
```

总结：主流的解决方式是第二种，将类模板成员函数写到一起，并将后缀名改为.hpp





### 类模板与友元



学习目标：

* 掌握类模板配合友元函数的类内和类外实现



全局函数类内实现 - 直接在类内声明友元即可

全局函数类外实现 - 需要提前让编译器知道全局函数的存在



<strong>示例：</strong>

```C++
#include <string>

//2、全局函数配合友元  类外实现 - 先做函数模板声明，下方在做函数模板定义，在做友元
template<class T1, class T2> class Person;

//如果声明了函数模板，可以将实现写到后面，否则需要将实现体写到类的前面让编译器提前看到
//template<class T1, class T2> void printPerson2(Person<T1, T2> & p); 

template<class T1, class T2>
void printPerson2(Person<T1, T2> & p)
{
	cout << "类外实现 ---- 姓名： " << p.m_Name << " 年龄：" << p.m_Age << endl;
}

template<class T1, class T2>
class Person
{
	//1、全局函数配合友元   类内实现
	friend void printPerson(Person<T1, T2> & p)
	{
		cout << "姓名： " << p.m_Name << " 年龄：" << p.m_Age << endl;
	}


	//全局函数配合友元  类外实现
	friend void printPerson2<>(Person<T1, T2> & p);

public:

	Person(T1 name, T2 age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}


private:
	T1 m_Name;
	T2 m_Age;

};

//1、全局函数在类内实现
void test01()
{
	Person <string, int >p("Tom", 20);
	printPerson(p);
}


//2、全局函数在类外实现
void test02()
{
	Person <string, int >p("Jerry", 30);
	printPerson2(p);
}

int main() {

	//test01();

	test02();

	system("pause");

	return 0;
}
```

总结：建议全局函数做类内实现，用法简单，而且编译器可以直接识别



> 案例：<strong>未完待续</strong>







# 初识STL

## STL的诞生



* 长久以来，软件界一直希望建立一种可重复利用的东西

* C++的<strong>面向对象</strong>和<strong>泛型编程</strong>思想，目的就是<strong>复用性的提升</strong>

* 大多情况下，数据结构和算法都未能有一套标准,导致被迫从事大量重复工作

* 为了建立数据结构和算法的一套标准,诞生了<strong>STL</strong>

  

## STL基本概念



* STL(Standard Template Library,<strong>标准模板库</strong>)
* STL 从广义上分为: <strong>容器(container) 算法(algorithm) 迭代器(iterator)</strong>
* <strong>容器</strong>和<strong>算法</strong>之间通过<strong>迭代器</strong>进行无缝连接。
* STL 几乎所有的代码都采用了模板类或者模板函数



## STL六大组件

STL大体分为六大组件，分别是:<strong>容器、算法、迭代器、仿函数、适配器（配接器）、空间配置器</strong>



1. 容器：各种数据结构，如`vector`、`list`、`deque`、`set`、`map`等,用来存放数据。
2. 算法：各种常用的算法，如sort、find、copy、for_each等
3. 迭代器：扮演了容器与算法之间的胶合剂。
4. 仿函数：行为类似函数，可作为算法的某种策略。
5. 适配器：一种用来修饰容器或者仿函数或迭代器接口的东西。
6. 空间配置器：负责空间的配置与管理。





## STL中容器、算法、迭代器



<strong>容器：</strong>置物之所也

STL<strong>容器</strong>就是将运用<strong>最广泛的一些数据结构</strong>实现出来

常用的数据结构：数组, 链表,树, 栈, 队列, 集合, 映射表 等

这些容器分为<strong>序列式容器</strong>和<strong>关联式容器</strong>两种:

​	<strong>序列式容器</strong>:强调值的排序，序列式容器中的每个元素均有固定的位置。
​	<strong>关联式容器</strong>:二叉树结构，各元素之间没有严格的物理上的顺序关系



<strong>算法：</strong>问题之解法也

有限的步骤，解决逻辑或数学上的问题，这一门学科我们叫做算法(Algorithms)

算法分为:<strong>质变算法</strong>和<strong>非质变算法</strong>。

质变算法：是指运算过程中会更改区间内的元素的内容。例如拷贝，替换，删除等等

非质变算法：是指运算过程中不会更改区间内的元素内容，例如查找、计数、遍历、寻找极值等等



<strong>迭代器：</strong>容器和算法之间粘合剂

提供一种方法，使之能够依序寻访某个容器所含的各个元素，而又无需暴露该容器的内部表示方式。

每个容器都有自己专属的迭代器

迭代器使用非常类似于指针，初学阶段我们可以先理解迭代器为指针



迭代器种类：

| 种类           | 功能                                                     | 支持运算                                |
| -------------- | -------------------------------------------------------- | --------------------------------------- |
| 输入迭代器     | 对数据的只读访问                                         | 只读，支持++、==、！=                   |
| 输出迭代器     | 对数据的只写访问                                         | 只写，支持++                            |
| 前向迭代器     | 读写操作，并能向前推进迭代器                             | 读写，支持++、==、！=                   |
| 双向迭代器     | 读写操作，并能向前和向后操作                             | 读写，支持++、--，                      |
| 随机访问迭代器 | 读写操作，可以以跳跃的方式访问任意数据，功能最强的迭代器 | 读写，支持++、--、[n]、-n、<、<=、>、>= |

常用的容器中迭代器种类为双向迭代器，和随机访问迭代器





## 容器算法迭代器初识

向容器中插入数据、并遍历这个容器



### vector存放内置数据类型



容器：`vector`

> `vector`容器本身可以理解为指针

算法：`for_each`

迭代器：`vector<int>::iterator`



示例：

```java
#include <iostream>
#include <algorithm>
using namespace std;
void myPrit(int value){
    cout << value << endl;
}

int main() {
    vector<int> v;
    v.push_back(10);
    v.push_back(20);
    v.push_back(30);
    v.push_back(40);

    //第一种遍历方式
    //通过迭代器访问容器中的数据
    vector<int>::iterator itBegin = v.begin();//指向容器中的第一个元素
    vector<int>::iterator itEnd = v.end();//指向容器中最后一个元素的最后一个位置
    while(itBegin != itEnd){
        cout << *itBegin << endl;
        itBegin++;
    }

    //第二种遍历
    for(vector<int>::iterator it = v.begin();it != v.end();it++){
        cout << *it << endl;
    }

    //第三种遍历
    for_each(v.begin(),v.end(), myPrit);
    return 0;
}
```

vector存放自定义数据类型

```c++
//
// Created by Lifetime on 2023/11/17 017.
//
//vector存放自定义数据类型

#include<iostream>
#include<vector>
#include<string>
using namespace std;

class Person{
private:
    string name;
    int age;
public:
    Person(const string &name, int age) : name(name), age(age) {}

    const string &getName() const {
        return name;
    }

    void setName(const string &name) {
        Person::name = name;
    }

    int getAge() const {
        return age;
    }

    void setAge(int age) {
        Person::age = age;
    }

    virtual ~Person() {

    }
};
void test01(){
    vector<Person>p;
    Person p1("Tom",12);
    Person p2("Jack",18);
    Person p3("Rose",18);
    Person p4("Jerry",18);
    Person p5("Georgy",13);
    Person p6("Max",12);

    p.push_back(p1);
    p.push_back(p2);
    p.push_back(p3);
    p.push_back(p4);
    p.push_back(p5);
    p.push_back(p6);

    for (vector<Person>::iterator it = p.begin();it != p.end();it++) {
        cout <<it->getName()<<endl;
    }
}
int main(){

    test01();

    return 0;
}
```



### Vector容器嵌套容器

```C++
//
// Created by Lifetime on 2023/11/17 017.
//
#include<iostream>
#include<vector>

using namespace std;
void test01(){
    vector<vector<int>>vec;
    //创建小容器
    vector<int>vector1;
    vector<int>vector2;
    vector<int>vector3;
    vector<int>vector4;
    vector<int>vector5;

    //向小容器中添加数据
    for (int i = 0; i < 5; ++i) {
        vector1.push_back(i+1);
        vector2.push_back(i+2);
        vector3.push_back(i+3);
        vector4.push_back(i+4);
        vector5.push_back(i+5);
    }

    //将小容器添加到大容器
    vec.push_back(vector1);
    vec.push_back(vector2);
    vec.push_back(vector3);
    vec.push_back(vector4);
    vec.push_back(vector5);

    //遍历大容器
    for(vector<vector<int>>::iterator it = vec.begin();vec.begin() != vec.end();it++){
        for (vector<int>::iterator iter = (*it).begin();iter != (*it).end();iter++) {
            cout<< "iter=" << *iter ;
        }
        cout<<endl;
    }

}
int main(){
    test01();
    return 0;
}
```

# STL-常用容器

## string容器

### 1. string基本概念

<strong>本质</strong>

+ string是C++风格的字符串，是个类

<strong>string和char*的区别</strong>

+ char*是一个指针
+ string是一个类，类内部封装了char\*，管理这个字符串，是一个char\*型的容器

<strong>特点：</strong>

string类内部封装了很多成员方法

> 查找find，拷贝copy，删除delete，替换replace，插入insert

string管理char*所分配的内存，不用担心赋值越界等，由类内部进行负责

### 2. string构造函数

构造函数原型：

+ `string();` //创建一个空的字符串
+ `string(const char* s)` //使用字符串初始化
+ `string(const string& str);`//使用一个string对象初始化另一个string对象
+ `string(int n,char c);` //使用n个字符c初始化

```c++
#include<iostream>
#include<string>
using namespace std;

void test01() {
	string s1;
	const char* str = "hello world";
	const string& str1 = "test_str1";

	string s2(str);
	cout << "s2=" << s2 << endl;
	string s3(str1);
	cout << "s3" << s3 << endl;
	char c = '1';
	int n = 3;
	cout<<string(n, c);

}
int main() {
	test01();
	return 0;
}
```

![](https://cdn.jsdelivr.net/gh/czlifetime/img/string%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0.png)

### 3. string赋值操作

<strong>功能描述：</strong>

* 实现在字符串末尾拼接字符串



<strong>函数原型：</strong>

* `string& operator+=(const char* str);`                   //重载+=操作符
* `string& operator+=(const char c);`                         //重载+=操作符
* `string& operator+=(const string& str);`                //重载+=操作符
* `string& append(const char *s); `                               //把字符串s连接到当前字符串结尾
* `string& append(const char *s, int n);`                 //把字符串s的前n个字符连接到当前字符串结尾
* `string& append(const string &s);`                           //同operator+=(const string& str)
* `string& append(const string &s, int pos, int n);`//字符串s中从pos开始的n个字符连接到字符串结尾



```c++
#include<iostream>
#include<string>
using namespace std;

void test01() {
	string str1;
	str1 = "hello string";
	cout << "str1=" << str1 << endl;

	string str2;
	str2.assign("hello string");
	cout << "str2=" << str2 << endl;
}
int main() {
	test01();
	return 0;
}
```



### 4. string字符串拼接

<strong>功能描述：</strong>

* 查找：查找指定字符串是否存在
* 替换：在指定的位置替换字符串



<strong>函数原型：</strong>

* `int find(const string& str, int pos = 0) const;`              //查找str第一次出现位置,从pos开始查找
* `int find(const char* s, int pos = 0) const; `                     //查找s第一次出现位置,从pos开始查找
* `int find(const char* s, int pos, int n) const; `               //从pos位置查找s的前n个字符第一次位置
* `int find(const char c, int pos = 0) const; `                       //查找字符c第一次出现位置
* `int rfind(const string& str, int pos = npos) const;`      //查找str最后一次位置,从pos开始查找
* `int rfind(const char* s, int pos = npos) const;`              //查找s最后一次出现位置,从pos开始查找
* `int rfind(const char* s, int pos, int n) const;`              //从pos查找s的前n个字符最后一次位置
* `int rfind(const char c, int pos = 0) const;  `                      //查找字符c最后一次出现位置
* `string& replace(int pos, int n, const string& str); `       //替换从pos开始n个字符为字符串str
* `string& replace(int pos, int n,const char* s); `                 //替换从pos开始的n个字符为字符串s

```C++
#include<iostream>
#include<string>
using namespace std;
void test01() {
	string str1 = "我";
	str1 += "想进步，赚大钱";
	cout << "str1=" << str1<<endl;
	str1 += 'wa';
	cout << "str1= " << str1 << endl;

	string str2;
	str2.append("天行健，君子以自强不息");
	cout << "str2=" << str2 << endl;
	str2.append("地势坤，君子以厚德载物",22);
	cout << "str2=" << str2 << endl;
	
}
int main() {
	test01();
	return 0;
}
```



### 5. string查找和替换

<strong>功能描述：</strong>

* 查找：查找指定字符串是否存在
* 替换：在指定的位置替换字符串



<strong>函数原型：</strong>

* `int find(const string& str, int pos = 0) const;`              //查找str第一次出现位置,从pos开始查找
* `int find(const char* s, int pos = 0) const; `                     //查找s第一次出现位置,从pos开始查找
* `int find(const char* s, int pos, int n) const; `               //从pos位置查找s的前n个字符第一次位置
* `int find(const char c, int pos = 0) const; `                       //查找字符c第一次出现位置
* `int rfind(const string& str, int pos = npos) const;`      //查找str最后一次位置,从pos开始查找
* `int rfind(const char* s, int pos = npos) const;`              //查找s最后一次出现位置,从pos开始查找
* `int rfind(const char* s, int pos, int n) const;`              //从pos查找s的前n个字符最后一次位置
* `int rfind(const char c, int pos = 0) const;  `                      //查找字符c最后一次出现位置
* `string& replace(int pos, int n, const string& str); `       //替换从pos开始n个字符为字符串str
* `string& replace(int pos, int n,const char* s); `                 //替换从pos开始的n个字符为字符串s

```C++
#include<iostream>
#include<string>
using namespace std;

//查找
void test01() {
	//find->从左往右找
	string str1 = "abcdefg";
	int pos =  str1.find("c");
	if (pos != -1) {
		cout << "字符串已找到" << endl;
		cout << "pos=" << pos << endl;
	}
	else {
		cout << "未找到字符串" << endl;
	}
	//rfind->从右往左找
}

//替换
void test02() {
	string str1 = "abcdefg";
	//从1号位置起3个字符 替换为"1111"
	str1.replace(1,3,"1111");
	//str1 = "a1111efg"
	cout << str1 << endl;
}

int main() {
	test01();
	test02();
	return 0;
}
```

+ `rfind()`从右往左，`find()`从左往右
+ `find()`返回查找到字符串第一个元素的位置，找不到元素，返回-1
+ `replace()`从第几个到第几个替换“”中的字符串

### 6. string字符串比较

<strong>功能描述：</strong>

* 字符串之间的比较

<strong>比较方式：</strong>

* 字符串比较是按字符的ASCII码进行对比

= 返回   0

\> 返回   1 

< 返回  -1



<strong>函数原型：</strong>

* `int compare(const string &s) const; `  //与字符串s比较
* `int compare(const char *s) const;`      //与字符串s比较

```C++
#include<iostream>
#include<string>
using namespace std;

void test01() {
	string str1 = "hello";
	string str2 = "hello";
	if (str1.compare(str2)==0) {
		cout << "字符串相等" << endl;
	}
}
void test02() {

	string str1 = "hello";
	string str2 = "aello";
	int res = str1.compare(str2);
	if (res > 0) {
		cout << "str1>str2" << endl;
	}
}
void test03() {
	string str1 = "aello";
	string str2 = "hello";
	int res = str1.compare(str2);
	if (res < 0) {
		cout << "<" << endl;
	}
}
int main() {
	test01();
	test02();
	test03();
	return 0;
}
```

总结：字符串对比主要是用于比较两个字符串是否相等，判断谁大谁小的意义并不是很大

### 7. string字符读取



string中单个字符存取方式有两种



* `char& operator[](int n); `     //通过[]方式取字符
* `char& at(int n);   `                    //通过at方法获取字符



```C++
#include<iostream>
#include<string>
using namespace std;
//通过数组访问单个字符
void test01() {
	string str = "Read String!";
	for (int i = 0; i < str.size(); i++) {
		cout << "str[" << i << "]=" << str[i] << endl;
	}
}
//使用at方式访问单个字符
void test02() {
	string str = "test_string";
	for (int i = 0; i < str.size(); i++) {
		cout << str.at(i) << endl;
	}
}
//通过[]或at修改单个字符
void test03() {
	string str = "alter";
	str[1] = '2';
	cout << str << endl;
	str.at(0) = 'b';
	cout << str << endl;
}
int main() {
	test01();
	test02();
	test03();
	return 0;
}
```





### 8. string插入和删除

<strong>功能描述：</strong>

* 对string字符串进行插入和删除字符操作

<strong>函数原型：</strong>

* `string& insert(int pos, const char* s);  `                //插入字符串
* `string& insert(int pos, const string& str); `        //插入字符串
* `string& insert(int pos, int n, char c);`                //在指定位置插入n个字符c
* `string& erase(int pos, int n = npos);`                    //删除从Pos开始的n个字符 

```C++
//字符串插入和删除
void test01()
{
	string str = "hello";
	str.insert(1, "111");
	cout << str << endl;

	str.erase(1, 3);  //从1号位置开始3个字符
	cout << str << endl;
}
int main() {
	test01();
	return 0;
}
```



### 9. string子串

<strong>功能描述：</strong>

* 从字符串中获取想要的子串



<strong>函数原型：</strong>

* `string substr(int pos = 0, int n = npos) const;`   //返回由pos开始的n个字符组成的字符串



```C++
//子串
void test01()
{

	string str = "abcdefg";
	string subStr = str.substr(1, 3);
	cout << "subStr = " << subStr << endl;

	string email = "hello@sina.com";
	int pos = email.find("@");
	string username = email.substr(0, pos);
	cout << "username: " << username << endl;

}

int main() {

	test01();

	return 0;
}
```



## vector容器

### 1. vector基本概念

<strong>功能：</strong>

* vector数据结构和<strong>数组非常相似</strong>，也称为<strong>单端数组</strong>



<strong>vector与普通数组区别：</strong>

* 不同之处在于数组是静态空间，而vector可以<strong>动态扩展</strong>



<strong>动态扩展：</strong>

* 并不是在原空间之后续接新空间，而是找更大的内存空间，然后将原数据拷贝新空间，释放原空间

  ![](https://cdn.jsdelivr.net/gh/czlifetime/img/vector%E5%AE%B9%E5%99%A8%E4%BB%8B%E7%BB%8D.jpg)

* vector容器的迭代器是支持随机访问的迭代器

### 2. vector构造函数

<strong>功能描述：</strong>

* 创建vector容器



<strong>函数原型：</strong>

* `vector<T> v; `               		     //采用模板实现类实现，默认构造函数
* `vector(v.begin(), v.end());   `       //将v[begin(), end())区间中的元素拷贝给本身。
* `vector(n, elem);`                            //构造函数将n个elem拷贝给本身。
* `vector(const vector &vec);`         //拷贝构造函数。

### 3. vector赋值操作



### 4. vector容量和大小



### 5. vector插入和删除



## 6. vector数据存取



## 7. vector互换容器



## 8. vector预留空间
