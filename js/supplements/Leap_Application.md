# 使用 LeapMotion 控制面板

这篇文章描述了 LeapMotion 控制面板，你可以使用里面的设置选项来改变 LeapMotion 控制器

## 概观

当 LeapMotion 控制面板运行时，它会显示在 Windows 任务栏或 Mac 通知栏区域，你可以通过它来快速启动 AppHome 应用或其他事情。当 LeapMotion 控制器接入并顺利工作时，图标变成绿色。其他的颜色都表示错误或异常。

* ![](../images/Leap_App_Icon_Unplugged.png) - LeapMotion 未接入(或 LeapMotion 软件还未检测到)
* ![](../images/Leap_App_Icon_Normal.png) - LeapMotion 控制器和软件正常工作
* ![](../images/Leap_App_Icon_Smudge.png) - 检测到 LeapMotion 设备上的脏污或阴影
* ![](../images/Leap_App_Icon_Error.png) - 表示追踪被暂停，因为 LeapMotion 的帧率低于可接受的阈值。USB 带宽之间的竞争是首要的因素。对于这种情况，应该直接将控制器接入计算机，而不是使用 USB 的集线器或延长线，或者拔掉其他的 USB 设备也是可以的。
* ![](../images/Leap_App_Icon_Robust.png) - 表明 LeapMotion 的帧速率低于可接受的阈值，你已经关闭了 LeapMotion 中的一些导致性能下降的选项，继续进行追踪将大大降低可靠性。
* ![](../images/Leap_App_Icon_Updates.png) - 表明软件可以进行更新。

LeapMotion 控制面板还提供了下面一些工具：

* 启动 AppHome - 打开 AppHome 应用
* 设置 - 打开 LeapMotion 控制面板
* Visualizer - 启动 Visualizer 应用
* Pause/Resume 追踪 - 停止/启动 LeapMotion 的追踪数据

## LeapMotion 设置

你可以调整 LeapMotion 控制面板的一些设置来进行诊断，你可以在图标的设置选项来打开控制面板。

## 通用设置

控制面板的通用设置也提供了下面的设置：

勾选允许 WebApp 可以激活 WebSocket 服务器并向他们提供数据（它永阳可以让其他应用连接到 WebSocket 服务，因此关闭这个设置也可能会影响桌面应用程序）。

勾选允许后台应用来激活应用即便在后台运行也能接受追踪数据。

勾选允许图像来激活接受相机图像，如果没有勾选，那么应用会持续接收除了图像以外的数据。

勾选自动节能来激活 LeapMotion 软件降低能耗调整追踪帧率。

勾选自动发送诊断数据来激活 LeapMotion 自动匿名发送诊断数据。

勾选自动交互高度来激活 LeapMotion 自动调整软件交互盒子的高度。

勾选自动更新软件可以自动下载安装软件更新。软件会在重新启动计算机后被安装。勾选安装更新会立即安装更新。

## 追踪设置

勾选鲁棒模式，可以使软件进入“鲁棒追踪模式”，它允许执行红外照明条件下的追踪。

当 LeapMotion 控制器挂载到 VR 设备时，可以勾选上下追踪优化选项。

取消选中工具追踪可以禁用对工具的追踪。

取消选中手追踪可以禁用对手的追踪。

勾选自动定向追踪，可以允许当它检测从相对侧进入所述视场手设备翻转z轴。点击相反方向键来手动翻转轴。

**鲁棒追踪模式**

鲁棒模式提高了在明亮的照明条件下的跟踪数据的可靠性。鲁棒模式允许LeapMotion控制器在更广泛的环境条件下工作;然而，其他性能特性可能会降低。对性能的主要作用是，会出现增加的处理延迟和非常快速的运动由用户将导致跟踪数据的丢失。

当光线条件变得糟糕时，LeapMotion控制器在位置至少30秒后就会自动抛弃鲁棒模式。

## 问题处理

点击显示软件日志来查看 LeapMotion 相关的日志。如果你遇到了问题，我们可能会要求你发送这些日志给 LeapMotion 然后来解决你的问题。你可以保存这些日志的副本。

