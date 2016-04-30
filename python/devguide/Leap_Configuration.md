# 运行时配置

LeapMotion 系统在配置文件中存储了很多选项。其中包括大部分 LeapMotion 控制面板中用户可设置的选项，业务控制设置以及功能控制设置。这些选项可以在运行 LeapMotion 服务/守护进程时作为命令行选项，通过修改一个 JSON 格式的配置文件，或使用 Config 类在运行时进行设置。

**重要说明**：这些设置会影响所有正在运行的支持 Leap 的程序，而不仅仅只针对你的程序。在你自己的电脑上修改设置时要小心，因为这些修改可能在你用户的电脑上不能轻易做到。


## 追踪控制设置

追踪设置可以控制供给应用程序的有效的追踪数据。

* `tracking_hand_enabled`: boolean
激活或关闭手部的追踪。注意，任何在视野中已经被手都能够被持续被追踪，如果关闭手部的追踪，那么将会持续到它们从视野中被移除，而任何新增加的手都不会被追踪。

从这个设置可以由用户控制后，你应该询问是否有更改这个设置值的权限：

```python
isHandTrackingEnabled = controller.config.get("tracking_hand_enabled");
if not isHandTrackingEnabled:
    # Show dialog to request permission to turn on hand tracking
    if permissionGranted:
        controller.config.set("tracking_hand_enabled", true);
        controller.config.save();
```

* `tracking_tool_enabled`: boolean
激活或关闭对工具的追踪。

自从这个设置可以由用户控制后，你应该询问是否具有改变这个设置值的权限：

```python
isToolTrackingEnabled = controller.config.get("tracking_tool_enabled");
if not isToolTrackingEnabled:
    # Show dialog to request permission to turn on tool tracking
    if permissionGranted:
        controller.config.set("tracking_tool_enabled", true);
        controller.config.save();
```

* `images_mode`: integer

激活或关闭图像模式。设置为0可以关闭图像；设置为2可以开启图像。

自从这个值可以由用户控制后，你应该询问是否具有改变这个值的权限。

注意，应用程序依然需要在运行时中调用图像代理 API获得图像数据。简单的在Leap服务中开启图像模式是不够的。

```python
areImagesEnabled = controller.config.get("tracking_images_mode") == 2;
if not areImagesEnabled:
    # Show dialog to request permission to turn on images
    if permissionGranted:
        controller.config.set("tracking_images_mode", 2);
        controller.config.save();
```

* `image_processing_auto_flip`: boolean
启动时，LeapMotion 设备可以同时将有绿色 LED 灯朝下或朝向远离用户方向进行使用。这个服务检测定位和翻转设备的图像。关闭时，图像永远不会进行翻转，且对于手部的识别必须当绿色 LED 灯所在一侧的设备朝向用户（或连接 HMD 设备朝下）时才能使用。

自从这个值可以由用户控制后，你应该询问是否具有改变这个值的权限。

```python
# read
autoFlip = controller.config.get("tracking_processing_auto_flip");

# write
controller.config.set("tracking_processing_auto_flip", false);
controller.config.save();
```

## 服务控制设置

服务控制设备能够改变 LeapMotion 服务或进程的操作。

* `robust_mode_enabled`: boolean

鲁棒模式下能够向外界提供充足的 IR 光线。然而它依然会显著低于帧率。如果帧率太低，关闭鲁棒模式能够可能导致较差的追踪性能。

鲁棒模式能够在控制面板中开启并设置`robust_mode_enabled`配置参数。当启动时，系统会在当 IR 光线被检测到时开启鲁棒模式。

```python
# read
robustMode = controller.config.get("robust_mode_enabled");

# write
controller.config.set("robust_mode_enabled", false);
controller.config.save();
```

自从这个值可以由用户控制后，你应该询问是否具有改变这个值的权限。

* `avoid_poor_performance`: boolean

