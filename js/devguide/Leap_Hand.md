# 手

手是 LeapMotion 控制器追踪的主要实体。控制器维护了一个人手和数据验证内建模型，控制器的传感器也依赖此模型。则允许控制器能追踪手指的位置，甚至当一个手指处于完全不可见状态。请注意，当一个手指不可见或者在手的背后时，移动或者改变位置是有可能失去目标。LeapMotion 软件匹配了内部模型和现有的数据。在某些情况下，软件会出现错误匹配的情况 - 比如讲一个右手识别为一个左手。

<!--
Hands are the main entity tracked by the Leap Motion controller. The controller maintains an inner model of the human hand and validates the data from its sensors against this model. This allows the controller to track finger positions even when a finger is not completely visible. Note that it is possible for movement or changes in position to be lost when a finger is behind or directly in front of the hand (from the point of view of the controller). The Leap Motion software matches the internal model against the existing data. In some cases, the software can make an incorrect match – for example, identifying a right hand as a left hand.
-->

[Hand](../api/Leap.Hand.md) 类表示了一个 Leap 检测到的物理手。一个 Hand 对象提供访问了它的可形象列表，以及描述手的位置、方向和运动属性。

Hand 可以识别分别识别左手和右手。此外，每个手都会在被检测到后分配一个 ID 值。如果你从 LeapMotion 视野中移除在重新插入一个手时会重新分配一个 ID（可以使用 `timeVisible` 属性来设置一个手是否被重新检测）。如果 LeapMotion 软件认为它误判了一只手的类型并要做改变时，还是会重新非配一个新的手 ID。

<!--
The Hand class represents a physical hand detected by the Leap. A Hand object provides access to lists of its pointables as well as attributes describing the hand position, orientation, and movement.

Hands can be identified by left versus right handedness. In addition, each hand is assigned an ID value when the hand is first detected. If you remove a hand from the Leap Motion field of view and then re-insert it, a new ID is assigned (use the timeVisible attribute to tell whether a hand is newly detected or not). New hand IDs are also assigned if the Leap Motion software decides it has misclassified a hand and must change its type from right to left or vice versa.
-->

## 获取手

从一个 [Frame](../api/Leap.Frame.md) 中获取 Hand 对象：

<!--
Getting Hands
Get Hand objects from a Frame:
-->

```python
frame = controller.frame() # controller is a Leap.Controller object
hands = frame.hands
first_hand = hands[0]
```

如果你知道手的 ID 也可以：

<!--Or, if you know the ID from a previous frame:-->

```python
know_hand = frame.hand(hand_ID)
```

你还可以利用帧中的相对位置获取手:

<!--You can also get hands by their relative positions in the frame:-->

```python
frame = controller.frame() # 控制器是一个 Leap.Controller 对象
hands = frame.hands

leftmost = hands.leftmost
rightmost = hands.rightmost
frontmost = hands.frontmost
```

注意，`leftmost()`和`rightmost()`函数只能识别哪只手是最远的。使用 `isLeft`或者`isRight`属性来判断一只手是左手还是右手。

<!--Note that the the leftmost() and rightmost() functions only identify which hand is farthest to the left or right. Use the Hand isLeft or isRight attribute to tell if a hand object represents a left or a right hand.-->

## 获取手的特征
一只手描述了它自身的类型、位置、方向、姿势以及动作：

* `isRight`、`isLeft` ——一只手是左手还是右手。
* `Palm Position`——从 LeapMotion 原点以毫米为单位的手掌的中心点。
* `Palm Velocity` ——以毫米为单位的手掌的移动速度和方向。
* `Palm Normal` ——垂直于手掌平面的向量，向量从手掌向外。
* `Direction` ——从掌心指向手指的向量。
* `grabStrength, pinchStrength` ——描述了手的姿势
* `Motion factors` ——提供了两帧之间的相关缩放、旋转、平移的因子。

<!--
Getting the Hand Characteristics
A hand is described by its handedness, position, orientation, posture, and motion:

isRight, isLeft — Whether the hand is a left or a right hand.
Palm Position — The center of the palm measured in millimeters from the Leap Motion origin.
Palm Velocity — The speed and movement direction of the palm in millimeters per second.
Palm Normal — A vector perpendicular to the plane formed by the palm of the hand. The vector points downward out of the palm.
Direction — A vector pointing from the center of the palm toward the fingers.
grabStrength, pinchStrength — Describe the posture of the hand.
Motion factors — Provide relative scale, rotation, and translation factors for movement between two frames.
-->

手的位置通过其手掌的位置属性给出，提供包含以毫米为单位的 LeapMotion 原点的三维坐标。手的方向通过两种向量给出：从掌心指向手指的方向向量，以及垂直于手掌平面向外的法向量。

手的移动给出了速度的属性，一个向量提供了以 mm/s 为单位的手的瞬间移动。你也可以获取一直手在两帧之间的平移、旋转、缩放的运动因子的值。

下面的代码段展示了如何从一个帧中获取手的基本属性：

```python
hand = frame.hands.rightmost
position = hand.palm_position
velocity = hand.palm_velocity
direction = hand.direction
```

<!--
The hand’s position is given by its palm position attribute, which provides a vector containing the 3-dimensional coordinates of the palm center point in millimeters from the Leap Motion origin. The hand’s orientation is given by two vectors: the direction, which points from the palm center towards the fingers, and the palm normal, which points out of the palm, perpendicular to the plane of the hand.

