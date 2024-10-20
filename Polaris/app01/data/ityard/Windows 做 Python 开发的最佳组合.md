
--- 
title:  Windows 做 Python 开发的最佳组合 
tags: []
categories: [] 

---
<img src="https://img-blog.csdnimg.cn/img_convert/93b42cda6d3af3f6f9ba1c4ae4f4efb4.png">

作者：Jon Fincher

来源：机器之心

在 Windows 上怎样做 Python 开发？是像大神那样使用纯文本编辑器，还是用更加完善的 IDE？到底是用自带的命令行工具，还是需要装新的 Terminal？本文将带你了解如何利用微软官方维护的 MS Terminal 与 VS Code，来为 Python 开发保驾护航。

使用 Windows 系统一大好处是它的应用太丰富了，甚至强大的 GPU 也能在闲暇时间做点其它「工作」。然而与 Linux 或 macOS 不同，在 Windows 上做开发总会遇到很多挑战，不论是文件编码、环境控制还是项目编译，开发过程中总会有一些神奇的收获。

这些对于初学者来说尤其突出：我们在安装某个库时可能出现各种依赖项错误，我们在读写文本时出现各种编码错误等等。

那么在 Windows 上如何做 Python 开发呢？相信大神们都会有自己的解决方案，但本文希望介绍微软官方发布的 Terminal 和 Visual Studio Code，希望它们能构建更流畅的 Windows 开发体验。

<img src="https://img-blog.csdnimg.cn/img_convert/e32dbe9c9242327c871d65cfdf3123cf.png">

Visual Studio Code 是程序员可以使用的最酷的代码编辑器之一，是一个可在所有平台上使用的开源、可扩展和轻量级编辑器。正是这些品质使微软的 VS Code 大受欢迎，并成为 Python 开发的绝佳平台。可能很多读者都比较熟悉 PyCharm 与 Jupyter Notebook 等常见的 Python IDE，但 VS Code 一样不会令你失望。

在本文中，你将学习到微软 Terminal 和 Visual Studio Code 的特性，包括：
- 什么是微软 Terminal- 微软 Terminal 效果怎么样- 安装 Visual Studio Code- 发现并安装 Python 扩展- 编写简单的 Python 应用程序- 了解如何在 VS Code 中运行和调试现有 Python 程序- 将 VS Code 连接到 Git 和 GitHub，与全世界分享你的代码
我们假设你了解 Python 开发，并且已经在系统上安装了某种版本的 Python（如 Python 2.7、Python 3.6/3.7、Anaconda 或其他）。由于 VS Code 可兼容所有主流平台，因此你可能会看到略有不同的 UI 元素，并且可能需要修改某些命令。

**新兴的微软 Terminal**

Windows Terminal 是一个开源终端应用程序，由微软在今年 5 月份的 Build 开发者大会上推出。MS Terminal 支持 Command Prompt 和 PowerShell 的所有优点，基本上命令行已经可以和 Linux 相融合了，除此之外运行命令提示符也是没问题的。

在 MS Terminal 开源后，GitHub 的 Star 量增长得非常快，目前已经超过了 5 万。这足以说明这个项目非常受关注，在社区的开源改进下，这个工具一定挺好用。

<img src="https://img-blog.csdnimg.cn/img_convert/71d9be876da57328cc5b04d50f818c3e.png">

MS Terminal 开源地址：https://github.com/microsoft/terminal

当然，目前 MS Terminal 已经可以直接下载安装程序了，社区的体验也非常不错。因此如果我们在 Windows 上做 Python 开发，命令行工具就可以采用 MS Terminal，它能解决很大一部分的包安装、环境控制等问题。

**MS Terminal 的效果怎么样**

MS Terminal 最核心的功能就是支持多条选项卡，且每一个选项卡都可以连接到命令行 shell 或应用，例如 Command Prompt 或通过 SSH 访问树莓派等。下图展示了这种多选项卡的支持情况：

