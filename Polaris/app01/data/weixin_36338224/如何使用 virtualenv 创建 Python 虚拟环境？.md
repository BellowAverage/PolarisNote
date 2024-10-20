
--- 
title:  如何使用 virtualenv 创建 Python 虚拟环境？ 
tags: []
categories: [] 

---
### 1. 什么是虚拟环境？

虚拟环境的意义，就如同 虚拟机 一样，它可以实现不同环境中Python依赖包相互独立，互不干扰。

举个例子吧。

假设我们的电脑里有两个项目，他们都用到同一个第三方包，本来一切都顺利。但是由于某种原因，项目B由于某些原因要使用这个第三方包的一些新特性（新版本才有），而如果就这样贸然升级了，对项目A的影响我们无法评估，这个时候我们就特别需要有一种解决方案可以让项目A和B，处于两个不同的Python环境中。互不影响。

为了方便大家对虚拟环境有个认识，我列举了下其优点：
- 使不同应用开发环境独立- 环境升级不影响其他应用，也不会影响全局的python环境- 可以防止系统中出现包管理混乱和版本的冲突
市场上管理 Python 版本和环境的工具有很多，这里列举几个：
- `p`：非常简单的交互式 python 版本管理工具。- `pyenv`：简单的 Python 版本管理工具。- `Vex`：可以在虚拟环境中执行命令。- `virtualenv`：创建独立 Python 环境的工具。- `virtualenvwrapper`：virtualenv 的一组扩展。
工具很多，但个人认为最好用的，当属 `virtualenvwrapper`，推荐大家也使用。 

### 2. virtualenv

由于 virtualenvwrapper 是 virtualenv 的一组扩展，所以如果要使用 virtualenvwrapper，就必须先安装 virtualenv。

**安装**

```
$ pip install virtualenv

# 检查版本
$ virtualenv --version
```

**基本使用**

由于virtualenv创建虚拟环境是在当前环境下创建的。所以我们要准备一个专门存放虚拟环境的目录。（以下操作在Linux在完成，windows相对简单，请自行完成，有不明白的请微信与我联系。）

**创建**

```
# 准备目录并进入
$ mkdir -p /home/wangbm/Envs
$ cd !$

# 创建虚拟环境（按默认的Python版本）
# 执行完，当前目录下会有一个my_env01的目录
$ virtualenv my_env01

# 你也可以指定版本
$ virtualenv -p /usr/bin/python2.7 my_env01
$ virtualenv -p /usr/bin/python3.6 my_env02

# 你肯定觉得每次都要指定版本，相当麻烦吧？
# 在Linux下，你可以把这个选项写进入环境变量中
$ echo "export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python2.7" &gt;&gt; ~/.bashrc
```

**进入/退出**

```
$ cd /home/wangbm/Envs

# 进入
$ source my_env01/bin/activate

# 退出
$ deactivate
```

**删除** 删除虚拟环境，只需删除对应的文件夹就行了。并不会影响全局的Python和其他环境。

```
$ cd /home/wangbm/Envs
$ rm -rf my_env01
```

>  
 注意： 创建的虚拟环境，不会包含原生全局环境的第三方包，其会保证新建虚拟环境的干净。 


如果你需要和全局环境使用相同的第三方包。可以使用如下方法：

```
# 导出依赖包
$ pip freeze &gt; requirements.txt

# 安装依赖包
$ pip install -r requirements.txt 
```

### 3. virtualenvwrapper

virtualenv 虽然已经相当好用了，可是功能还是不够完善。

你可能也发现了，要进入虚拟环境，必须得牢记之前设置的虚拟环境目录，如果你每次按规矩来，都将环境安装在固定目录下也没啥事。但是很多情况下，人是会懒惰的，到时可能会有很多个虚拟环境散落在系统各处，你将有可能忘记它们的名字或者位置。

还有一点，virtualenv 切换环境需要两步，退出 -&gt; 进入。不够简便。

