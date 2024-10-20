
--- 
title:  100天精通Python（数据分析篇）——第48天：数据分析入门知识 
tags: []
categories: [] 

---


#### 文章目录
- - - - - 


## 1. 为什么要学数据分析？

近两年来，数据分析师的岗位需求非常大，90%的岗位技能需要掌握Python作为数据分析工具。Python语言的易学性、快速开发，拥有丰富强大的扩展库和成熟的框架等特性很好地满足了数据分析师的职业技能要求。

<img src="https://img-blog.csdnimg.cn/56b6989f3f924bd99848cd3360fd9e83.png#pic_center" alt="在这里插入图片描述">

## 2. 数据分析的概念

数据分析是指用适当的统计分析的方法对收集来的大量数据进行分析，提取有用信息和形成结论而对数据加以详细研究和概括总结的过程。——《 百度百科》

**数据分析的定义：**
- 用适当的<mark>统计分析方法</mark>对收集来的<mark>大量数据</mark>进行分析- 提取<mark>有用信息</mark>和形成<mark>结论</mark> 对数据加以<mark>详细研究</mark>和<mark>概括总结</mark>
**目的**：从数据中挖掘规律、验证猜想、进行预测

## 3. 数据分析涉及哪些能力

**计算机知识**：编程能力、量化操作、算法思想…

**数学和统计知识**：常见的分布、最小二乘法…

**行业知识**：业务场景、专业知识… <img src="https://img-blog.csdnimg.cn/e942630cd7e9426aa663b15dcf69beb4.png" alt="在这里插入图片描述">

## 4. 数据分析的流程

<img src="https://img-blog.csdnimg.cn/7f1e5e1d61f442d4987fb7c59f85ac81.png" alt="在这里插入图片描述">

**（1）明确目的：**
- 为什么要开展数据分析?- 通过数据分析要解决什么问题?- 需要从哪些角度进行分析?- 需要采用哪些分析指标I方法? …
**（2）数据获取（常用的数据获取途径）：**
-  网络爬虫 -  公开数据库 -  自有数据库 -  调查问卷 -  客户数据 
**（3）数据解析：**
- 把杂乱无章的数据处理成有一定结构、整洁的数据的过程- 数据清洗- 处理缺失值- 处理异常值
**（4）数据分析：**
- 如何对数据进行一些融合？- 如何进行一些数据的筛选？- 数据的一些替换
**（5）结果呈现：**
- 数据可视化- 机器学习简单介绍
## 5. Python做数据分析学什么？

**NumPy模块**： NumPy（Numerical Python的简称）是是Python 数据分析三剑客之一，它是高性能科学计算和数据分析的基础包。NumPy最重要的一个特点就是其N维数组对象（即ndarray），该对象是一个快速而灵活的大数据集容器。可以利用这种数组对整块数据执行一些数学运算，比python自带的数组以及元组效率更高，其语法跟变量元素之间的运算一样，无需进行循环操作。

**SciPy模块**： 是一个用于数学、科学、工程领域的常用软件包，可以处理插值、积分、优化、图像处理、常微分方程数值解的求解、信号处理等问题。它用于有效计算Numpy矩阵，使Numpy和Scipy协同工作，高效解决问题。

**Pandas模块**：（Python data analysis）组合缩写，是python中基于numpy和matplotlib的第三方数据分析库，与后两者共同构成了python数据分析的基础工具包，享有数分三剑客之名。对于和表格数据交互非常理想，Pandas中把表格数据称为数据框（DataFrame）。对画图功能也有一些包装，使得无需使用MPL（Meta-Programming Library，元编程库）就可以快速实现画图。我使用Pandas而非其他的工具来操作数据。

**MatPlotLib模块**： Matplotlib是Python中最常用的可视化工具之一，可以非常方便地创建海量类型地2D图表和一些基本的3D图表，可根据数据集（DataFrame，Series）自行定义x, y轴，绘制图形（线形图，柱状图，直方图，密度图，散布图等等），能够解决大部分的需要。Matplotlib中最基础的模块是pyplot。  
