
--- 
title:  Python代码文件不只是“.py” 
tags: []
categories: [] 

---
来源：麦叔编程

>  
  今天同事给我扔了一个`.pyd`文件，说让我跑个数据。然后我就傻了。。 
 

不知道多少粉丝小伙伴会run`.pyd`代码文件？如果你也懵懵的，请继续往下读吧。。

今天科普下各类`Python`代码文件的后缀，给各位`Python`开发“扫扫盲”。

### .py

最常见的Python代码文件后缀名，官方称`Python源代码文件`。

不用过多解释了~

### .ipynb

这个还是比较常见的，`.ipynb`是`Jupyter Notebook`文件的扩展名，它代表"`IPython Notebook`"。

学过数据分析，机器学习，深度学习的同学一定不陌生！

### .pyi

`.pyi`文件是`Python`中的类型提示文件，用于提供代码的**静态类型**信息。

一般用于帮助开发人员进行**类型检查**和**静态分析**。

示例代码：

```
hellp.pyi


def hello(name: str) -&gt; None:
    print(f"hello {name}")
```

>  
  `.pyi`文件的命名约定通常与相应的`.py`文件相同，以便它们可以被自动关联在一起。 
 

### .pyc

`.pyc`是`Python`字节码文件的扩展名，用于存储已编译的`Python`源代码的中间表示形式，因为是二进制文件所以我们无法正常阅读里面的代码。

>  
  `.pyc`文件包含了已编译的字节码，它可以更快地被`Python`解释器加载和执行，因为解释器无需再次编译源代码。 
 

### .pyd

`.pyd`是`Python`扩展模块的扩展名，用于表示使用`C`或`C++`编写的二进制`Python`扩展模块文件。

`.pyd`文件是编译后的二进制文件，它包含了编译后的扩展模块代码以及与`Python`解释器交互所需的信息。

此外，`.pyd`文件通过`import`语句在`Python`中导入和使用，就像导入普通的`Python`模块一样。

>  
  由于`C`或`C++`的执行速度通常比纯`Python`代码快，可以使用扩展模块来优化`Python`代码的性能，尤其是对于计算密集型任务。 
 

### .pyw

`.pyw`是`Python`窗口化脚本文件的扩展名。

它表示一种特殊类型的`Python`脚本文件，用于**创建没有命令行界面**（即控制台窗口）的窗口化应用程序。

>  
  一般情况下，运行`Python`脚本会打开一个命令行窗口，其中显示脚本输出和接受用户输入。但是，对于某些应用程序，如图形用户界面（GUI）应用程序，不需要命令行界面，而是希望在窗口中显示交互界面。这时就可以使用`.pyw`文件。 
 

示例代码：

```
# click_button.pyw


import tkinter as tk


def button_click():
    label.config(text="Button Clicked!")


window = tk.Tk()
button = tk.Button(window, text="Click Me", command=button_click)
button.pack()


label = tk.Label(window, text="Hello, World!")
label.pack()


window.mainloop()
```

### .pyx

`.pyx`是`Cython`源代码文件的扩展名。

`Cython`是一种**编译型的静态类型扩展语言**，它允许在`Python`代码中使用`C`语言的语法和特性，以提高性能并与`C`语言库进行交互。

我对比了下Cython与普通python的运行速度：

fb.pyx(需使用cythonize命令进行编译)

```
cdef int a, b, i


def fibonacci(n):
    if n &lt;= 0:
        raise ValueError("n必须是正整数")


    if n == 1:
        return 0
    elif n == 2:
        return 1
    else:
        a = 0
        b = 1
        for i in range(3, n + 1):
            a, b = b, a + b
        return b
```

run.py

```
import fb
import timeit


def fibonacci(n):
    if n &lt;= 0:
        raise ValueError("n必须是正整数")


    if n == 1:
        return 0
    elif n == 2:
        return 1
    else:
        a, b = 0, 1
        for _ in range(3, n + 1):
            a, b = b, a + b
        return b


# 纯Python版本
python_time = timeit.timeit("fibonacci(300)", setup="from __main__ import fibonacci", number=1000000)


# Cython版本
cython_time = timeit.timeit("fb.fibonacci(300)", setup="import fb", number=1000000)


print("纯Python版本执行时间:", python_time)
print("Cython版本执行时间:", cython_time)
```

得出结果：

```
纯Python版本执行时间: 12.391942400000516
Cython版本执行时间: 6.574918199999956
```

在这种计算密集任务情况下，`Cython`比普通`Python`效率快了近一倍。










