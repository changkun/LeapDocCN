# 项目设置
这篇文章讨论如何向 Python 程序中引入 Python 库。

<!--This article discusses how to import the Python libraries in a Python program.-->

## 库
LeapMotion 的 Python API 作为 Python 扩展模块提供了一个包含 Python本身及本地代码。Python API 支持 Python 2.7。

<!--
Libraries
The Leap Motion Python API is provided as a Python extension module containing both Python and native code. The Python API supports Python 2.7.
-->

||Windows|Mac|Linux|
|:--|:--|:--|:--|
|Python模块|lib/Leap.py|lib/Leap.py|lib/Leap.py|
|32位本地库|lib/x86/LeapPython.pyd<br>lib/x86/Leap.dll||lib/x86/LeapPython.so<br>lib/x86/libLeap.so|
|64位本地库|lib/x64/LeapPython.pyd<br>lib/x64/Leap.dll||lib/x64/LeapPython.so<br>lib/x64/libLeap.so|
|通用二进制本地库||lib/LeapPython.so<br>lib/libLeap.dylib||

你可以在下载的 LeapMotion SDK 包的`lib`文件夹中找到这些库文件。在 WIndows 和 Linux 上，32位 Python 需要使用 x86的库文件，64位的 Python 需要使用 x64 的库文件。

<!--You can find these libraries in the lib folder of the Leap Motion SDK download package. On Windows and Linux, you must use the x86 versions of the native libraries for 32-bit versions of Python and the x64 versions for 64-bit versions of Python.-->

LeapMotion 没有把库作为一个标准的 Python 包直接安装到用户电脑上。而是把库作为你应用的一个内置模块，你应该吧库和你的应用程序一起发布。

<!--Leap Motion does not provide these libraries in a standard Python package or install them on end-user computers. Treat the libraries as internal modules of your application. It is your responsibility to distribute the libraries with your application.-->

## 包含 LeapMotion 模块

为了引入 Leap 模块，这些苦文件必须放置到和 Python 运行时可以找到的地方。最简单的方法就是把库文件和程序代码放到同一个目录中。Python 会在同一个目录里导入这个模块。

<!--Importing the Leap Motion Module
To import the Leap module, the library files must be placed in a location where the Python runtime can find them. The easiest way to do this is to put them in the same directory as your application source code. Python looks in the same directory as the importing file for imported modules.-->

如果你想把库放在与你源码不同的目录，你可以在引入模块前把库文件的路径添加到`sys.path`中：

<!--If you prefer to keep the libraries in a separate directory from your source code, you can add the path to the Leap Motion libraries to the Python sys.path list before importing the Leap module:-->

```python
import sys
sys.path.insert(0, "path/to/leap/libraries")
import Leap
```

例如，你项目的文件结构可以像这样：

<!--For example, if your project file structure looked like:-->

```
SnakesAndLadders/
    src/
        Snakes.py
        Ladders.py
    lib/
```
你也可以将 LeapMotion 库文件拷贝到`lib`子文件夹中（确保复制的是适合你的平台架构的文件）。比如在 Mac 上，你的项目结构可以这样：

<!--You could copy the Leap Motion libraries to the lib subfolder (making sure to copy the appropriate files for your platform and architecture). For example, on a Mac, your project would look like:-->

```
SnakesAndLadders/
    src/
        Snakes.py
        Ladders.py
    lib/
        Leap.py
        LeapPython.so
        libLeap.dylib
```

于是你可以使用下面的方法在`Snakes.py`或者`Ladders.py`中引入 Leap 模块：

<!--From the Snakes.py or Ladders.py source, you could then import the Leap module with the following:-->

```python
import sys
sys.path.insert(0, "../lib")
import Leap
```

这种引入的方式假设你的 Python 文件总是运行在当前工作目录下运行。为使得主程序能够从任何位置运行时都能正常工作，你可以使用 Python`inspect`模块获取包含源文件的路径并设置`sys.path`关联到那个文件件：

```python
import os, sys, inspect
src_dir = os.path.dirname(inspect.getfile(inspect.currentframe()))
lib_dir = os.path.abspath(os.path.join(src_dir, '../lib'))
sys.path.insert(0, lib_dir)
import Leap
```

**注意**：如果你开发的程序只为你自己使用，你可以把 Leap 模块和其他需要的库放在任何位置，比如其中一个文件夹放置`sys.path`变量，另一个文件夹是你的`PYTHONPATH`环境变量等等。只需在更新 SDK 的时候你还能记得你把它们放到哪儿了。然而，自从 Leap 模块目前不在 Python 包管理器有效，不推荐吧 LeapMotion 拷贝到 Python 标准模块索引的位置。这样做会导致多个程序尝试安装他们不同的 LeapMotion 库时而发生冲突。

