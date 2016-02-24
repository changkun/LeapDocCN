# LeapMotion SDK 中文文档 - Python

<div style="text-align: left;">
    <img src="./images/logo.png" style="height: 100px;">
    <img src="./images/python-icon.png" style="height: 110px;">
</div>

> 当前文档版本： v2.3

## 目录

* [文档概述(v2.3)](./index.md)
* [骨骼追踪模型概述](./devguide/Intro_Skeleton_API.md)
* [API 综述](./devguide/Leap_Overview.md)
* 设计指南
  - [菜单设计指南](./practices/Leap_Menu_Design_Guidelines.md)
  - [用户导向与教程设计指南](./practices/Leap_Orientation_and_Tutorial_Guidelines.md)
  - [应用资产与营销指南](./practices/App_Assets_and_Marketing_Guidelines.md)
  - [用户体验设计指南](./practices/Leap_UX_Guidelines.md)
* 应用程序开发
  - [SDK 库](./devguide/Leap_SDK_Overview.md)
  - [快速入门](./devguide/Sample_Tutorial.md)
  - [项目设置](./devguide/Project_Setup.md)
  - [系统架构](./devguide/Leap_Architecture.md)
  - [运行时配置](./devguide/Leap_Configuration.md)
* 使用追踪 API
  - Connecting to the Controller
  - [追踪模型](./devguide/Leap_Tracking.md)
  - [帧](./devguide/Leap_Frames.md)
  - [手](./devguide/Leap_Hand.md)
  - [手指](./devguide/Leap_Pointables.md)
  - Gestures
  - Touch Emulation
  - [运动](./devguide/Leap_Motions.md)
  - Coordinate Systems
  - Camera Images
  - Serializing Tracking Data
* API 参考
  - [Arm](./api/Leap.Arm.md)
  - [Bone](./api/Leap.Bone.md)
  - [CircleGesture](./api/Leap.CircleGesture.md)
  - [Config](./api/Leap.Config.md)
  - Controller
  - Device
  - [DeviceList](./api/Leap.DeviceList.md)
  - Finger
  - FingerList
  - Frame
  - Gesture
  - GestureList
  - Hand
  - HandList
  - Image
  - [ImageList](./api/Leap.ImageList.md)
  - InteractionBox
  - KeyTapGesture
  - Listener
  - Matrix
  - Pointable
  - PointableList
  - ScreenTapGesture
  - SwipeGesture
  - [Tool](./api/Leap.Tool.md)
  - [ToolList](./api/Leap.ToolList.md)
  - Vector
* 附录
  - [Leap Motion Release Notes](./supplements/SDK_Release_Notes.md) 
  - [使用 LeapMotion 控制面板](./supplements/Leap_Application.md)
  - [使用诊断可视化工具](./supplements/Leap_Visualizer.md)
  - [WebSocket 通信](./supplements/Leap_JSON.md)
  - [鸣谢](./supplements/Leap_Acknowledgements.md)

## 开源协议
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">LeapMotion SDK 中文文档 - Python</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="http://www.changkun.us/pylm-cn/" property="cc:attributionName" rel="cc:attributionURL">欧长坤</a> 创作，采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://developer.leapmotion.com/documentation/python/index.html" rel="dct:source">LeapMotion 官方 Python 文档</a>上的作品创作。