自从这个值可以由用户控制后，你应该询问是否具有改变这个值的权限。

```python
# read
avoidPoorPerformance = controller.config.get("avoid_poor_performance");

# write
controller.config.set("avoid_poor_performance", false);
controller.config.save();
```

* `background_app_mode`: integer

决定应用程序能够在后台任务中收到追踪数据。

自从这个值可以由用户控制后，你应该询问是否具有改变这个值的权限。

```python
backgroundModeAllowed = controller.config.get("background_app_mode") == 2;
if not backgroundModeAllowed:
    # Show dialog to request permission to allow background mode apps
    if permissionGranted:
        controller.config.set("background_app_mode", 2);
        controller.config.save();
```

* `cpu_affinity_mask`: integer

处理器关联会在多核系统上控制进程在某个 CPU 核心在运行。你可以使用`cpu_affinity_mask`配置参数来控制 LeapMotion 服务的处理器关联。这个参数需要一个整数值转换为位掩码，用于指定由哪个 CPU 核心来运行服务（例如，3的二进制表示为0011，将指定核心运行在核心1和核心2上）。值为0时表示使用 OS 默认行为。

这个掩码会被传递给 Windows SetProcessorAffinityMask() API。所以这个参数不支持其他操作系统。

改变这个值后会重启当前服务。一般来说，使用 LeapSvc 命令或在 JSON 文件中配置这个值更有意义。

```json
{
  "configuration": {
    "cpu_affinity_mask": 1,
    "process_niceness": 6
  }
}
```

* `process_niceness`: integer

线程优先级控制了引起 LeapMotion 服务的线程优先级。线程优先级由`process_niceness`配置参数进行控制。指定 0 表示 分配 OS 的默认优先级；可以分配从 1~9 的特定优先级（1=最低，9=最高）

改变这个值后会重启当前服务。一般来说，使用 LeapSvc 命令或在 JSON 文件中配置这个值更有意义。这个设置只在 Windows 中有效。

* `no_cp_startup`: boolean

决定了 LeapMotion 的控制面板是否会在计算机启动时自动启动。设置为 true 时候不会被自动启动，false（默认值）来允许自动启动。

```
# read
controlPanelOnStartup = controller.config.get("no_cp_startup");

# write
controller.config.set("no_cp_startup", false);
controller.config.save();
```

* `auto_check_updates`: boolean

决定了 LeapMotion 服务是否会自动进行软件更新。

自从这个设置可以由用户进行控制，你应该在改变这个设置之前检查是否具有修改权限。

```
# read
autoUpdateCheck = controller.config.get("auto_check_updates");

# write
controller.config.set("auto_check_updates", false);
controller.config.save();
```

* `auto_install_updates`: boolean

决定了 LeapMotion 服务是否会自动更新软件。只有当`auto_check_updates`设置被设置为 true 时才能有效。

```
# read
autoInstallUpdates = controller.config.get("auto_install_updates");

# write
controller.config.set("auto_install_updates", false);
controller.config.save();
```

* `show_tray_messages`: boolean

允许通知区域消息在服务或守护进程图表中显示。设置为 true 时表示允许（默认值）；false 为阻止消息。

这个设置只能在你控制的电脑上进行使用。

```
# read
showNotifications = controller.config.get("show_tray_messages");

# write
controller.config.set("show_tray_messages", false);
controller.config.save();
```

* `metrics_enabled`: boolean

允许使用公制度量。

这个设置只能在你控制的计算机上使用。

```
# read
enableMetrics = controller.config.get("metrics_enabled");

# write
controller.config.set("metrics_enabled", false);
controller.config.save();
```

## 节能选项

节能选项包括了控制面盘节能选项和低资源模式的设置。节能模式在电脑运行在电池下时会自动开启，但也可以通过参数进行配置。
节能模式的配置参数如下：

* `power_saving_adapter`: boolean

限制帧率进行节能，即使电脑接通电源。

