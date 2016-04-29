# 连接到控制器

通过创建 `Controller` 对象能够连接到 LeapMotion 设备。`Controller`对象能够在向你应用中通过 `Frame` 对象传递追踪数据时，自动建立和 LeapMotion 守护进程或服务的连接。

```python
controller = Leap.Controller()
```

使用`Controller`对象能够获取所硬件连接的信息以及设置你应用的一些连接选项。

## 获取帧

通过调用 `Controller.frame()` 函数来获取包含追踪数据的 `Frame` 对象。无论你的应用是否已经准备好处理由 LeapMotion 生成的最新的数据，你都能够调用这个函数。

更多信息请查看 [Frame](../api/Leap.Frame.md)。

## 前台和后台应用

通常，LeapMotion 服务或守护进程只能发送追踪数据给位于操作系统前台的应用程序。

如果你的应用运行在后台，而且你依然想要获取这些数据，那么你可以检查 `Controller.has_focus` 或者通过 Controller 对象监听调度事件。服务或守护进程会通过操作系统直接获取应用程序在当前系统中的状态。注意，Linux 操作系统并没有提供这些信息，因此运行在 Linux 系统下的应用总是能够收到追踪数据。

值得一提的是，应用连接到 LeapMotion 服务或守护进程的 WebSocket 服务时，不会自动的接收数据，即便应用切换至操作系统前台时。使用 WebSocket 服务的应用在移动至后台时，必须明确指出请求的状态。（幸运的是，LeapJS 库帮你管理了前后台的过渡。）

你可以使用 `Controller.set_policy()` 来告诉控制器当你的应用处于后台时依然能够接受数据。设置 BACKGROUND_POLICY_FLAG 策略可以做到。另外， LeapMotion 控制面板中的*允许后台程序应用*必须被勾选，企图改变这个策略会被拒绝。

```python
controller.set_policy(Leap.Controller.POLICY_BACKGROUND_FRAMES)
controller.set_policy(Leap.Controller.POLICY_IMAGES)
controller.set_policy(Leap.Controller.POLICY_OPTIMIZE_HMD)
```

## 访问图像

为了让你的应用接受从 LeapMotion 相机所发来的图像，你必须设置`Images`策略。LeapMotion 控制面板中的`允许图像`设置必须被启用，企图设置策略会被拒绝。见[相机图像](../devguide/Leap_Images.md)。

## 启动手势

要使用内置的手势，你必须在首次使用时使用`Controller.enable_gesture`启用它们。

```python
controller.enable_gesture(Leap.Gesture.TYPE_SWIPE)
```

最好只启用你的应用需要的手势。

## 连接状态

当你撞见一个 Controller 时，对象会试图建立和 LeapMotion 服务/守护进程的连接。当连接成功后，`Controller.isServiceConnected`属性会变成 true。同样的，如果 LeapMotion 被接入并且被服务或守护进程监测到，那么`Controller.is_connected`属性会变为 true。

`is_service_connected()`和`is_connected`属性可以在你的应用运行时改变，你可以在链接状态改变时监视这些值或监听事件的调度。

## 控制器事件监听

`Controller`对象使用了`Listener`机制调度了若干事件。为处理这些事件你可以扩展 Listener 类来实现这些回调函数。`Controller`会在事件发生时，调用相关的回调函数。

这些事件包括：

|回调函数|解释|
|:--:|:--|
|on_connect()|Controller 连接到 LeapMotion 服务/守护进程、或 LeapMotion 硬件时|
|on_device_change()|LeapMotion 硬件状态发生改变时|
|on_disconnect()|Controller 失去 LeapMotion 服务/守护进程、或 LeapMotion 硬件的连接时|
|on_exit()|Controller 对象被销毁时|
|on_focus_gained()|应用程序位于操作系统前台输入和即将开始接受追踪数据时|
|on_focus_lost()|当应用程序失去操作系统后台任务或即将停止接受追踪数（除非设置了 BACKGROUND_FRAMES_POLICY）|
|on_frame()|一个新的 Frame 追踪数据有效时|
|on_init()|Controller 对象被初始化时|
|on_service_connect()|Controller 连接到 LeapMotion 服务或守护进程时|
|on_service_disconnect()|Controller 对象失去LeapMotion 服务或守护进程的连接时|

下面的例子展示了一个包含典型回调函数的 Listener 子类的实现：

```python
import Leap, sys

class LeapEventListener(Leap.Listener):

    def on_connect(self, controller):
        print "Connected"
        controller.enable_gesture(Leap.Gesture.Type.TYPE_SWIPE)
        controller.config.set("Gesture.Swipe.MinLength", 200.0)
        controller.config.save()

    def on_disconnect(self, controller):
        # Note: not dispatched when running in a debugger.
        print "Disconnected"

    def on_frame(self, controller):
        print "Frame available"
        frame = controller.frame()
        #Process frame data
```

你可以将你的 Listener 实现的实例添加给一个控制器：

```python
listener = LeapEventListener
controller = Leap.Controller()
controller.add_listener(listener)
```

每个时间的回调函数都在一个独立的由 LeapMotion 库创建的线程上运行。由库说创建的追踪对象是线程安全的，但是你必须保证其他应用数据在回调函数中能够安全的访问。你可以通过轮换控制器框架进行调度，从而避免多项成应用的一些并发问题。

## 设备类型

目前有三种类型的 LeapMotion 硬件是可用的：作为配件的标准控制器、嵌入到控制器的计算机键盘、嵌入笔记本电脑中的控制器。然而，这些设备非常不同。例如嵌入在笔记本电脑中的控制器是不能拔出的，而是使用键盘上的快捷键决定启用与否。

你可以使用 Device.type 获取设备类型。使用 Controller.Devices 来获得链接的设备列表（当前在同一时间内允许识别获得一个设备）。
