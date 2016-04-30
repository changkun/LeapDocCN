# SDK 库

LeapMotion 库由 C++编写。LeapMotion 还是用了 SWIG（一个开源工具）为 C#、Java、以及 Python 生成语言绑定。SWIG 生成的绑定会转化所绑定的编程语言上的调用到基于 C++ 的 LeapMotion 库。每个 SWIG 绑定使用了两个额外的库。对 JavaScript 和 Web 应用的开发，LeapMotion 提供了一个 WebSocket 服务和一个客户端 JavaScript 库。

<!--
The Leap Motion library is written in C++. Leap Motion also uses SWIG, an open source tool, to generate language bindings for C#, Java, and Python. The SWIG-generated bindings translate calls written in the bound programming language to calls into the base C++ Leap Motion library. Each SWIG binding uses two additional libraries. For JavaScript and web application development, Leap Motion provides a WebSocket server and a client-side JavaScript library.
-->

开发支持 Leap 的应用程序和插件所需要的的库、代码及头文件都包含在了 LeapMotion 的 SDK 中，除 `leap.js` 这个库外。你可以从 LeapMotion 开发者入口下载 LeapMotion 的 SDK。 SDK 对每个支持的操作系统都是可用的。JavaScript 客户端库被分开发布到了 LeapJS GitHub 仓库中，可以在[这里](https://github.com/leapmotion/leapjs)下载。

<!--
All the library, code, and header files required to develop Leap-enabled applications and plugins are included in the Leap Motion SDK, except the leap.js client JavaScript library. You can download the Leap Motion SDK from the Leap Motion Developer Portal. An SDK package is available for each supported operating system. The JavaScript client library is distributed separately and can be downloaded from the LeapJS GitHub repository.
-->

Unity 5 和 虚幻引擎4.9 的插件从主 SDK 中被分开提供。虚幻的插件集成在了虚幻引擎4.9以上的版本。而 Unity 的插件可以在[这里](https://developer.leapmotion.com/downloads/unity)下载。

<!--
Plugins for Unity 5 and Unreal Engine 4.9 are provided separately from the main SDK. The Unreal plugin is included with Unreal Engine 4.9+ (source code release only, at this time). The Unity plugin is available at https://developer.leapmotion.com/downloads/unity.
-->

## 支持的编译器和 IDE
* C++ on Windows: Visual Studio 2008, 2010, 2012, and 2013
* C++ on Mac: Xcode 3.0+, clang 3.0+, and gcc
* Objective-C: Mac OS 10.7+, Xcode 4.2+ and clang 3.0+
* C# for .NET framework versions 3.5 and 4.0
* Mono version 2.10
* Unity Pro and Personal versions 5.0
* Java versions 6 and 7
* Python version 2.7.3
* UnrealEngine 4.9

<!--
Supported Compilers and IDEs
C++ on Windows: Visual Studio 2008, 2010, 2012, and 2013
C++ on Mac: Xcode 3.0+, clang 3.0+, and gcc
Objective-C: Mac OS 10.7+, Xcode 4.2+ and clang 3.0+
C# for .NET framework versions 3.5 and 4.0
Mono version 2.10
Unity Pro and Personal versions 5.0
Java versions 6 and 7
Python version 2.7.3
UnrealEngine 4.9
-->

## Python
`Leap.py`包含了 Python 模块，你可以引用它到你的 Python 程序当中。这个模块加载了`LeapPython.so`(Mac 和 Linux)或`LeapPython.dll`(Windows)库文件。而这些库文件则加载了 `libLeap.dylib`、`Leap.dll` 或者 `libLeap.so`（取决于平台）。

<!--
Python
Leap.py contains the Python module that you reference in your Python application. This module loads LeapPython.so (Mac and Linux) or LeapPython.dll (Windows). These libraries load libLeap.dylib, Leap.dll, or libLeap.so (depending on platform).
-->

## C++
使用 C++ 开发 LeapMotion 控制器，需要包含 API 头文件到你的程序并且根据平台来链接 LeapMotion 的库`libLeap.dylib`、`Leap.dll` 或者 `libLeap.so`。

在 Windows 上，分别提供了 32 位和 64 位不同架构版本的库，以及调试生成与发布构建（共四个版本的组件）工具。

在 Mac OS X 上，两个不同架构均包含在了同一个库文件中。


<!--
C++
To develop for the Leap Motion Controller in C++, include the API header files in your program and link with the Leap Motion library, either libLeap.dylib, Leap.dll, or libLeap.so, depending on platform.

On Windows, separate libraries are provided for 32-bit versus 64-bit architectures as well as debug builds versus release builds (for a total of 4 versions for each component).

On Mac OS X, both architectures and release modes are supported in a single library file.
-->

# Objective-C
Objective-C 应用支持手动封装代码。为了构建支持 Leap 的 Objective-C 程序需要包含封装头文件和 Objective-C++ 代码文件以及 LeapMotion C++ 头文件。然后你就可以在纯的 Objective-C 应用中使用封装的类定义了。记得将`libLeap.dylib`、库以及你的应用链接到你的应用程序包中。

<!--
Objective-C
Objective-C applications are supported by hand-written wrapper code. To build a Leap-enabled Objective-C application, include the wrapper header and Objective-C++ code file in your application along with the Leap Motion C++ headers. You can then use the classes defined in the wrapper in (otherwise) pure Objective-C applications. Link your application with libLeap.dylib and include the library in your application package.
-->


## C#.
C# 类定义分别提供了 .NET 3.5 和 .NET 4.0 库。你的代码可以分别使用`LeapCSharp.NET3.5.dll` 或 `LeapCSharp.NET4.0.dll`（在所有支持的操作系统上使用相同的库名）。这些库调用了`libCSharp.dylib`(Mac)、`LeapCSharp.dll`(Windows) 或 `libLeapCSharp.so`(Linux)。中间库则加载了`libLeap.dylib`、`Leap.dll` 或 `libLeap.so` (取决于平台)。

<!--
C#
The C# class definitions are provided for .NET 3.5 and .NET 4.0 in separate libraries. Your code can reference either LeapCSharp.NET3.5.dll or LeapCSharp.NET4.0.dll (the same library names are used for this library on all supported operating systems). These libraries load libCSharp.dylib (Mac), LeapCSharp.dll (Windows), or libLeapCSharp.so (Linux). The intermediate libraries load libLeap.dylib, Leap.dll, or libLeap.so (depending on platform).
-->

## Unity
对于 Unity 5 而言，专业版和个人版都支持插件。Unity 插件使用了在`LeapCSharp.NET3.5.dll`中的 C# 类定义。这个库加载了本地的`libCSharp.dylib`(Mac)或`LeapCSharp.dll`(Windows) 库。反过来，这些中间库加载了 `libLeap.dylib` 或 `Leap.dll` (取决于平台)。

<!--
Unity
As of Unity 5, both the Pro and Personal versions support plugins. The Unity plugin uses the C# class definitions in LeapCSharp.NET3.5.dll. This library loads the native libCSharp.dylib (Mac) or LeapCSharp.dll (Windows) library. In turn, these intermediate libraries load libLeap.dylib or Leap.dll (depending on platform).
-->

## Java
`Leap.jar`包含了一个 LeapMotion 的 Java 类。这份代码加载了 `libLeapJava.dylib`(Mac)、`LeapJava.dll`(Windows) 或 `libLeapJava.so`(Linux)。这些库包含了原生的代码并把 Java 调用转化了给了`libLeap.dylib`、`Leap.dll`、`libLeap.so`（取决于平台）的基本 LeapMotion API。而基本 LeapMotion 动态库通过中间库进行加载。对于 64 位架构的 Windows，还需要 Microsoft Visual C 运行时库。

<!--
Java
Leap.jar contains the Leap Motion Java classes. This code loads libLeapJava.dylib (Mac), LeapJava.dll (Windows), or libLeapJava.so (Linux). These libraries contain the native code that translates the Java calls to the base Leap Motion API in libLeap.dylib, Leap.dll, or libLeap.so (depending on platform). The base Leap Motion dynamic library is loaded by the intermediate library. For Windows 64-bit architectures, the Microsoft Visual C runtime libraries are also required.
-->

## JavaScript
LeapMotion JavaScript 支持两个主要组件。第一个组件是 由 LeapMotion 服务提供的 WebSocket 服务器。这个服务器允许 Web 应用（或者任何应用连接到 WebSocket）来访问 LeapMotion 的 JSON 格式的追踪消息。第二个组件是一个 JavaScript 客户端库`Leap.js`。`Leap.js`是一个开源的 JavaScript API，它能够使用 WebSocket 的 JSON 数据并且提供了在一个设计哲学和结构形式都与本地 LeapMotion API一致的接口。

<!--
JavaScript
Leap Motion JavaScript support has two main components. The first component is the WebSocket server provided by the Leap Motion service. This server allows web applications (or any application that can connect to a WebSocket) to access Leap Motion tracking data as JSON-formatted messages. The second component is the JavaScript client library, Leap.js. Leap.js is an open-source JavaScript API that consumes the WebSocket JSON output and presents it in a form that is consistent in philosophy and structure to the native Leap Motion API.
-->

## 其他语言
很多社区诞生的语言绑定都是可用的，部分列表可以访问：[社区库](https://developer.leapmotion.com/libraries)。

<!--
Other Languages
Many community-created language bindings are available, for a partial list, visit: Community Libraries.
-->

## 操作系统支持
LeapMotion 软件现在支持 Linux(Ubuntu 12)、OS X 10.7+、Windows 7+。
<!--
Operating System Support
The Leap Motion software currently supports Linux (Ubuntu 12), OS X 10.7+, Windows 7+.
-->