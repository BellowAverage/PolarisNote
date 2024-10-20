
--- 
title:  活久见~ Python 装包八种方法，你都 OK 吗？ 
tags: []
categories: [] 

---
### 1. 使用 easy_install

`easy_install` 这应该是最古老的包安装方式了，目前基本没有人使用了。下面是 `easy_install` 的一些安装示例

```
# 通过包名，从PyPI寻找最新版本，自动下载、编译、安装
$ easy_install pkg_name

# 通过包名从指定下载页寻找链接来安装或升级包
$ easy_install -f http://pythonpaste.org/package_index.html 

# 指定线上的包地址安装
$ easy_install http://example.com/path/to/MyPackage-1.2.3.tgz

# 从本地的 .egg 文件安装
$ easy_install xxx.egg

```

### 2. 使用 pip install

pip 是最主流的包管理方案，使用 `pip install xxx` 就可以从 PYPI 上搜索并安装 `xxx` （如果该包存在的话）。

下面仅列出一些常用的 `pip install`的安装示例

```
$ pip install requests

# 前提你得保证你已经下载 pkg 包到 /local/wheels 目录下
$ pip install --no-index --find-links=/local/wheels pkg

# 所安装的包的版本为 2.1.2
$ pip install pkg==2.1.2

# 所安装的包必须大于等于 2.1.2
$ pip install pkg&gt;=2.1.2

# 所安装的包必须小于等于 2.1.2
$ pip install pkg&lt;=2.1.2

```

更多 pip 的使用方法，可参考我之前写过的文章，介绍得非常清楚：

### 3. 使用 pipx

pipx 是一个专门用于安装和管理 cli 应用程序的工具，使用它安装的 Python 包会单独安装到一个全新的独有虚拟环境。

由于它是一个第三方工具，因此在使用它之前，需要先安装

```
$ python3 -m pip install --user pipx
$ python3 -m userpath append ~/.local/bin
Success!

```

安装就可以使用 pipx 安装cli 工具了。

```
# 创建虚拟环境并安装包
$ pipx install pkg

```

更多 pipx 的使用方法，可参考我之前写过的文章，介绍得非常清楚：

### 4. 使用 setup.py

如果你有编写 setup.py 文件，可以使用如下命令直接安装

```
# 使用源码直接安装
$ python setup.py install

```

### 5. 使用 yum

Python 包在使用 `setup.py` 构建的时候，对于包的发布格式有多种选项，其中有一个选项是 `bdist_rpm`，以这个选项发布出来的包是 `rpm` 的包格式。

```
# 发布 rpm 包
$ python setup.py bdist_rpm

```

对于`rpm` 这种格式，你需要使用 `yum install xxx` 或者 `rpm install xxx` 来安装。

```
# 使用 yum 安装
$ yum install pkg

# 使用 rpm 安装
$ rpm -ivh pkg

```

### 6. 使用 pipenv

如果你在使用 pipenv 创建的虚拟环境中，可以使用下面这条命令把包安装到虚拟环境中

```
$ pipenv install pkg

```

### 7. 使用 poetry

如果你有使用 poetry 管理项目依赖，那么可以使用下面这条命令安装包

```
# 直接安装包
$ poetry add pkg

# 指定为开发依赖
$ poetry add pytest --dev

```

### 8. 使用 curl + 管道

有一些第三方工具包提供的安装方法，是直接使用 curl 配置管道来安装，比如上面提到的 poetry 就可以用这种方法安装。

```
$ curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python

```

以上就是今天分享的内容，是不是涨姿势啦？

如果内容对你有帮助，可以请你帮我点个赞吗？hhhh

**本系列更多文章**
- - - - - - - - 