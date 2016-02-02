# CircleGesture

属性：

* center
* normal
* progress
* radius
* pointable
* class_type

## ***class*** **Leap. CircleGesture**
继承自 `Gesture` 。

CircleGesture 类表示一个画圈的手指动作。

手指指尖在 LeapMotion 控制器视野内做一个画圈的动作是能够被识别的。

<!--Extends Gesture.

The CircleGesture classes represents a circular finger movement.

A circle movement is recognized when the tip of a finger draws a circle within the Leap Motion Controller field of view.-->

![](../images/Leap_Gesture_Circle.png)

注意：在你的应用中始终画圈手势识别前你必须先激活它，你可以这样做：

<!--Important: To use circle gestures in your application, you must enable recognition of the circle gesture. You can enable recognition with:-->

```python
controller.enable_gesture(Leap.Gesture.TYPE_CIRCLE)
```

画圈手势是连续的。CircleGesture 对象的手势有三种状态：

* STATE_START - 一个圈型手势刚刚开始。指尖的移动过程处理一定程度后，分类器就会把它识别成一个圆圈。
* STATE_UPDATE - 一个圈型手势还在继续。
* STATE_STOP - 圈型手势结束。

你可以使用 config 属性来设置一个连接的 Controller 对象识别圆圈手势的最小半径和最小弧长。使用下面的键值来配置圆圈的识别：

<!--Circle gestures are continuous. The CircleGesture objects for the gesture have three possible states:

STATE_START – The circle gesture has just started. The movement has progressed far enough for the recognizer to classify it as a circle.
STATE_UPDATE – The circle gesture is continuing.
STATE_STOP – The circle gesture is finished.
You can set the minimum radius and minimum arc length required for a movement to be recognized as a circle using the config attribute of a connected Controller object. Use the following keys to configure circle recognition:-->

|键值|类型|默认值|单位|
|:--|:--|:--|:--|
|Gesture.Circle.MinRadius|float|5.0|mm|
|Gesture.Circle.MinArc|float|1.5 * pi|radians|

下面的例子展示了如何设置一个圆圈的配置参数：

<!--The following example demonstrates how to set the circle configuration parameters:-->

```python
controller.config.set("Gesture.Circle.MinRadius", 10.0)
controller.config.set("Gesture.Circle.MinArc", .5)
controller.config.save()
```

*New in version 1.0*

----

### 构造函数

*classmethod* **CircleGesture([*gesture*])**
从一个 Gesture 类实例中构造一个 CircleGesture 对象。

<!--Constructs a CircleGesture object from an instance of the Gesture class.-->

```python
circle = Leap.CircleGesture(gesture)
```
参数：**gesture**(*Gesture*) - 特定的 Gesture 实例。这个 Gesture 实例必须是 CircleGesture 对象。如果没有设置参数，或者传入其他实例的手势，则会创建一个无效的CircleGesture 对象。

<!--Parameters:	gesture (Gesture) – The Gesture instance to specialize. This Gesture instance must be a CircleGesture object. If no argument is supplied, an invalid CircleGesture object is created.-->

----

### 属性

#### center
类型：Vector

当前 LeapMotion 帧中所画圆圈的圆心。

<!--The center point of the circle within the Leap Motion frame of reference.-->

```python
centerPoint = circle.center
```
*New in version 1.0*

--

#### normal
类型：Vector

被追踪的圆圈的法向量。

如果你顺时针画圆圈，那么法向量会与可指向对象画圈的方向相同。如果你你逆时针方向画圈，那么法向量就会与可指向对象的方向相背。相反，如果法向量和可指向对象的夹角小于90度，那么所画圈则为顺时针方向。

<!--The normal vector for the circle being traced.

If you draw the circle clockwise, the normal vector points in the same general direction as the pointable object drawing the circle. If you draw the circle counterclockwise, the normal points back toward the pointable. If the angle between the normal and the pointable object drawing the circle is less than 90 degrees, then the circle is clockwise.-->

```python
circle = Leap.CircleGesture(gesture)
if (circle.pointable.direction.angle_to(circle.normal) <= Leap.PI/2):
    clockwiseness = "clockwise"
else:
    clockwiseness = "counterclockwise"
```

*New in version 1.0*

--

#### progress
类型： float

指尖画圈的次数。

Progress 的值是一个正值。例如当一个progress 的值为 0.5 时，表示手指已经画完一半了，如果值为 3 则表示已经画满三圈了。

<!--The number of times the finger tip has traversed the circle.

Progress is reported as a positive number of the number. For example, a progress value of .5 indicates that the finger has gone halfway around, while a value of 3 indicates that the finger has gone around the the circle three times.-->

```python
import math
completeTurns = math.floor(circle.progress)
```

Progress 在画圈手势开始时启动。 LeapMotion 软件识别出它时，画圈这个动作必须已经完成了其中一部分，progress 会从 0 开始生产当它首次出现在一帧中时。

<!--Progress starts where the circle gesture began. Since the circle must be partially formed before the Leap Motion software can recognize it, progress will be greater than zero when a circle gesture first appears in the frame.-->

*New in version 1.0*

--

#### radius
类型：float

画圈的弧度。

<!--The radius of the circle.-->

```python
diameter = 2 * circle.radius
```

*New in version 1.0*

--

#### pointable
类型： Pointable

执行画圈的手指。

<!--The finger performing the circle gesture.-->

```python
circlingPointable = circle.pointable
```
*New in version 1.0*

----

### 类属性

#### class_type
类型：int

圆圈手势类型指示符：Gesture.TYPE_CIRCLE

<!--The circle gesture type designator: Gesture.TYPE_CIRCLE-->

*New in version 1.0*