<img src="https://img-blog.csdnimg.cn/img_convert/2ffcb1b28ee781802ae5e2c76540e0a0.png">

此外，除了功能外，更重要的就是颜值，就像我们常用 zsh 来提供更美观的命令行一样。虽然 zsh 目前的 GitHub 收藏量已经达到 9.4 万了，但 ReadMe 文档清楚地写着它最好用于 macOS 或 Linux。而新发布的 MS Terminal 不论在界面还是在文字风格，都以前都强了很多。

背景透明度、文字高亮都可以自行定义，还能定义 emoji 等符号。如下为基本的展示，我们可以根据自己的需要调整整个界面。

<img src="https://img-blog.csdnimg.cn/img_convert/f3e85360ab14977464a8b5703fe8b26f.png">

整个项目还在积极开发中，很多功能也都在完善与增加。不过既然是微软官方维护的开源项目，那么我们还是非常有信心的，至少在命令行部分可以降低开发过程中的各种报错。当然如果读者在 Windows 上有更好的命令行工具推荐，也可以在文末留言。

**安装和配置 VS Code**

前面介绍了开发中必不可缺的命令行工具，下面我们该聊一聊 VS Code 了，它是支持 Python 开发的核心工具。下面我们从最初的安装、环境管理到编写、测试、发布代码，介绍我们该如何优雅地使用 VS Code。

在任何平台上都可以安装 Visual Studio Code。官网提供了 Windows、Mac 和 Linux 的完整安装说明，并且会每月更新编辑器，其中包含新功能和错误修正。你可以在 Visual Studio Code 网站上找到所有安装内容：

<img src="https://img-blog.csdnimg.cn/img_convert/477d83045f9c6c082ac60fdee2307bf0.png">

此外，除名称相近外，Visual Studio Code（简称 VS Code）与基于 Windows 的更大规模的 Visual Studio 几乎没有其他相同的地方。

Visual Studio Code 本身支持多种语言，并且它的一个扩展模型具有支持其他组件的丰富生态系统。VS Code 每月更新，你可以在微软 Python 博客中了解更新信息。任何用户都可以克隆微软的 VS Code Github 仓库并贡献自己的代码。

VS Code UI 已有详细记录，这里不予赘述：

<img src="https://img-blog.csdnimg.cn/img_convert/1747be841a1df94d304e7d8ef25d04ab.png">

**Python 扩展**

如上所述，VS Code 通过详细记录的扩展模型支持多种编程语言的开发。Python 扩展使用户可以在 Visual Studio Code 中进行 Python 开发，具有以下特征：
- 既支持 Python 3.4 及更高版本，也支持 Python 2.7 版本- 使用 IntelliSense 完成代码补全- Linting- 调试支持- 代码片段支持- 单元测试支持- 自动使用 conda 和虚拟环境- 在 Jupyter 环境和 Jupyter 笔记本中进行代码编辑
<img src="https://img-blog.csdnimg.cn/img_convert/899762046bdd4b604b33906795929685.png">

Visual Studio Code 扩展不仅仅具有编程功能：
- Keymaps 允许已经熟悉 Atom，Sublime Text，Emacs，Vim，PyCharm 或其他环境的用户更加容易上手。- 主题自定义 UI，无论您喜欢在明亮，黑暗或更丰富多彩的地方进行编码。- 语言包提供本地化体验。
以下是比较有用的一些其他扩展和设置：
- GitLens 直接在编辑视窗中提供了大量有用的 Git 功能，包括非责任注释和存储库开发功能。- 通过从菜单中选择 File, Auto Save，可以轻松进行自动保存。默认延迟时间为 1000 毫秒，也可以重新配置。- Settings Sync 允许用户借助 GitHub 在不同的装置中同步自己的 VS Code 设置。如果用户在不同的计算机上工作，这有助于运行环境保持一致。- Docker 让用户可以快速轻松地使用 Docker，帮助创作 Dockerfile 和 docker-compose.yml，打包和部署项目，甚至为项目生成适当的 Docker 文件。
当然，在使用 VS Code 时，你可能会发现其他有用的扩展。请在评论中分享你的发现和设置！

