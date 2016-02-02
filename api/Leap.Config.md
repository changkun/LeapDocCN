# Config

方法：

* get()
* set()
* save()

## ***class*** **Leap.Config**
Config(配置) 类提能够访问 LeapMotion 配置系统信息。

你面向一个连接的 Controller 对象使用 Config 对象可以设置手势的参数（`Controller.config`）。标识一个配置参数所需的字符串键值包括：

<!--class Leap.Config
The Config class provides access to Leap Motion system configuration information.

You can get and set gesture configuration parameters using the Config object obtained from a connected Controller object (Controller.config). The key strings required to identify a configuration parameter include:-->

|键值|类型|默认值|单位|
|:--|:--|:--|:--|
|Gesture.Circle.MinRadius|float|5.0|mm|
|Gesture.Circle.MinArc|float|1.5 * pi|radians|
|Gesture.Swipe.MinLength|float|150|mm|
|Gesture.Swipe.MinVelocity|float|100|mm/s|
|Gesture.KeyTap.MinDownVelocity|float|50|mm/s|
|Gesture.KeyTap.HistorySeconds|float|0.1|s|
|Gesture.KeyTap.MinDistance|float|3.0|mm|
|Gesture.ScreenTap.MinForwardVelocity|float|50|mm/s|
|Gesture.ScreenTap.HistorySeconds|float|0.1|s|
|Gesture.ScreenTap.MinDistance|float|5.0|mm|
|head\_mounted\_display\_mode|boolean|false|n/a|

设置值之后，你必须调用 `save()` 方法来提交这些修改。你可以在 `Controller` 连接到 LeapMotion 设备和后台后再调用`save()`方法。换句话说，在`serviceConnected` 或 `connected` 事件或者 `Controller.isConnected` 为 `true`之后为`Controller`设置其配置。配置的值并不是持久的，你的应用应该在每次运行的时候都进行这样的设置。

注意：`head_mounted_display_model`是一个临时设置，它通知 LeapMotion 软件手的视野被调整到了手的背面。从长远考虑，我们希望软件能够自动的处理两种情况而不是使用一个标志。它也可以从 LeapMotion 的控制面板进行设置。

<!--After setting a configuration value, you must call the save() method to commit the changes. You can call save() after the Controller has connected to the Leap Motion service/daemon. In other words, after the Controller has dispatched the serviceConnected or connected events or Controller.isConnected is true. The configuration value changes are not persistent; your application needs to set the values everytime it runs.

Note: “head_mounted_display_mode” is a temporary setting that tells the Leap Motion software to expect hands viewed from the top rather than the bottom. In the long run, we expect that the software will handle both automatically without the need for a flag. This setting can also be set from the Leap Motion control panel.-->

进一步阅读：

* [CircleGesture](Leap.CircleGesture.md)
* [KeyTapGesture](Leap.KeyTapGesture.md)
* [ScreenTapGesture](Leap.ScreenTapGesture.md)
* [SwipeGesture](Leap.SwipeGesture.md)

*New in Version 1.0*

----

### 构造函数
*classmethod* **Config()**

构造一个 Config 对象。

不要创建你自己的 Config 对象。你应该从一个连接的控制器中访问一个 Config 对象，参考`Controller.config`。

<!--Constructs a Config object.

Do not create your own Config objects; rather, access the Config object of a connected controller with: Controller.config.-->

```python
config = controller.config
```

*New in Version 1.0*

----

### 方法

#### get(*key*)

获得当前配置的值。

<!--Gets the current value of a configuration variable.-->

```python
min_swipe_length = config.get("Gesture.Swipe.MinLength")
```

参数：**key**(*string*) - 设置变量的名字。
返回值：当前与制定键值关联的值。

<!--Parameters:	key (string) – The name of the configuration variable.
Returns:	the value currently associated with the specified key.-->

--

#### set(*key*, *value*)
将配置变量设置为本地指定的值。如果不调用`save()`方法则不会生效。

<!--Sets a configuration variable to the specified value locally. The change in value is not effective until the save() method is called.-->

```python
config.set("Gesture.Swipe.MinLength", 100)
```

参数：

* **key**(*string*) - 配置变量的名字
* **value**(必须设置成对应的参数类型) - 要设置的值

<!--Parameters:	
key (string) – The name of the configuration variable.
value (must be convertible to the type specified by the type parameter) – The value to set.
-->

--

#### save()
保存当前状态的配置。

<!--Saves the current state of the config.-->

```
config.save()
```

调用`save()`之后。`save()`函数改变了LeapMotion 服务的配置。你可以在`Controller`连接 LeapMotion 服务或后台之后调用`save()`。换句话说，在`serviceConnected` 或 `connected` 事件或者 `Controller.isConnected` 为 `true`之后为`Controller`设置其配置。配置的值并不是持久的，你的应用应该在每次运行的时候都进行这样的设置。

返回值：`True` 表示设置成功，`False` 表示设置失败。

<!--Call save() after making a set of configuration changes. The save() function transfers the configuration changes to the Leap Motion service. You can call save() after the Controller has connected to the Leap Motion service/daemon. In other words, after the Controller has dispatched the serviceConnected or connected events or Controller.isConnected is true.The configuration value changes are not persistent; your application must set the values everytime it runs.

Returns:	True on success; False on failure.-->

*New in Version 1.0*