为了解决这两个问题，virtualenvwrapper就诞生了。

**安装**

```
# 安装 - Linux
pip install virtualenvwrapper

# 安装 - Windows
pip install virtualenvwrapper-win
```

**配置** 先find一下`virtualenvwrapper.sh`文件的位置

```
find / -name virtualenvwrapper.sh
# /usr/bin/virtualenvwrapper.sh
```

若是 windows 则使用everything 查找 virtualenvwrapper.bat 脚本

```
D:\Program Files (x86)\Python38-32\Scripts\virtualenvwrapper.bat
```

在~/.bashrc 文件新增配置

```
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/workspace
export VIRTUALENVWRAPPER_SCRIPT=/usr/bin/virtualenvwrapper.sh
source /usr/bin/virtualenvwrapper.sh
```

若是 windows 则新增环境变量：`WORKON_HOME`

<img src="https://img-blog.csdnimg.cn/20201029125012152.png" alt="">

**基本语法**：

mkvirtualenv [-a project_path] [-i package] [-r requirements_file] [virtualenv options] ENVNAME

**常用方法**

```
# 创建
$ mkvirtualenv my_env01

# 进入
$ workon my_env01

# 退出
$ deactivate

# 列出所有的虚拟环境，两种方法
$ workon
$ lsvirtualenv

# 在虚拟环境内直接切换到其他环境
$ workon my_env02

# 删除虚拟环境
$ rmvirtualenv my_env01
```

**其他命令**

```
# 列出帮助文档
$ virtualenvwrapper

# 拷贝虚拟环境
$ cpvirtualenv ENVNAME [TARGETENVNAME]

# 在所有的虚拟环境上执行命令
$ allvirtualenv pip install -U pip

# 删除当前环境的所有第三方包
$ wipeenv

# 进入到当前虚拟环境的目录
$ cdsitepackages

# 进入到当前虚拟环境的site-packages目录
$ cdvirtualenv

# 显示 site-packages 目录中的内容
$ lssitepackages
```

更多内容，可查看 官方文档 

### 4. 实战演示

以上内容，是一份使用指南。接下来，一起来看看，如何在项目中使用虚拟环境。

如何使用在我们的开发中使用我们的虚拟环境呢

通常我们使用的场景有如下几种
- 交互式中- PyCharm中- 工程中
接下来，我将一一展示。

#### 4.1 交互式中

先对比下，全局环境和虚拟环境的区别，全局环境中有requests包，而虚拟环境中并未安装。 当我们敲入 `workon my_env01`，前面有`my_env01`的标识，说明我们已经处在虚拟环境中。后面所有的操作，都将在虚拟环境下执行。 <img src="https://img-blog.csdnimg.cn/20201029125026819.png" alt="">

#### 4.2 工程项目中

我们的工程项目，都有一个入口文件，仔细观察，其首行可以指定Python解释器。

倘若我们要在虚拟环境中运行这个项目，只要更改这个文件头部即可。

现在我还是以，`import requests` 为例，来说明，是否是在虚拟环境下运行的，如果是，则和上面一样，会报错。

文件内容：

```
#!/root/.virtualenvs/my_env01/bin/python

import requests
print "ok"
```

运行前，注意添加执行权限。

```
$ chmod +x ming.py
```

好了。来执行一下

```
$ ./ming.py
```

发现和预期一样，真的报错了。说明我们指定的虚拟环境有效果。 <img src="https://img-blog.csdnimg.cn/20201029125028681.png" alt="">

#### 4.3 PyCharm中

点击 File - Settings - Project - Interpreter <img src="https://img-blog.csdnimg.cn/20201029125031348.png" alt=""> 点击小齿轮。如图点击添加，按提示添加一个虚拟环境。然后点 OK 就可以使用这个虚拟环境，之后的项目都会在这个虚拟环境下运行。 <img src="https://img-blog.csdnimg.cn/20201029125033435.png" alt="">
