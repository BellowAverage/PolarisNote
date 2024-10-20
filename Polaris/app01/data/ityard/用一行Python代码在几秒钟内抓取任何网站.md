
--- 
title:  用一行Python代码在几秒钟内抓取任何网站 
tags: []
categories: [] 

---
如果你正在寻找最强大的 Python 抓取工具？不要再看了！这一行代码将帮助你立即启动并运行。

**Scrapeasy**

Scrapeasy 是一个 Python 库，可以轻松抓取网页并从中提取数据。它可用于从单个页面抓取数据或从多个页面抓取数据。它还可用于从 PDF 和 HTML 表格中提取数据。

Scrapeasy 让你只用一行代码就可以用 python 抓取网站，它非常便于使用并为你处理一切。你只需指定要抓取的网站以及你想要接收什么样的数据，其余的交给 Scrapeasy。

Scrapeasy Python 爬虫在编写时考虑到了快速使用。它提供以下主要功能：
- 一键抓取网站——不仅仅是单个页面。- 最常见的抓取活动（接收链接、图像或视频）已经实现。- 从抓取的网站接收特殊文件类型，如 .php 或 .pdf 数据。
**如何使用 Scrapeasy**

**通过 pip 下载**

```
$ pip install scrapeasy
```

**使用它**

Scraeasy 考虑到了易用性。首先，从 Scrapeasy 导入网站和页面

```
from scrapeasy import Website, Page
```

**初始化网站**

首先，让我们创建一个新的网站对象。对于这种方式，只需提供主页的 URL。我将使用我多年前创建的网站的 URL：

```
web =Website("https://tikocash.com/solange/index.php/2022/04/13/how-do-you-control-irrational-fear-and-overthinking/
")
```

**获取所有子站点的链接**

好的，现在我们的网站已经初始化，我们对 tikocash.com 上存在的所有子网站感兴趣，要找出这一点，请让 Web 对象接收所有子页面的链接。

```
links = web.getSubpagesLinks()
```

根据你的本地互联网连接和你正在抓取的网站的服务器速度，此请求可能需要一段时间，确保不要使用这种非常庞大的方法抓取整个网页。

但回到链接获取：通过调用 .getSubpagesLinks()，用你请求所有子页面作为链接，并将收到一个 URL 列表。

```
links2 = web.getSubpagesLinks()
```

你可能已经注意到缺少典型的 http://www.-stuff。这是没有目的的，并且使你的生活更容易进一步使用链接。但请确保——当你真正想在浏览器中或通过请求调用它们时——请在每个链接前面添加 http://www. 。

**查找媒体**

让我们尝试找到指向 fahrschule-liechti.com 放置在其网站上的所有图像的链接。

我们通过调用 .getImages() 方法来做到这一点。

```
images = web.getImages()
```

响应将包括指向所有可用图像的链接。

**下载媒体**

现在让我们做一些更高级的事情。我们喜欢 tikocash.com 在其网站上的图片，所以让我们将它们全部下载到我们的本地磁盘。听起来工作量是不是很大？其实很简单！

```
web.download("img", "fahrschule/images")
```

首先，我们定义通过关键字 img 下载所有图像媒体。接下来，我们定义输出文件夹，图像应保存到的位置。就是这样！运行代码，看看发生了什么。几秒钟之内，你就收到了 Tikocash.com 上的所有图片。

**获取链接**

接下来，让我们找出 tikocash.com 链接到哪些页面。为了获得总体概述，让我们找出它链接到的其他网站，出于这个原因，我们指定只获取域链接。

```
domains = web.getLinks(intern=False, extern=False, domain=True)
```

因此，我们得到了在 tikocash.com 上链接的所有链接的列表。

好的，但现在我们想进一步了解这些链接，我们如何做到这一点？

**获取链接域**

好吧，更详细的链接只不过是外部链接，所以，我们做了同样的请求，但这次包括外部，但不包括域。

```
domains = web.getLinks(intern=False, extern=True, domain=False)
```

在这里，我们将详细了解所有外部链接。

**初始化页面**

好的，到目前为止，我们已经看到了很多关于网站的东西，但是，我们还没有发现 Page 是做什么的。

好吧，如前所述，该页面只是网站中的一个站点，让我们通过初始化W3schools页面，来尝试不同的示例。

```
w3 = Page("https://www.w3schools.com/html/html5_video.asp")
```

如果你还没有猜到，你很快就会明白为什么我选择了这个页面。

**下载视频**

是的，你没听错。Scrapeasy 可让你在几秒钟内从网页下载视频，让我们来看看如何。

```
w3.download("video", "w3/videos")
```

是的，仅此而已。只需指定要将所有视频媒体下载到输出文件夹 w3/videos 中，就可以开始了。当然，你也可以只收到视频的链接，然后再下载，但这会不太酷。

```
video_links = w3.getVideos()
```

**下载其他文件类型（如 pdf 或图片）**

现在让我们更笼统地说，下载特殊文件类型，如 .pdf、.php 或 .ico 怎么样？使用通用的 .get() 方法接收链接，或使用文件类型作为参数的 .download() 方法。

```
calendar_links = Page("https://tikocash.com").get("php")
```

到这里就完毕。

现在让我们下载一些 PDF。

```
Page("http://mathcourses.ch/mat182.html").download("pdf", "mathcourses/pdf-files")
```

总之，Python 是一种通用语言，只需一行代码即可在几秒钟内抓取任何网站上的内容。

因此，这使其成为网络抓取和数据挖掘的强大工具。如果你需要从网站中提取数据，Python 是适合你的工具。

**总结**

以上就是我想跟你分享的关于用Python抓取网站的内容的实例教程，希望今天这个内容对你有用，如果你觉得有用的话，请点赞我，关注我，并将这篇文章分享给想学习如何用Python抓取网站内容数据的朋友，因为也许能够帮助到他。
- - - 