单击活动栏（Activity Bar）上的「扩展」图标可以访问和安装新扩展和主题。用户可以输入关键词来搜索扩展程序，以多种方式对搜索结果进行排序，快速轻松地安装扩展程序。在本文中，在活动栏的 Extensions 项中键入 python 并单击 Install 即可安装 Python 扩展：

<img src="https://img-blog.csdnimg.cn/img_convert/58d85b0e76eda7285e5b786c802b3877.gif">

用户可以通过相同的方式查找和安装上述任何扩展。

**Visual Studio Code 配置文件**

值得一提的是，Visual Studio Code 可通过用户和工作区设置（User and Workspace Settings）实现高度配置。

用户设置（User settings）在所有 Visual Studio Code 实例中都是全局性的，而工作区设置（Workspace Settings）是特定文件夹或项目工作区的本地设置。工作区设置为 VS Code 提供了极大的灵活性，工作区设置会在整篇文章中提到。工作区设置以.json 文件的形式存储在名为.vscode 的项目工作区本地文件夹中。

**启动新的 Python 程序**

让我们以一个新的 Python 程序来探索 Visual Studio Code 中的 Python 开发。在 VS Code 中，键入 Ctrl + N 打开一个新文件。你也可以从菜单中选择「文件」-「新建」。

无论你如何操作，你都应该看到一个类似于以下内容的 VS Code 窗口：

<img src="https://img-blog.csdnimg.cn/img_convert/a6b5e7e4293e5dd6e01b8f46e4cbb3ec.png">

打开新文件后，你即可以输入代码。

**输入 Python 代码**

作为测试，我们可以快速编码埃拉托斯特尼筛法（Sieve of Eratosthenes，它可以找出小于已知数的所有质数）。在刚打开的新选项卡中键入以下代码：

<img src="https://img-blog.csdnimg.cn/img_convert/46c624cec77bb06aec2e65ba4c05bebf.png">

等等，这是怎么回事？为什么 Visual Studio Code 没有进行任何关键词高亮显示，也没有进行任何自动格式化或任何真正有用的操作呢？它提供了什么？

答案是，VS Code 不知道它正在处理的是什么类型的文件。缓冲区被称为 Untitled-1，如果你查看窗口的右下角，则可以看到 Plain Text（纯文本）。

若要激活 Python 扩展，请保存文件（从菜单中选择 File-Save 或者从命令面板中选择 File-Save File 或者只使用 Ctrl + S）为 sieve.py。VS Code 将看到.py 扩展名并正确地将该文件转化为 Python 代码。

现在你的窗口视图应如下所示：

<img src="https://img-blog.csdnimg.cn/img_convert/1cb246de136b5994511856af205bc2c5.png">

这样就好多了！VS Code 会自动将文件重新格式化为 Python 代码，你可以通过检查左下角的语言模式予以验证。

如果你有多个 Python 安装（如 Python 2.7、Python 3.x 或 Anaconda），则可以通过单击语言模式指示器或者从命令面板中选择 Python: Select Interpreter 来更改 VS Code 所要使用的 Python 解释器。默认情况下，VS Code 支持使用 pep8 格式，但你也可以选择 black 或 yapf。

<img src="https://img-blog.csdnimg.cn/img_convert/fb179a2a9ad3a726d8b28c772ac29fea.png">

现在可以添加其余的 Sieve 代码。若要查看 IntelliSense，请直接键入此代码而不要剪切和粘贴，你应该看到如下内容：

<img src="https://img-blog.csdnimg.cn/img_convert/8ebe9989ac304052a9cdbbd22a92387f.gif">

当键入代码时，VS Code 会对 for 和 if 语句下面的行进行自动、适当的缩进，添加右括号，并给出内容提示。

**运行 Python 代码**

