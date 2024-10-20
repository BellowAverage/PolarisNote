
--- 
title:  C/C++中的static关键字详细解析 
tags: []
categories: [] 

---
### 1.C和C++中static共有特性
- 修饰全局变量，表明一个全局变量只对定义在同一文件中的函数可见。
```
在全局变量前加上关键字static，全局变量就变成了一个全局静态变量。
静态存储区：在整个程序执行期间一直存在。 
初始化：未经初始化的全局静态变量会自动初始化为0（否则不经过初始化的值是任意的）
作用域：全局静态变量在声明之前他的文件之外是不可见的，准确地说是从定义之处开始，到文件结尾。

```

当我们同时编译多个文件时，所有未加 static 前缀的全局变量和函数都具有全局可见性。为理解这句话，我举例来说明。我们要同时编译两个源文件，一个是 test1.h，另一个是 main.c。 test1.h

```
#include &lt;iostream&gt;
#include &lt;string&gt;

using namespace std;

string a = "this is a var"; // global variable

void msg()
{<!-- -->
    cout &lt;&lt; "hello world!" &lt;&lt; endl;
}

```

main.c

```
#include "test1.h"

int main()
{<!-- -->    
    // extern string a;    // extern variable must be declared before use
    cout &lt;&lt; "a:" &lt;&lt; a &lt;&lt; endl;
    msg();
    return 0;
}

```

输出结果：

```
A Hello

```

如果加了 static，就会对其它源文件隐藏。例如在 a 和 msg 的定义前加上 static，main.c 就看不到它们了。利用这一特性可以在不同的文件中定义同名函数和同名变量，而不必担心命名冲突。
- 修饰局部变量，表明该变量的值不会因为函数终止而丢失。
```
在静态局部变量之前加上关键字static，局部变量就变成了一个局部静态变量。
内存中的位置：也是静态存储区
初始化：未经初始化的局部静态变量会被初始化为0（自动对象的值是任意的）
作用域：局部作用域，当定义他的语句或者函数块结束的时候，作用域结束。
但是当局部静态变量离开作用域后，并没有销毁，而是仍然驻留在内存中，只是我们不能对他进行访问，直至该函数再次调用，并且值不变。

```
- 修饰函数，表明该函数只在同一文件中调用。
```
在函数返回类型前面加上static，函数就定义成静态函数。
函数的定义和声明在默认的情况下都是extern的，但静态函数只是在声明的文件中可见，不能被其他文件所用。
函数的实现使用static修饰，那么这个函数只可在本cpp内使用，不会同其他cpp中的同名函数引起冲突；
warning：不要再头文件中声明static的全局函数，不要在cpp内声明非static的全局函数，
如果你要在多个cpp中复用该函数，就把它的声明提到头文件里去，否则cpp内部声明需加上static修饰；

```

### 2.C++中static独有特性
- 修饰类的数据成员，表明对该类所有对象这个数据成员都只有一个实例。即该实例归 所有对象共有。- 用static修饰不访问非静态数据成员的类成员函数。这意味着一个静态成员函数只能访问它的参数、类的静态
### 3.static作用

```
1.先来介绍它的第一条也是最重要的一条：隐藏。（static函数，static变量均可）
当同时编译多个文件时，所有未加static前缀的全局变量和函数都具有全局可见性。
2.static的第二个作用是保持变量内容的持久。（static变量中的记忆功能和全局生存期）
存储在静态数据区的变量会在程序刚开始运行时就完成初始化，也是唯一的一次初始化。
共有两种变量存储在静态存储区：全局变量和static变量，只不过和全局变量比起来，
static可以控制变量的可见范围，说到底static还是用来隐藏的。
3.static的第三个作用是默认初始化为0（static变量）
其实全局变量也具备这一属性，因为全局变量也存储在静态数据区。在静态数据区，
内存中所有的字节默认值都是0x00，某些时候这一特点可以减少程序员的工作量。
4.static的第四个作用：C++中的类成员声明static
1)函数体内static变量的作用范围为该函数体，不同于auto变量，该变量的内存只被分配一次，
因此其值在下次调用时仍维持上次的值；
2)在模块内的static全局变量可以被模块内所用函数访问，但不能被模块外其它函数访问；
3)在模块内的static函数只可被这一模块内的其它函数调用，这个函数的使用范围被限制在声明它的模块内；
4)在类中的static成员变量属于整个类所拥有，对类的所有对象只有一份拷贝；
5)在类中的static成员函数属于整个类所拥有，这个函数不接收this指针，因而只能访问类的static成员变量。
类内：
6)static类对象必须要在类外进行初始化，static修饰的变量先于对象存在，
所以static修饰的变量要在类外初始化；
7)由于static修饰的类成员属于类，不属于对象，因此static类成员函数是没有this指针的，
this指针是指向本对象的指针。正因为没有this指针，所以static类成员函数不能访问非static的类成员，
只能访问 static修饰的类成员；
8)static成员函数不能被virtual修饰，static成员不属于任何对象或实例，
所以加上virtual没有任何实际意义；
静态成员函数没有this指针，虚函数的实现是为每一个对象分配一个vptr指针，
而vptr是通过this指针调用的，所以不能为virtual；
虚函数的调用关系，this-&gt;vptr-&gt;ctable-&gt;virtual function


```