The movement of the hand is given by the velocity attribute, which is a vector providing the instantaneous motion of the hand in mm/s. You can also get motion factors that translate how a hand has moved between two given frames into translation, rotation, and scaling values.

The following code snippet illustrates how to get a Hand object from a frame and access its basic attributes:

hand = frame.hands.rightmost
position = hand.palm_position
velocity = hand.palm_velocity
direction = hand.direction
-->

## 获取手指
你可以获取与手关联的手指作为一个列表，或单独的使用在前一帧中获取的 ID。

通过列表：

<!--Getting the Fingers
You can get the fingers associated with a hand as a list or individually using an ID obtained in a previous frame.

By list:-->

```
# hand 是一个 Leap.Hand 对象
pointables = hand.pointables
fingers = hand.fingers
```

通过前一帧中的 ID：
<!--By ID from a previous frame:-->

```
known_pointable = hand.pointable(pointable_ID)
```

若需获取 Leap 视野内的手指相对位置，请使用匹配列表类的 rightmost, leftmost 和 fontmost 函数：

<!--To get a finger by relative position within the Leap field of view, use the right-, left- and frontmost functions of the matching list class:-->

```
# hand 是一个 Leap.Hand 对象
left_pointable = hand.pointables.leftmost
right_finger = hand.fingers.rightmost
front_finger = hand.fingers.frontmost
```

请注意，这些函数都是相对 LeapMotion 原点而不是手本身的。为获得手相关的手指，你可以使用 Leap Matrix 类来平移手指位置到参考系手所在帧中。

<!--
Note that these functions are relative to the Leap Motion origin, not to the hand itself. To get the fingers relative to the hand, you can use the Leap Matrix class to transform the finger positions into the hands frame of reference.
-->

## 计算手的方向

你可以使用[Hand](../api/Leap.Hand.md)的方向和法向量计算手的方向角。

<!--Computing the Hand Orientation¶
You can compute the hand orientation angles using the Hand direction and normal vectors.-->

![法向量从手掌垂直引出；方向向量则指向前方](../../images/Leap_Palm_Vectors.png)

[Vector](../api/Leap.Vector.md)定义pitch, yaw, roll 三个角度，他们分别是绕 x, y, z 三轴所成夹角。

<!--The Vector class defines functions for getting the pitch (angle around the x-axis), yaw (angle around the y-axis), and roll (angle around the z-axis):-->

```
pitch = hand.direction.pitch
yaw = hand.direction.yaw
roll = hand.palm_normal.roll
```
注意， roll 仅在同时使用法向量时才提供预期的角度。

<!--Note that the roll function only provides the expected angle when used with a normal vector.-->

## 将手指坐标平移到手的参考帧

有时候获取手所在帧参考系中手指的坐标很有用。则使你可以对手进行空间排序，还能够简化分析手的位置。你可以创建一个平移矩阵通过使用 Leap [Matrix](../api/Leap.Matrix.md) 类来平移手指位置和方向坐标。手的参考帧可以有效的定义手的 [basis](../api/Leap.Hand.md) 以及 [palm_position](../api/Leap.Hand.md)。basis 将 x 轴设置为手的侧向，z 轴则指向前方，而 y 轴则平行于手掌的法向量。palm_position 为平移原点。

<!--
Transforming Finger Coordinates into the Hand’s Frame of Reference
Sometimes it is useful to obtain the coordinates of the fingers of a hand with respect to the hand’s frame of reference. This lets you sort the fingers spatially and can simplify analysis of finger positions. You can create a transform matrix using the Leap Matrix class to transform the finger position and direction coordinates. The hand frame of reference can be usefully defined by the hand’s basis and palm_position. The basis orients the x-axis sideways across the hand, the z-axis pointing forward, and the y-axis parallel with the palm normal. The origin of the transform is the palm_position.-->

```
frame = controller.frame()
for hand in frame.hands:
    hand_x_basis = hand.basis.x_basis
    hand_y_basis = hand.basis.y_basis
    hand_z_basis = hand.basis.z_basis
    hand_origin = hand.palm_position
    hand_transform = Leap.Matrix(hand_x_basis, hand_y_basis, hand_z_basis, hand_origin)
    hand_transform = hand_transform.rigid_inverse()

    for finger in hand.fingers:
        transformed_position = hand_transform.transform_point(finger.tip_position)
        transformed_direction = hand_transform.transform_direction(finger.direction)
        # Do something with the transformed fingers
```

## 手序列
[HandList](../api/Leap.HandList.md) 类的行为如同一个向量形式的数组且支持迭代器。你不能够从 LeapMotion API 来删除或修改手列表的成员对象，但你可以组合相同对象类型作为一个新的列表。

迭代器的使用方法：

<!--
Hand Lists
The HandList class acts like a vector-style array and supports iterators. You cannot remove or alter the member objects of a hand lists received from the Leap Motion API, but you can combine lists of the same object type.

To use an iterator with a list class:-->

```
for hand in handList:
    print hand
```

[HandList](../api/Leap.HandList.md) 类定义了一个附加的函数从 Leap 坐标系统中的相对位置来获取列表成员。这些函数包括 leftmost(), rightmost() 和 frontmost()。下面的代码段展示了如何获取一个最右边的一个手对象：

<!--The HandList class defines additional functions for getting a member of the list based on its relative position within the Leap coordinate system. These functions include leftmost(), rightmost(), and frontmost(). The following snippet illustrates how to get the hand object furthest to the right:-->

```
furthest_right = frame.hands.rightmost
```