现在代码已经完成，你可以运行它了。没有必要让编辑器执行此操作：Visual Studio Code 可以直接在编辑器中运行此程序。保存文件（Ctrl + S），然后在编辑器窗口中单击右键并选择在终端（Terminal）中运行 Python 文件（Run Python File）：

<img src="https://img-blog.csdnimg.cn/img_convert/c9464fa0cebc71d944430363fe802e4f.gif">

你会看到终端窗格显示在窗口的底部，并显示代码输出结果。

**编辑现有的 Python 项目**

在 Sieve of Eratosthenes 示例中，你创建了一个 Python 文件。作为一个例子这很不错，但很多时候，你需要创建更大的项目，并在更长的时间内在它上面进行开发。

典型的新项目工作流程可能如下所示：
- 创建一个文件夹来保存项目（可能包含一个新的 GitHub 项目）- 更改为新文件夹- 使用命令 code filename.py 创建初始 Python 代码
在 Python 项目（而不是单个 Python 文件）上使用 Visual Studio Code 开辟了更多功能，使得 VS Code 能够真正发挥作用。让我们来看看它在更大的项目中如何运作。

假如我们编写了一个计算器程序，该程序通过艾兹格·迪科斯彻（Edsger Dijkstra）调度场算法的一种变体来解析中缀符号（infix notation）编写的方程式。

为了说明 Visual Studio Code 以项目为中心的特征，我们现在开始在 Python 中重新创建调度场算法作为方程式评估库。相应 GitHub 地址：https://github.com/JFincher42/PyEval。

本地文件夹创建后，你可以快速打开 VS Code 中的整个文件夹。由于我们已经创建了文件夹和基本文件，所以首选方法（如上所述）做出如下修正：

>  
  cd /path/to/project 
  code . 
 

当你这种方式打开时，VS Code 了解并将使用它看到的任何 virtualenv、pipenv 或 conda 环境。你甚至不需要首先启动虚拟环境。通过菜单中的 File, Open Folder、键盘上的 Ctrl+K, Ctrl+O 或者命令面板中的 File, Open Folder 等方式，你可以打开用户界面（UI）上的文件夹。

以下是创建的方程式 eval 库项目：

<img src="https://img-blog.csdnimg.cn/img_convert/1c86a4446afe0b0c811475da6e7df57c.png">

当 Visual Studio Code 打开文件夹时，它还会再次打开上次打开的文件（这是可配置的）。你可以打开、编辑、运行和调试列出的任何文件。左侧活动栏中的资源管理器视图（Explorer view）提供文件夹中所有文件的视图，并显示当前选项卡集中有多少未保存文件。

**代码测试的支持**

VS Code 可以自动识别在 unittest、pytest 或 Nose 框架中编写的现有 Python 测试，但前提是在当前环境中安装了这些框架。作者在 unittest 框架中编写了一个用于方程式 eval 库的单元测试，你可以在这个例子中使用它。

若要运行项目中任何 Python 文件的现有单元测试，请单击右键并选择 Run Current Unit Test File。系统将提示指定测试框架，在项目中搜索测试的位置以及测试使用的文件名模式。

所有这些都保存为本地.vscode/settings.json 文件中的工作区设置，并可以进行修改。对于这个等式项目，你可以选择 unittest、当前文件夹和模式 *_test.py。

测试框架设置完成并显示测试后，你可以单击状态栏（Status Bar）上的 Run Tests 并从命令面板中选择一个 option 来运行所有测试：

<img src="https://img-blog.csdnimg.cn/img_convert/0512a550a42e653449dbaab3629a811e.png">

通过在 VS Code 中打开测试文件，单击状态栏上的 Run Tests，然后选择 Run Unit Test Method 以及其他要运行的特定测试，你还可以运行单个测试。这使得解决单个测试失败并重新运行失败的测试变得很简单，从而能够节省大量时间。测试结果显示在 Python Test Log 下的 Output 窗格中。

**调试支持**