```
# read
acPowerSaver = controller.config.get("power_saving_adapter");

# write
controller.config.set("power_saving_adapter", false);
controller.config.save();
```

* `power_saving_battery`: boolean

当电脑运行在电池驱动下时，限制帧率来节约能源。

```
# read
batteryPowerSaver = controller.config.get("power_saving_battery");

# write
controller.config.set("power_saving_battery", false);
controller.config.save();
```

* `low_resource_mode_enabled`: boolean

限制帧率以降低 USB 带宽。

```
# read
lowResourceMode = controller.config.get("low_resource_mode_enabled");

# write
controller.config.set("low_resource_mode_enabled", false);
controller.config.save();
```

当设置`false`时，禁用这些选项；当设置为`true`时开启它们。

这些设置不会叠加。当你同时开启了两种节能模式和低资源模式时，那么由此产生的帧率为所设置的最小值。

节能模式的设置参数会在图像模式被开启时失效。（低资源模式下依然有效。）

## WebSocket 选项

WebSocket 的选项控制程序如何能连接到 LeapMotion 提供的 WebSocket 服务。

**重要**：如果你修改了这些值，那些期望使用默认 WebSocket 设置的程序将会连接失败。

|键值|值类型|默认值|用途|
|:-:|:-:|:-:|:-:|
|websockets_enabled|布尔值|true|启用或禁用所有连接|
| websockets\_allow\_remote |布尔值|false|允许非本地客户端链接|
|ws_port|整数|6437|用于 HTTP 客户端|
|wss_port|整数|6436|用户 HTTPS 客户端|

注意，修改端口号只有在 LeapMotion 服务或守护进程重启时才能生效。一般情况下，在命令行或者 config.json 文件中设置这些值会更有意义：

```json
{
  "configuration": {
    "websockets_enabled": true,
    "websockets_allow_remote": false,
    "ws_port": 51000,
    "wss_port": 51001
  }
}
```

## 功能控制设置
两套配置设置控制了独立追踪功能如何运作的。

### InteractionBox 选项

Interaction Box 选项使用 InteractionBox 类来计算坐标中交互盒子的位置和大小。

|键值|值类型|默认值|功能|
|:-:|:--|:--|:--|
|`interaction_box_auto`|boolean|true|基于用户的手设置高度|
|`interaction_box_height`|integer|200mm|当前高度设置|
|`interaction_box_scale`|float|0.8|变换盒子的尺寸|

高度参数设置了LeapMotion 设备上方的交互区域的高度。盒子的大小最大化到交互区域的边界上。你可以在 Visulizer 中双击 L 键进行查看。

注意，在2.2.5以上的版本中存在一个 Bug，会阻止手动设置交互盒子的高度。高度只有在`interaction_box_auto`有效时，在响应用户手的移动时才能被改变。

自从`interaction_box_auto`和`interaction_box_height`设置能够被用户设置，你应该检查是否有修改这个值的权限。

更多信息请参考：[InteractionBox](../api/Leap.InteractionBox.md) 和 [坐标系统](../devguide/Leap_Coordinate_Mapping.md)

### 手势选项

手势选项可以调整 LeapMotion 内置的手势检测参数。这些参数的默认值的设置不仅让手势的检测变得简单，且不会引发很多错误的手势。如果你要使用全部的手势，你可能不能改进默认值，请精良在不同的应用程序之间使用不同的交互设计。相反的，如果你只是用一个或两个手势，那么你可以很好的调整调整这些参数来满足你的交互，因为这时触发这些检测算法之间的互相『碰撞』的几率会小很多。尤其是两个点按手势对于用户执行的可靠性会变得非常糟糕。如果你能够在特定的时间或地插你限制点击手势的执行（以一种直观的方式展现给用户），那么你可以考虑激活他们——在没有使用意外的情况下。

