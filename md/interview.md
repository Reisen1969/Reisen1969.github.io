+++
author = "rayrain"
title = "面试"
date = "2022-05-03"
description = "interview"
toc= true
math= true
tags = [
    "interview"
]

+++

## C/C++相关

### static 关键字

1. 修饰局部变量,
2. 修饰全局变量,
3. 修饰成员变量,
4. 修饰普通函数,
5. 修饰成员函数,
6. 修饰类,this指针等

### const 关键字

1. 修饰变量，说明该变量不可以被改变；
2. 修饰指针，分为指向常量的指针（pointer to const）和自身是常量的指针（常量指针，const pointer）；
3. 修饰引用，指向常量的引用（reference to const），用于形参类型，即避免了拷贝，又避免了函数对值的修改；
4. 修饰成员函数，说明该成员函数内不能修改成员变量。
5. 宏和常量的区别

| 宏定义 #define         | const 常量     |
| ---------------------- | -------------- |
| 宏定义，相当于字符替换 | 常量声明       |
| 预处理器处理           | 编译器处理     |
| 无类型安全检查         | 有类型安全检查 |
| 不分配内存             | 要分配内存     |
| 存储在代码段           | 存储在数据段   |
| 可通过 `#undef` 取消   | 不可取消       |

### 内存

![img](https://media.geeksforgeeks.org/wp-content/uploads/memoryLayoutC.jpg)

1. 栈stack,  只要出现花括号,就会开辟新栈
2. 堆heap
3. 未初始化全局变量bss,
4. 初始化全局变量,存放全局数据和静态数据,又可细分为可读和可写区
5. 代码段text,只读

内存泄漏 堆栈溢出

### 指针和引用

- 引用和指针的区别,

引用只是别名,不需要分配内存空间,指针是变量,需要分配内存空间

- 引用和指针的尺寸,

引用不占内存,指针的尺寸和cpu的字长有关.

- 右值引用,表示什么意思?有什么用?[完美转发是什么?]

可以实现移动语义,实现移动构造函数,避免深拷贝

STL中好多地方都用到了这个,如unique_ptr只支持移动构造函数

- 深拷贝和浅拷贝?

### inline关键字

- 有什么用?原理?优缺点?
- 和宏对比

### 类相关

- 如果不写构造函数,默认的构造函数是什么?

有两个:拷贝构造 赋值构造

- 初始化列表是什么?有什么好处?

- 静态类

### 多态

- C++的多态是什么,实现的原理是什么?

编译器厂商都是用虚函数和虚表实现的

- 纯虚函数是什么?
- 构造函数和析构函数是否可以是虚函数?为什么?



### STL

- 简单介绍一下STL
- 一些容器的特性以及使用场景

vector 动态数组 ,size和capacity ,以及扩容机制,扩容完之后迭代器失效等等

list 双向链表

map和unordered_map

- 介绍一下迭代器

- new delete 智能指针



### 如何避免临时对象生成

(可能是过时的)

临时对象一般是在栈上生成的,源码中不可见的对象,会多调用一次构造和析构函数

1. 传参和返回时,尽量使用引用传递而不是值传递, 
2. 实参和形参要类型匹配,不要发生隐式类型转换,比如使用显式关键字explicit





### 单片机相关

C51等简单的单片机,问一下中断的概念

STM32等ARM核的高级单片机

中断 中断向量表 DMA等问题



### QT相关

- 父类被析构时,需不需要手动析构子类对象,为什么?

对象树机制





## 操作系统相关

