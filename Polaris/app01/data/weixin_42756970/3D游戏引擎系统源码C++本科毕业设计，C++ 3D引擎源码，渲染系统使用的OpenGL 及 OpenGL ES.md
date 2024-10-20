
--- 
title:  3D游戏引擎系统源码C++本科毕业设计，C++ 3D引擎源码，渲染系统使用的OpenGL 及 OpenGL ES 
tags: []
categories: [] 

---
## Effective 3D Engine

##### 渲染系统使用的OpenGL 及 OpenGL ES，Windows上OpenGL ES使用AMD的ES模拟器。

<img src="https://img-blog.csdnimg.cn/883a3a89a8fe48f889f3927d8b142094.png" alt="在这里插入图片描述">

### 环境部署

完整代码下载地址：

#### Win32环境配置
1. 编辑器- 将`proj_win32/RenderSystem/gles_renderSystem/GLES/dll` 中的dll文件拷贝到`proj_win32/bin/Editor`中。- 将`proj_win32/RenderSystem/opengl_renderSystem/glew2.1.0/bin/Release/Win32` 中的dll文件拷贝到`proj_win32/bin/Editor`中。- 打开`proj_win32/E3DEditor.sln` 设置`E3DEditorWindow`为启动项目，编译选项选择`EditorRelease`,编译Engine和Editor下的项目，运行E3DEditorWindow。1. WindowsPlayer- 将`proj_win32/RenderSystem/gles_renderSystem/GLES/dll` 中的dll文件拷贝到`proj_win32/bin/WindowsPlayer`中。- 将`proj_win32/RenderSystem/opengl_renderSystem/glew2.1.0/bin/Release/Win32` 中的dll文件拷贝到`proj_win32/bin/WindowsPlayer`中。- 打开`proj_win32/E3DEngine.sln` 设置`WindowsPlayer`为启动项目，编译选项选择`Release/Debug`,编译Engine和WindowsPlayer下的项目，运行WindowsPlayer，运行时需要项目资源，资源文件夹需要和exe文件在同级目录内，并取名为“App_Data”，或者从命令行给WindowsPlayer启动参数，启动参数为3个并用英文逗号分开，第一个参数是资源目录，第二个参数是编辑器的窗口句柄，此处可以不填，这个是为了从编辑器启动游戏后，游戏与编辑器相互通信用的，第三个参数是起始场景，也可以不填。
### Mono C#代码调试方法

下载并安装 `Xamarin Studio`，在系统环境变量中添加 `MONODEVELOP_SDB_TEST` 值为 1， 打开`MonoScriptManager.cpp` 修改`_DEBUG_CSHARP` 为 1，启动程序，这时候程序会进入等待状态，不会显示出来， 接下来在`Xamarin Studio`中打开`Demo.CSharp\Demo.CSharp.csproj`，在`Solution`面板中右键项目从打开菜单中选择 “RunWith -&gt; CustomConfiguration”， 窗口最下方`RunAction`处选择`Debug-Custom Command Mono Soft Debugger`,然后单击最右下方的`Debug`按钮， 打开新的窗口后，在IP一栏填入`127.0.0.1` Port一栏填入 `10000` 点击`Connect`按钮。之前处于等待的程序会出现了，接下来就可以在Xamarin Studio中调试Mono C#代码了。
