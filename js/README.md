# LeapMotion SDK 中文文档 - JavaScript

<div style="text-align: left;">
    <img src="../images/logo.png" style="height: 100px;">
    <img src="../images/javascript-icon.png" style="height: 110px;">
</div>

> 当前文档版本： v2.3

## 目录

* [文档概述(v2.3)](./index.md)
* [骨骼追踪模型概述](./devguide/Intro_Skeleton_API.md)
* [API 综述](./devguide/Leap_Overview.md)
* 设计指南
  - [菜单设计指南](./practices/Leap_Menu_Design_Guidelines.md)
  - [用户导向与教程设计指南](./practices/Leap_Orientation_and_Tutorial_Guidelines.md)
  - TODO: [应用展示与营销指南](./practices/App_Assets_and_Marketing_Guidelines.md)
  - [用户体验设计指南](./practices/Leap_UX_Guidelines.md)
* 应用程序开发
  - [SDK 库](./devguide/Leap_SDK_Overview.md)
  - [快速入门](./devguide/Sample_Tutorial.md)
  - [项目设置](./devguide/Project_Setup.md)
  - [系统架构](./devguide/Leap_Architecture.md)
  - [运行时配置](./devguide/Leap_Configuration.md)
* 使用追踪 API
  - [连接到控制器](./devguide/Leap_Controllers.md)
  - [追踪模型](./devguide/Leap_Tracking.md)
  - [帧](./devguide/Leap_Frames.md)
  - [手](./devguide/Leap_Hand.md)
  - [手指](./devguide/Leap_Pointables.md)
  - [手势](./devguide/Leap_Gestures.md)
  - [触摸仿真](./devguide/Leap_Touch_Emulation.md)
  - [运动](./devguide/Leap_Motions.md)
  - [坐标系统](./devguide/Leap_Coordinate_Mapping.md)
  - [相机图像](./devguide/Leap_Images.md)
  - [序列化追踪数据](./devguide/Leap_Serialization.md)
* TODO: [LeapJS 插件](./devguide/Leap_JS.md)
* API 参考
  - TODO: [Leap namespace](./api/Leap.Classes.md)
  - TODO: [Bone](./api/Leap.Bone.md)
  - TODO: [CircleGesture](./api/Leap.CircleGesture.md)
  - TODO: [Controller](./api/Leap.Controller.md)
  - TODO: [Finger](./api/Leap.Finger.md)
  - TODO: [Frame](./api/Leap.Frame.md)
  - TODO: [Gesture](./api/Leap.Gesture.md)
  - TODO: [Hand](./api/Leap.Hand.md)
  - TODO: [InteractionBox](./api/Leap.InteractionBox.md)
  - TODO [KeyTapGesture](./api/Leap.KeyTapGesture.md)
  - TODO: [Pointable](./api/Leap.Pointable.md)
  - TODO: [ScreenTapGesture](./api/Leap.ScreenTapGesture.md)
  - TODO: [SwipeGesture](./api/Leap.SwipeGesture.md)
  - TODO: [Matrix](./api/Leap.Matrix.md)
  - TODO: [Vector](./api/Leap.Vector.md)
* 附录
  - [Leap Motion Release Notes](https://developer.leapmotion.com/documentation/python/supplements/SDK_Release_Notes.html) 
  - [使用 LeapMotion 控制面板](./supplements/Leap_Application.md)
  - [使用可视化诊断工具](./supplements/Leap_Visualizer.md)
  - [WebSocket 通信](./supplements/Leap_JSON.md)
  - [鸣谢](./supplements/Leap_Acknowledgements.md)

## 许可
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">LeapMotion SDK 中文文档 - JavaScript</span> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="http://www.changkun.us/pylm-cn/" property="cc:attributionName" rel="cc:attributionURL">欧长坤</a> 创作，采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://developer.leapmotion.com/documentation/index.html" rel="dct:source">LeapMotion 官方文档</a>上的作品创作。