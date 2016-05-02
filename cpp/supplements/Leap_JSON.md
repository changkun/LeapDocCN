# WebSocket 通信

任何安装在了 LeapMotion 的计算机上都有一个 WebSocket 服务器。这个 WebSocket 服务器监听了本地 6347 端口（http://127.0.0.1:6437）。任何客户端程序，包括 Web 客户端，都能够通过建立 WebSocket 链接来访问 LeapMotion 的 JSON 格式的追踪数据消息。WebSocket 服务由 `leapd` 进程提供，作为服务运行在 Windows 中，而作为守护进程运行在 OSX 和 Linux 中

大部分情况下，你应该使用已经有的客户端库而不是在你的应用中直接使用这个协议。如果你在开发自己的库，那么这篇文章会对你有帮助。现有的库有：

* [`leap.js`](https://github.com/leapmotion/leapjs) - JavaScript 客户端库，支持浏览器和 NodeJS。
* [LeapMotionAS3](https://github.com/logotype/LeapMotionAS3) - 对 AdobeFlash 和 AIR 提供支持的 ActionScript 客户端库。


## 协议

WebSocket 的服务器和客户端之间的通信是通过数据交换子协议介导的。此子协议定义了消息可以在客户端和服务器和JSON数据的格式之间发送。其特色在于设置服务器的协议版本定义使用与客户进行沟通。

你可以通过在 URL 中添加类似`v6.json`的格式来请求特定版本的 LeapMotion 子协议，其中的数字6表示的表示的是使用的版本。如果省略了URL 的这个部分，那么你会得到1.0版本的数据。注意，leap.js JavaScript库会自动选择相应的库版本的协议版本。当您成功连接到 LeapMotion 的 WebSocket  服务器，他会通过一条消息来报告的协议版本。如果客户端的LeapMotion软件版本太旧，那么请求的版本可能会小于你需要的版本。

该协议的当前版本是v6.json。

## 客户端服务端消息

WebSocket 服务器和一个客户端会交换下面的消息：

* 服务端到客户端

**version**

指定当前 LeapMotion 服务和 WebSocket 子协议的版本：

```json
{"serviceVersion":"2.3.1+33747", "version":6}
```

**deviceEvent**

当 LeapMotion 的服务或守护进程暂停时，亦或者当控制器硬件接入或者拔出时：

```json
{
  "event": {
    "state": {
      "attached": false,
      "id": "NNNNNNNNNNN",
      "streaming": false,
      "type": "peripheral"
    },
    "type": "deviceEvent"
  }
}
```

| | |
|:--:|:--:|
|id|LeapMotion的设备 ID|
|attached|LeapMotion 硬件是否接入|
|streaming|服务或守护进程是否在发送追踪数据，当 attached 为 fasle 的时候总是fasle|
|type|硬件类型，比如『外设』『键盘』『笔记本电脑』|

**Tracking data**
包含了全部的追踪数据，见下。

* 客户端到服务端

**background**

指定客户端是否要接收帧时，它不是焦点的应用程序：

```json
{"background": true}
{"background": false}
```

**focused**

指定应用程序是否处于活动状态。`focused`设置为 true 时，阻止其他的 WebSocket 客户端获取数据。`focused`设置为 false ，从获取数据（和可能不需要输入）停止你的WebSocket客户端：

```json
{"focused": true}
{"focused": false}
```

**enableGestures**

启用或地址手势识别：

```json
{"enableGestures": true}
{"enableGestures": false}
```

**optimizeHMD**

指定客户端硬件是否介入了头戴显示器：

```json
{"optimizeHMD": true}
{"optimizeHMD": false}
```

向 WebSocket 服务器发送消息，首先必须将消息编码为JSON 字符串。在 JavaScript 中，你可以使用 `stringify()`函数封装消息，并使用 WebSocket 中的`send()`函数。

```
//ws 是一个连接的 WebSocket 对象
var backgroundMessage = JSON.stringify({background: true});
ws.send(backgroundMessage);
```

## JSON 追踪数据格式

从 WebSocket 服务器发来的数据的每一帧都包含一个由 JSON 定义的帧数据。JSON 消息中的每一帧的属性都很相似，但和本地库中的 `Frame` 对象包含的内容也不一样，JSON 数据内容包括：

```json
"currentFrameRate": float
"id": float
"r": array of floats (Matrix)
"s": float
"t":  array of floats (vector)
"timestamp": integer
"devices": 未实现 (总是一个空数组)

"gestures": Gesture 对象数组
    (通过手势类型表示的属性)
    "center": float 数组 (vector) -- 仅限于 Circle 手势时才存在
    "direction": float 数组 (vector) -- 仅限于 Swipe, keyTap, screenTap 手势时才存在
    "duration": integer 毫秒
    "handIds":  integer 数组
    "id": integer
    "normal": float 数组 -- 仅限于 Circle 手势时才存在
    "pointableIds": array
    "position": float 数组 (vector) -- 仅限于 Swipe, keyTap, ScreenTap 手势时才存在
    "progress": float -- 仅限于 Circle, KeyTap, ScreenTap 时才存在
    "radius": float -- 仅限于 Circle  手势时才存在
    "speed": float -- 仅限于 Swipe 手势时才存在
    "startPosition": float 数组 (vector) -- 仅限于 Swipe 手势时才存在
    "state": string -"start", "update", "stop" 中的一个
    "type": string - "circle", "swipe", "keyTap", "screenTap" 中的一个

"hands":  Hand 对象数组
   "armBasis: 手臂的三个基向量(vector 数组)
   "armWidth: float
   "confidence: float
   "direction": float 数组 (vector)
   "elbow: float 数组 (vector)
   "grabStrength: float
   "id": integer
   "palmNormal": float 数组 (vector)
   "palmPosition": float 数组 (vector)
   "palmVelocity": float 数组 (vector)
   "pinchStrength: float
   "r": float 数组 (Matrix)
   "s": float
   "sphereCenter": float 数组 (vector)
   "sphereRadius": float
   "stabilizedPalmPosition": float 数组 (vector)
   "t": float 数组 (vector)
   "timeVisible": float
   "type": string - "right", "left" 中的一个
   "wrist: float 数组 (vector)

"interactionBox": object
   "center": float 数组 (vector)
   "size": float 数组  (vector)

"pointables": array of Pointable objects
   "bases":  每块骨头的三个基向量, 按索引顺序, 从 wrist 到 tip (array of vectors).
   "btipPosition":distal phalanx (第三指节骨)尖端的位置，包含三个浮点数的数组
   "carpPosition":metacarpal bone (掌骨)的位置，包含三个浮点数的数组
   "dipPosition:"  distal phalanx (第三指节骨)的位置，包含三个浮点数的数组.
   "direction": array of floats (vector)
   "extended": boolean (true or false)
   "handId": integer
   "id": integer
   "length": float
   "mcpPosition": 位置向量，包含三个浮点数的数组
   "pipPosition": 位置向量，包含三个浮点数的数组
   "stabilizedTipPosition": float 数组 (vector)
   "timeVisible": float
   "tipPosition":  float 数组 (vector)
   "tipVelocity":  float 数组 (vector)
   "tool": boolean (true 或 false)
   "touchDistance": float
   "touchZone": string - "none", "hovering", "touching" 中的一个
   "type": integer - 0 表示拇指; 4 表示小指(pinky finger)
   "width": float
```

注意：

* 如果手势识别通过发送 enableGestures 消息到的 WebSocket 服务器启用姿势数据仅包含在数据的一帧。
* Hand.basis 由 `palmNormal` 和 `direction` 向量计算而来，它不包括在JSON数据。

## 运动因子

r, s, t 是 Hand 和 Frame 对象上的运动因子，他们是运动发生在帧之间的快照。这些因素必须与前一帧相结合才能导出相对运动。

* r - 3x3 旋转矩阵
* s - 缩放因子
* t - 3 个元素的平移向量

**旋转因子**

两个帧之间的相对旋转矩阵，可以由计算当前帧的 r 矩阵乘以起始帧的 r 矩阵的逆矩阵。

```
rotation = r_{currentframe} * r_{sinceframe}^{-1}
```

**缩放因子**

相对缩放因子可以由当前帧和起始帧差的指数函数的结果计算得来。

```
scalefactor = \exp{s_{currentframe}-s_{sinceframe}}
```

**平移因子**

相对平移因子可以由当前帧的平移因子起始帧的平移因子。

```
\overrightarrow{translation} = \overrightarrow{t_{currentframe}} - \overrightarrow{t_{sinceframe}}
```

## 协议变化

这篇文档描述了协议最近的变化。

每个版本的协议对应于特定安装版本的 LeapMotion 软件以及leap.js 库的版本：

|协议|LeapMotion 客户端软件|Leap.js|
|:--:|:--:|:--:|
|v1.json|prerelease|0.1.n|
|v2.json|prerelease|0.2.n|
|v3.json|1.0+|0.3.n|
|v4.json|1.0.9+|0.4.n|
|v5.json|1.2.0+|0.5.n|
|v6.json|2.0+|0.6.n|

### v6

* 增加了 LeapMotion v2 的附属数据和骨骼追踪模型：
* Hand.confidence
* Hand.grabStrength
* Hand.pinchStrength
* Hand.type
* Pointable.dipPosition
* Pointable.extended
* Pointable.mcpPosition
* Pointable.pipPosition
* Pointable.type
* 为手指增加了 Pointable.width
* 增加了 optimizeHMD 的客户端到服务端消息

### v5
增加了 deviceEvent 消息
去除了 deviceEvent 的 deviceConnected 消息

### v4
增加了 focused 和 background 消息
移除了 heartbeat 消息。支持v4以上的服务器会忽略 heartbeat 消息，及时他们连接了v2或v3

### v3
增加了 deviceConnected 事件

### v2
 增加了 heartbeat 消息。如果你的应用程序支持 v2或v3，你应该每 100ms 就发送一次 heartbeat 消息。如果这段时间内服务器没有收到 hearbeat 消息，那么他会假设客户端处于非活动状态并停止发送数据，知道收到新的心跳数据。heartbeat 已经在 v4 以后的版本中被移除。