
--- 
title:  Mac下将Python源码打包成可执行程序（基于py2applet） 
tags: []
categories: [] 

---
### 1、安装py2app

打开终端，执行命令：

```
pip install py2app
```

### 2、创建存储文件夹

自选一个目录位置，创建一个文件夹，命名xxx（如app），用于存放待打包的源代码、相关配置文件、及最终的打包结果。

### 3.源代码准备

将待打包的源代码复制到步骤2中的文件夹

### 4、生成配置文件

入终端，切路径至步骤2中的xxx文件夹下，执行命令，生成配置文件。

如下命令，其中 app.py 为待打包的源代码文件，读者替换成自己的文件名即可。

```
py2applet --make-setup app.py
```

### 5、开始打包应用

切路径至步骤2中的xxx文件夹下，执行命令，打包应用

```
python setup.py py2app
```

### 6、完毕

步骤2中的xxx文件下出现dist文件夹，打开后里面有个app，双击即可运行
