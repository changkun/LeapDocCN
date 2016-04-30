# KeyTapGesture

属性：

* [direction](#direction)
* [position](#position)
* [pointable](#pointable)
* [class_type](#class_type)


## ***class*** **Leap.KeyTapGesture**
扩展自 [Gesture](../api/Leap.Gesture.md)

KeyTapGesture(击键手势) 类表示手指或工具的点击手势。

击键手势识别手指指尖的旋转并返回原始位置的手势。如果要识别这个手势，那么手指必须在开始前短暂停顿。

![](../images/Leap_Gesture_Tap.png)

重要：要在应用中使用击键盘手势，你需要激活击键手势识别。你可以通过下面的代码激活这种识别：

```python
controller.enable_gesture(Leap.Gesture.TYPE_KEY_TAP);
```

KeyTap 手势是离散的，KeyTapGesture 对象总是表示一个点击的状态 STATE_STOP。仅当识别到屏幕点击手势后才会被创建。

你可以设置手指移动范围和速度的最小值。使用下面的键值可以进行设置：

|键值|值类型|默认值|单位|
|:--:|:--:|:--:|:--:|:--:|
|Gesture.ScreenTap.MinDownVelocity|float|50|mm/s|
|Gesture.Swipe.HistorySeconds|float|0.1|mm|
|Gesture.ScreenTap.MinDistance|float|3.0|mm|

下面的代码展示了如何设置这些值：

```python
controller.config.set("Gesture.KeyTap.MinDownVelocity", 40.0)
controller.config.set("Gesture.KeyTap.HistorySeconds", .2)
controller.config.set("Gesture.KeyTap.MinDistance", 1.0)
controller.config.save()
```

*New in Version 1.0*

### 构造函数
*classmethod* **KeyTapGesture([gesture])**

从 Gesture 类实例中构造一个 KeyTapGesture 对象。

```python
for gesture in frame.gestures():
    if gesture.type is Leap.Gesture.TYPE_KEY_TAP:
        key_tap = Leap.KeyTapGesture(gesture)
```

参数：

gesture([Gesture](../api/Leap.Gesture.md)) - Gesture 实例专用。这个 Gesture 实例必须是一个 ScreenTapGesture 对象。如果没有给出参数，那么一个无效的 ScreenTapGesture 对象会被创建。

*New in Version 1.0*

### 属性

**position**

类型：[Vector](../api/Leap.Vector.md)

点击手势的位置。

```python
tap_point = key_tap.position
```

*New in Version 1.0*

**position**

类型：[Vector](../api/Leap.Vector.md)

击键手势的当前位置

```python
current = key_tap.position
```

*New in Version 1.0*

**direction**

类型：[Vector](../api/Leap.Vector.md)

手指指尖的方向。如果手指不动，那么这个手势也会被记录，并被记录为零向量。

```python
tap_direction = key_tap.direction
```

*New in Version 1.0*

**progress**

类型：float

progress 值总是 1。

*New in Version 1.0*

**pointable**

类型：[Pointable](../api/Leap.Pointable.md)

执行击键手势的手指。

```python
tapper = key_tap.pintable
```

*New in Version 1.0*

### 类属性
*classmethod* **class_type()**

类型：integer

击键手势类型指示器：`Gesture.TYPE_KEY_TAP`