即使 VS Code 是代码编辑器，直接在 VS Code 中调试 Python 也是可以的。VS Code 提供的诸多功能可以媲美好的代码调试器，包括：
- 自动变量跟踪- 监看表达式- 断点- 调用堆栈检查
你可以在活动栏上的 Debug 视图中看到这些功能：

<img src="https://img-blog.csdnimg.cn/img_convert/fea62d5259e9f5c67b6a5c66e8868be1.png">

调试器可以控制在内置终端或外部终端实例中运行的 Python 应用程序。它可以附加到已经运行的 Python 实例中，甚至可以调试 Django 和 Flask 应用程序。

在单个 Python 文件中调试代码就像按 F5 启动调试器一样简单。你可以按 F10 和 F11 分别跳过和进入函数，并按 Shift + F5 退出调试器。按 F9 设置断点，或者通过单击编辑器窗口中的左空白（lift margin）进行设置。

在开始调试更复杂的项目（包括 Django 或 Flask 应用程序）之前，你首先需要设置并选择调试配置。设置调试配置相对简单。从 Debug 视图中选择 Configuration 下拉列表（drop-down），然后选择 Add Configuration 和 Python：

<img src="https://img-blog.csdnimg.cn/img_convert/797d16dd9a69430bd4a85925ab6b5f8d.png">

Visual Studio Code 将在当前名为.vscode/launch.json 的文件夹下创建一个调试配置文件，它允许用户设置特定的 Python 配置以及调试 Django 和 Flask 等特定应用程序的设置。

你还可以执行远程调试，并调试 Jinja 和 Django 模板。关闭编辑器中的 launch.json 文件，然后从 Configuration 下拉列表中为应用程序选择正确的配置。

**Git 集成**

VS Code 不仅内置对源代码控制管理的支持，还支持 Git 和 GitHub。你可以在 VS Code 中安装对其他 SCM 的支持，并列使用它们。用户可以从 Source Control 视图访问源代码控制：

<img src="https://img-blog.csdnimg.cn/img_convert/e1f038d532ab8943550f57e4b1c953c8.png">

如果你的项目文件夹包含.git 文件夹，VS Code 会自动打开所有 Git / GitHub 功能。你可以执行以下诸多任务：
- 将文件提交给 Git- 将更改推送到远程存储库（remote repo）并从中取出更改- check-out 现有或创建新的分支和标签（branch and tag）- 查看并解决合并冲突（merge conflict）- 查看差异（view diffs）
所有这些功能都可以直接从 VS Code UI 获得：

<img src="https://img-blog.csdnimg.cn/img_convert/4cebb4d24028bff379f5440322b5c6a1.png">

VS Code 还可以识别编辑器外部进行的更改并且正确运作。

在 VS Code 中提交最近的更改相当简单。修改后的文件显示在 Source Control 视图中，并带有 M 标记，而新的未跟踪文件使用 U 标记。将鼠标悬停在文件上然后单击加号（+）可以暂存更改。在视图顶部添加提交消息，然后单击复选标记来提交更改：

<img src="https://img-blog.csdnimg.cn/img_convert/e55e6f2a746faf6985b7fade917f1133.png">

你也可以在 VS Code 中将本地提交（local commits）推送到 GitHub。从 Source Control 视图菜单中选择 Sync，或者单击分支指示器（branch indicator）旁边状态栏上的 Synchronize Changes。

所以在作者看来，Visual Studio Code 是最酷的通用编辑器之一，也是 Python 开发的最佳候选工具。希望你也可以在 Python 开发中尝试使用 Visual Studio Code 编辑器，相信不会令你失望的。

参考文章：

https://realpython.com/python-development-visual-studio-code

https://devblogs.microsoft.com/commandline/introducing-windows-terminal

&lt; END &gt;

<img src="https://img-blog.csdnimg.cn/img_convert/d76ce2035dc74851a312a919fc1f19f3.gif">

微信扫码关注，了解更多内容