<!--Note: If you are developing applications solely for your own use, you can put the Leap module and its supporting native libraries in any convenient location: for example, in one of the folders listed in the Python sys.path variable, a folder referenced in your PYTHONPATH environment variable, etc – just remember where you put them when it comes time to update your Leap Motion SDK. However, since the Leap module isn’t currently available through standard Python package managers, copying the Leap Motion libraries to one of the standard Python module search locations isn’t recommended. Doing so could create conflicts if multiple applications try to install their own version of the Leap Motion libraries.-->

## 支持 32 位和 64 位 Python 架构

要同时支持 Windows 和 Linux 32位及64位架构，你可以运行时检查然后用 `sys.path` 设置正确的文件即可。在 Mac 中，LeapMotion 库是通用二进制的，支持两种架构，这种技术是不需要的。

<!--Supporting 32- and 64-bit Python Architectures¶
To support both 32-bit and 64-bit architectures at the same time on Windows and Linux, you can use a run-time check for the architecture and then set the sys.path to reference the correct files. On Mac, the Leap Motion libraries are universal binaries that support both architectures, so this technique is not needed.
-->

以 SnakeAndLadders 为例，在程序里你应该吧两种库都分别放到两个文件夹中，例如：

<!--Using the hypothetical SnakesAndLadders project as an example again, you would copy both sets of library files to separate folders within the application, for example:-->

```
SnakesAndLadders/
    src/
        Snakes.py
        Ladders.py
    lib/
        x86/
            Leap.py
            LeapPython.so
            libLeap.so
        x64/
            Leap.py
            LeapPython.so
            libLeap.so
```
然后引入合适的 Leap 模块：

<!--And then reference the proper Leap module at run time:-->

```python
import os, sys, inspect
src_dir = os.path.dirname(inspect.getfile(inspect.currentframe()))
arch_dir = '../lib/x64' if sys.maxsize > 2**32 else '../lib/x86'
sys.path.insert(0, os.path.abspath(os.path.join(src_dir, arch_dir)))

import Leap
```
相同的办法你可以同时支持更多平台。

<!--The same technique could be extended to support multiple platforms at the same time.-->


## 使用不同的 Python 发行版
在 Mac、Linux、或者自荐的 Python 中使用 LeapMotion 的 Python 库，你必须更新 `LeapPython.so` 的加载路径到 Python 的相应实例。

<!--Using a Different Python Distribution
To use the Leap Motion Python libraries with an alternate Python 2.7 distribution on Mac or Linux (i.e HomeBrew or MacPorts, etc.) or with a self-built version of Python, you must update the LeapPython.so loader path to reference the desired instance of Python.-->

首先，运行`otool`工具来显示当前的加载路径：

<!--First, run the otool utility to display the current loader paths:-->

```bash
otool -L LeapPython.so
```

显示结果与下面很相似：

<!--Which will display output similar to:-->

```
LeapPython.so:
    @loader_path/LeapPython.so (compatibility version 0.0.0, current version 0.0.0)
    /Library/Frameworks/Python.framework/Versions/2.7/Python (compatibility version 2.7.0, current version 2.7.0)
    @loader_path/libLeap.dylib (compatibility version 0.7.0, current version 2.0.1)
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 169.3.0)
    /usr/lib/libstdc++.6.dylib (compatibility version 7.0.0, current version 56.0.0)
```

Python位于 `/Library/Frameworks/Python.framework/Versions/2.7/Python` 这行，它需要用`install_name_tool`工具来修改。

<!--The line starting with, /Library/Frameworks/Python.framework/Versions/2.7/Python is the reference to Python, which needs to be changed with the install_name_tool utility.-->

其次，使用 `install_name_tool` 工具把 Python 的路径修改到你所需要的位置，例如：
<!--Second, run the install_name_tool utility to update the Python reference to the desired location. For example:-->

```python
install_name_tool -change /Library/Frameworks/Python.framework/Versions/2.7/Python \
/usr/local/Cellar/python/2.7.5/Frameworks/Python.framework/Versions/2.7/lib/libpython2.7.dylib \
LeapPython.so
```
**注意**：`otool`和`install_name_tool`都是标准的 Linux 和 OS X 命令行工具。

<!--Note: otool and install_name_tool are standard Linux and OS X command line utilities.-->

# 为 Python 3 重新编译 LeapPython
LeapMotion SDK 包含的 LeapPython 库文件只支持 Python2.7。然而 SDK 还包含 SWIG 结构文件，它可以用来生成 LeapPython 源代码。所以，高级用户可以生成并编译他们自己的 LeapPython。作为指导，请参考[使用 SWIG2.0.9 生成 Python3.3.0 包](https://support.leapmotion.com/entries/39433657-Generating-a-Python-3-3-0-Wrapper-with-SWIG-2-0-9)。

<!--Recompiling LeapPython for Python 3¶
The LeapPython library included in the Leap Motion SDK supports only Python 2.7. However, the SDK also includes the SWIG interface file used to generate the LeapPython source code, so advanced users can generate and compile their own version of LeapPython. For instructions, refer to Generating a Python 3.3.0 Wrapper with SWIG 2.0.9 in our support knowledge base.-->