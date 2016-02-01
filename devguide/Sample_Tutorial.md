# Hello World

本文主要暂时如何连接 LeapMotion 控制机以及访问基本的追踪数据。读完本文并亲自实践之，将会为你之后开发自己的应用程序打下一个坚实的基础。

首先，先介绍一些背景知识……

## LeapMotion 控制器工作原理
LeapMotion 控制器包含硬件和软件两个部分。

LeapMotion 硬件部分包含了一对立体红外相机和 LED 照明灯。相机传感器在设备处于标准位置时朝上。下图展示了LeapMotion如何监视一个用户的手：

![LeapView](../images/Leap_View.jpg)

LeapMotion 的软件部分则负责接收传感器的数据并分析这些与手、手指、手臂、工具的数据（追踪其他类型的物体特性会在以后被添加，目前这些就是全部能够被追踪的集合）。 软件包含一个手的内部模型和收到的传感器数据进行对比来确定最佳匹配。传感器数据以帧为单位，将每一帧数据发送给支持 LeapMotion 的应用。 你的程序接收到Frame 对象包含了全部的已知位置、向量及全部追踪的到的特点，比如手、手指、工具等。类似手势、动作这种横跨多个帧的数据同样会在每帧被更新。作为控制器提供的追踪数据的综述，请参考 API 综述.

LeapMotion 软件会宗伟一个服务（Windows）或后台（Mac 或 Linux）运行在电脑上。原生的 LeapMotion 支持程序可以通过 LeapMotion 动态库（SDK 里的一部分）使用 API 连接到这个服务。网页应用可以连接到一个 WebSocket 服务器。WebSocket 会发送一个 JSON 格式的追踪数据消息，每个消息便是一帧数据。LeapJS 是一个 Javascript 库，提供 API 封装这些数据。更多信息可以参考 系统架构。

## 设置文件
本教程使用命令行编译器以及链接器（需要时）以便专注于代码而不是环境本身。如何在 IDE 中使用 SDK 简历项目的细节请参考项目设置。

1. 如果你准备好了，从开发者网站下载并解压最新版本的 LeapMotion SDK 并安装最新的 LeapMotion 服务。

2. 打开终端或控制台，进入 SDK 的samples文件夹。

3. Sample.py 包含了本教程的完整代码，但为了获得更好的学习效果，你也可以重命名这个文件并在文件夹中创建一个空的新文件。

4. 在你的新文件 Sample.py 中， 使用代码引入 LeapMotion 库，下面的代码用来判断使用的是 32 还是 64 位 Python 从而引入合适的库：

```python
import os, sys, inspect, thread, time
src_dir = os.path.dirname(inspect.getfile(inspect.currentframe()))
arch_dir = '../lib/x64' if sys.maxsize > 2**32 else '../lib/x86'
sys.path.insert(0, os.path.abspath(os.path.join(src_dir, arch_dir)))

import Leap
from Leap import CircleGesture, KeyTapGesture, ScreenTapGesture, SwipeGesture
```

5. 添加结构化的代码定义 Python 命令程序：

```python
def main():

    # 保持运行，按回车键退出
    print "按回车键退出..."
    try:
        sys.stdin.readline()
    except KeyboardInterrupt:
        pass

if __name__ == "__main__":
    main()
```
注意: sys.stdin.readline() 在 IDEL 和其他一些 IDE 中执行得不好，你需要使用其他方式来保证程序能够执行到main()函数的结尾使程序能够立即退出。

这段代码简单的打印的一条消息然后在退出之前等待键盘输入。见『运行示例』。

## 获得连接
下一步就是在程序中添加一个 Controller 对象使其能够连接到 LeapMotion 服务/后台。

```python
def main():
     controller = Leap.Controller()

     # 保持运行，按回车键退出
     print "按回车键退出..."
     try:
         sys.stdin.readline()
     except KeyboardInterrupt:
         pass
```
创建Controller 对象后，它会自动与 LeapMotion 服务连接，一旦建立连接，你便可以使用Controller.frame() 方法来获得追踪数据。

连接进程是异步的，因此你不能在一行创建Controller然后希望在下一行便能够获得数据，你必须等待连接的完成。但是，这需要多长时间？

## 监听与否
你可以添加一个 Listener 对象给 Controller，这提供了一个基于事件的机制来响应 Controller 的状态变化。这就是我们这个教程中用到的方法——但它并不总是最好的方法。