|键值|值类型|默认值|单位|
|:--|:--|:--|:--|
|`Gesture.Circle.MinRadius`|float|5.0|mm|
|`Gesture.Circle.MinArc`|float|1.5 * pi|弧度|
|`Gesture.Swipe.MinLength`|float|150|mm|
|`Gesture.Swipe.MinVelocity`|float|1000|mm/s|
|`Gesture.KeyTap.MinDownVelocity`|float|50|mm/s|
|`Gesture.KeyTap.HistorySeconds`|float|0.1s|
|`Gesture.KeyTap.MinDistance`|float|5.0|mm|
|`Gesture.ScreenTap.MinForwardVelocity`|float|50|mm/s|
|`Gesture.ScreenTap.HistorySeconds`|float|0.1|s|
|`Gesture.ScreenTap.MinDistance`|float|3.0|mm|



## 设置配置选项

### 使用命令行
在命令行中设置配置参数，可以在窗口中运行 LeapSvc，具体说明如下：

* Windows:
  - LeapSvc --option_name=value --another_option=value
* Mac/Linux:
  - leapd --option_name=value --another_option=value

通常 LeapSvc 或 leapd 会作为服务或守护进程被自动安装。在手动运行 LeapSvc 之前，你必须将已经运行的服务停止。你可以标准的 Windows 网络命令中（使用管理员账户）：

* Windows
  - net stop LeapService
* Mac
  - sudo launchctl unload /Library/LaunchDaemons/com.leapmotion.leapd.plist
* Linux:
  - sudo service leapd stop

作为例子，下面的命令开启了手部追踪和图像的传送：

* Windows
  - LeapSvc –tracking_hand_enabled=true –images_mode=2
* Mac/Linux
  - leapd –tracking_hand_enabled=true –images_mode=2

**重要**：命令行配置设置会在 LeapMotion 控制板已经运行时被忽略。

### 使用配置文件
你可以向一个 JSON 格式的配置文件中添加选项。你可以使用 LeapSvc 命令中的 `--config` 参数进行指定到文件，也可以手动将你的选项写到标准文件中。

配置文件必须是有效的 JSON，一个配置文件指定的选项类似于下面所示：

```json
{
  "configuration": {
    "cpu_affinity_mask": 3,
    "images_mode": 2,
    "power_saving_adapter": false,
    "power_saving_battery": false,
    "process_niceness": 5,
    "robust_mode_enabled": false,
    "tracking_hand_enabled": true
  }
}
```

在命令行中，你可以按下面的样子进行配置：

```bash
LeapSvc –config=/path/to/config.json
leapd –config=/path/to/config.json
```

LeapMotion 系统保留了两种不同的标准 JSON 配置文件，一个用户服务或守护进程，另一个这用户 LeapMotion 的控制面板程序。当两个服务和控制面板正在运行时，会共享设置并保持同步。否则，则控制面板的设置优先。换句话说，如果控制面板启动时，服务或守护进程已经运行，那么设置将会被更新，以匹配控制面板文件中的设置；如果当服务或守护进程启动时，控制面板已经运行，那么控制面板的设置依然会优先于任何配置文件，甚至命令行的设置。

编辑这些设置文件当服务/守护进程或控制面板运行时不会改变当前运行时设置。我们推荐你退出控制面板，并关闭服务及守护进程后再修改这些设置。

配置文件的名字是 `config.json` 它能够在下面的路径中被找到：

|OS|控制面板配置路径|服务/守护进程配置路径|
|:-:|:--|:--|
|Android|/sdcard/user/Leap\ Motion|/sdcard/Leap\ Motion|
|Linux|$HOME/Leap\ Motion|/var/Leap\ Motion|
|OS X|$HOME/Library/Application\ Support/Leap\ Motion|/Library/Application\ Support/Leap\ Motion|
|Windows|%AppData%/Leap Motion|%ProgramData%/Leap Motion|

注意，其中一些文件夹可能会是隐藏文件夹。