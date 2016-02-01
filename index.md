# Python 文档（v2.3）
此版本的 SDK 变化情况请参考：[Leap Motion Release Notes]()。

## 首先
为了帮助你开始使用 Leap Motion API 进行编程，接下来的文章将提供一个 LeapMotion 所跟踪数据的概述、LeapMotion 的硬件和软件如何工作、以及如何将 SDK 设置在项目中：

* [API 综述](devguide/Leap_Overview.md)
* [系统架构](devguide/Leap_Architecture.md)
* [设置项目](devguide/Project_Setup.md)

并且，作为 LeapMotion API 的最快介绍，下面的内容是非常重要的：

* [Hello World](devguide/Sample_Tutorial.md)

## 最佳实践
一旦你有一个你能做到的好想法，那么花点时间考虑你应该做些什么，下面的文章会有帮助：

* [VR 最佳实践指南 (PDF)](https://developer.leapmotion.com/assets/Leap%20Motion%20VR%20Best%20Practices%20Guidelines.pdf)
* [手势控制引导](https://developer.leapmotion.com/articles/intro-to-motion-control)
* [设计直观的应用程序](https://developer.leapmotion.com/articles/designing-intuitive-applications)
* [菜单设计指南](practices/Leap_Menu_Design_Guidelines.md)
* [User Orientation and Tutorial Guidelines](practices/Leap_Orientation_and_Tutorial_Guidelines.md)
* [Application Asset and Marketing Guidelines](practices/App_Assets_and_Marketing_Guidelines.md)
* [用户体验设计指南](practices/Leap_UX_Guidelines.md)

## 深入主题
作为 LeapMotion API 的深度讨论，请参考下面的文章：

* [连接控制器](devguide/Leap_Controllers.md)
* [跟踪模型](devguide/Leap_Tracking.md)
* [帧(Frames)](devguide/Leap_Frames.md)
* [手(Hands)](devguide/Leap_Hand.md)
* [手指(Fingers)](devguide/Leap_Pointables.md)
* [手势(Gestures)](devguide/Leap_Gestures.md)
* [模拟触摸](devguide/Leap_Touch_Emulation.md)
* [动作(Motions)](devguide/Leap_Motions.md)
* [坐标系统](devguide/Leap_Coordinate_Mapping.md)
* [摄像头图像](devguide/Leap_Images.md)
* [序列化跟踪数据](devguide/Leap_Serialization.md)

## API 参考

||||
|:-:|:-:|:-:|
|[Arm (手臂)](api/Leap.Arm.md)| Frame (帧)| Listener (监听器)|
|骨骼（Bone）|手势（Gesture）|矩阵（Matrix）|
|圈型手势（CircleGesture）|手势序列（GestureList）|可定向（Pointable）|
|配置（Config）|手（Hand）|可定向序列（PointableList）|
|控制器（Controller）|手序列（HandList）|屏幕触摸手势（ScreenTapGesture）|
|设备（Device）|图像（Image）|滑动手势（SwipeGesture）|
|设备序列（DeviceList）|图像序列（ImageList）|工具（Tool）|
|Finger|交互空间（InteractionBox）|工具列表（ToolList）|
|手指序列（FingerList）|按键手势（KeyTapGesture）|向量（Vector）|

## 附录

* [Leap Motion Release Notes](supplements/SDK_Release_Notes.md) 
  - 最新版的 LeapMotion SDK 和 API 的变化。
* [使用 LeapMotion 控制面板](supplements/Leap_Application.md)
  - 关于 LeapMotion 本身的控制面板介绍。
* [使用诊断可视化工具](supplements/Leap_Visualizer.md)
  - 关于诊断可视化工具的介绍。
* [WebSocket 通信](supplements/Leap_JSON.md)
  - 对 WebSocket 的服务器和用于提供 JSON 格式追踪数据的子协议介绍。
* [感谢](supplements/Leap_Acknowledgements.md)
  - 关于本文档。