Listener 的问题： Listener 对象使用了独立的线程来执行事件中的代码。因此使用 Listener 机制会将复杂的线程问题引入你的程序当中。你有责任保证线程安全，让你的 Listener 子类中的代码安全的访问程序的其他部分。比如你一般不能从主线程外其他地方访问和 GUI 控制的相关变量。或者也可以创建和清理线程关联的附加开销。

避免 Listener： 在方便的情况下，你也可以值通过简单的查看一帧的 Controller 对象来避免 Listener 对象。很多程序已经有事件循环或者动画循环来驱动用户输入和动画。如果这样，你可以在每一个循环获取一次追踪数据，这通常也跟你使用数据的速度一样快。

The Listener 类在 API 中定义了一个函数的签名，这个函数会在 Controller 事件发生时被调用。你通过创建一个 Listener 子类并实现你感兴趣事件的回调函数。

接下来，添加 SampleListener 类到程序中：

```python
class SampleListener(Leap.Listener):

    def on_connect(self, controller):
        print "Connected"


    def on_frame(self, controller):
        print "Frame available"

def main():
    #...
```
如果你已经看过完成的文件，你可能注意到它有很多回调函数。你也可以加上一些其他的，但为了保证简单，我们将专注于 on_connect() 和 on_frame() 两个函数。

现在创建一个 SampleListener 对象使用你的新类并添加到你的 Controller 中：

```python
def main():
    # 创建 listener 和 controller
    listener = SampleListener()
    controller = Leap.Controller()

    # 对 controller 添加 listener 事件
    controller.add_listener(listener)

    # 结束时移除 listener
    print "Press Enter to quit..."
    try:
        sys.stdin.readline()
    except KeyboardInterrupt:
        pass
    finally:
        # Remove the sample listener when done
        controller.remove_listener(listener)
```
现在是时候测试你的程序了，跟随下面的指示：运行示例.

如果一切正确，你会看到终端窗口上打印出『Connected』然后是一堆『Frame Avaliable』的信息。如果有错误，你搞不清楚你可以在developer.leapmotion.com中问问。当开发出现问题时，可以打开可视化诊断。它会显示 LeapMotion 的追踪数据，你可以对比你程序的实现与可视化中的结果（他们使用同样的 API）从而判断出了什么问题。

## 连接后
当你的Controller 对象成功连接到 LeapMotion 服务，同时硬件部分也成功连接后，Controller 对象会将它的 is_connected 属性变为 true 并且使你的 Listener.on_connect() 执行回调（如果有）。

当 controller 连接后，你可以使用 Controller.enable_gesture() 和 Controller.set_policy() 来设置控制器属性。例如。你可以用 onConnect() 函数识别扫动的手势：

```python
def on_connect(self, controller):
    print "Connected"
    controller.enable_gesture(Leap.Gesture.TYPE_SWIPE);
```

## 帧
LeapMotion 系统中所有的追踪数据都是通过 Frame 对象进行传递。 你可以通过调用 Controller.frame() 从你的控制器（当连接成功后）来获得Frame 对象。 Listener 子类的 on_frame() 方法会在数据的新帧有效时被回调。 当你不使用 Listener 时，你可以比较你处理的最后一帧的 id 值来判断是否有新的帧。注意，通过设置 frame() 函数的 history 参数，你可以得到比目前一帧更早的帧（最多60个）。因此，即使监测的速度慢于 LeapMotion 的速度，你也可以处理每一帧。

为了获取 frame，可以把 frame() 添加到 on_frame() 回调中获取帧：

```python
def on_frame(self, controller):
    frame = controller.frame()
```
然后会打印一些 Frame 对象的属性：

```python
def on_frame(self, controller):
    frame = controller.frame()

    print "Frame id: %d, timestamp: %d, hands: %d, fingers: %d, tools: %d, gestures: %d" % (
          frame.id, frame.timestamp, len(frame.hands), len(frame.fingers), len(frame.tools), len(frame.gestures()))
```
再次运行你的程序，把手放在 LeapMotion 设备的上方，你可以看到每一帧的基本数据出现在控制台窗口中。

本教程到此结束，但是你可以查看原始示例程序的其他部分，用他们来获得每一帧中的 Hand, Finger, Arm, Bone 以及 Gesture 对象。

## 运行示例
输入下面的命令（当前位置为 SDK 的 samples 文件夹）：

```bash
python Sample.py
```

你应该能在应用初始化并连接 Leapm 后看见『Connected』消息被打印到标准输出流。然后你会看见 Leap 在onFrame事件中打印出每个时间点的帧信息。