点击 诊断Visualizer 来打开 Visualizer 应用。
点击校准设备来启动设备校准工具。
点击报告软件问题来打开 bug 报告表单。
点击重置默认设置来恢复 LeapMotion 的原始设置。

取消选中避免性能下降禁用较低的设备帧率检查。当检测到较低的设备帧速率，这样就可以采取纠正措施的帧频检查将暂停跟踪。如果禁用此选项，追踪就不会暂停。 USB带宽问题是低装置的帧速率的最常见的原因，但大部分 CPU 的负载都是没什么问题的，即便是接近或低于我们的最低推荐系统要求的计算机上。

选中低资源模式可以减少Leap Motion控制器和软件使用的CPU和USB带宽。此设置可以减少最大跟踪范围，速度，和准确性，但可能有必要拥塞的USB总线（来自多个USB和蓝牙设备）或评级较低的CPU芯片的计算机上。

点击开始诊断可以执行一系列系统和环境测试。

## 诊断

争端测试包括了一系列的检查，第一轮的测试包括控制器和软件：

* 认证 - 验证控制器的固件版本。如果测试失败，请联系 LeapMotion 支持。
* 设备测试 - 控制器将发送大量数据给 LeapMotion 软件进行检查。
* 软件测试 - LeapMotion 软件会产生大量数据用于检查（这个测试要求你的一只手位于 LeapMotion 视野内）。

第二轮测试会检查一些外部环境因素：

* 检查污点 - 检查设备窗口上的污点，如果失败，请清理这个表面。
* 检查光线条件 - 检查 LeapMotion 控制器内的光线强度。如果测试失败，请考虑移动控制器或耕管广元，如果可能，不要让控制器直接对准光源。

第三轮测试包含一些设备的校准。

点击报告诊断按钮来发送一些 LeapMotion 的测试结果。我们会使用这些信息进行质量控制。

## 校准

如果 LeapMotion 控制器上的传感器被从初始校准移开，那么必须要重新进行校准，这些校准包括：

* 持续的跳动
* 追踪数据中频繁出现不连续
* 追踪数据出现偏差，发生在特定的视野中
* 有限的追踪范围
* 你可以在 Visualizer 中查看这些症状

如果你在一块玻璃或者红外透明材料下面放置你的控制器，我们还建议使用镜子重新进行校准。

对重新校准你的 LeapMotion 控制器可以：

1. 打开 LeapMotion 设置；
2. 选择问题处理页；
3. 点击重新校准设备按钮；
4. 根据听木上的提示来进行校准。

![](../images/Leap_Recalibrate.png)
*你需要一个平坦的反射面，镜面是立项的。但是想显示器这种也是可以接受的。在整个过程中，拿好 LeapMotion 控制器使得 LED灯能够在镜面中反社会设备。标定窗口上户显示一个磁盘，让你干煸当前设备和平面之间的角度来描绘整个窗口。LeapMotion 控制器上下左右进行移动是不会影响校准的，但旋转会。*


## Bug 报告

如果你遇到了 LeapMotion 的硬件或软件问题，我们可以帮你解决。你可以想 LeapMotion 开发者网站提交错误报告。

我们可能会向你询问关于重现这个错误Bug 的问题，比如一些诊断信息、设备信息等。你可以发送这些信息来帮助我们评估这个问题。你可以在 LeapMotion 的 Bug 报告表单启动或停止诊断信息。这些数据会被压缩和加密，而且对你的本地应用调试不会有人呢和帮助。数据会随着时间的增长而变多，所以我们不推荐你启动很长时间。

报告一个 bug：

1. 打开 LeapMotion 设置诊断
2. 选择问题处理页
3. 点击报告软件问题按钮
4. 打开bug 报告表单，选择合适的原因
5. 添加一些重要的细节，比如如何重现你的 bug
6. 对于 bug 的类型你会被要求记录一些诊断信息
7. 完成后，点击发送按钮。你的信息和诊断记录会被发送给 LeapMotion

当你被要求记录诊断信息时，

1. 点击记录按钮
2. 重现问题（启用 Visualizer 会很有帮助）
3. 点击停止按钮
4. 点击发送