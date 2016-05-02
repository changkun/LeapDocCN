# 运动

LeapMotion 软件分析了从先前帧开始发生的全部运动，综合了典型的平移、旋转及缩放因子。例如，如果你同时移动两只手向左，那么 LeapMotion 视野所在镇则会包含平移。如果你旋转双手像捧一个球一样，那么帧就会包含旋转。如果你移动双手靠拢或彼此远离则会包含缩放。

<!--
The Leap Motion software analyzes the overall motion that has occurred since an earlier frame and synthesizes representative translation, rotation, and scale factors. For example, if you move both hands to the left in the Leap Motion field of view the frame contains translation. If you twist your hands as if turning a ball, the frame contains rotation. If you move your hands towards or away from each other, the frame contains scaling.-->

LeapMotion 软件分析运动以及在[Frame](../api/Leap.Frame.md)返回运动因子时，会使用视野内的全部对象。如果只能检测到一只手，那么 LeapMotion 软件会在这只手的移动中求出帧的运动因子。你也可以在每个[Hand](../api/Leap.Hand.md)对象中中获得独立的运动因子。

<!--
The Leap Motion software uses all of the objects within the field of view when analyzing motion and reports the motion factors in the Frame object. If it only detects one hand, then the Leap Motion software bases the frame motion factors on the movement of that hand. If it detects two hands, then the Leap Motion software bases the frame motion factors on the movement of both hands together. You can also get independent motion factors for each hand from a Hand object.
-->

运动是由比较当前帧的特殊的早期帧推导得出。

<!--Motions are derived by comparing the current frame with a specified earlier frame.-->

## 运动的类型
LeapMotion API 提供了以下几种类型的运动：

* 平移 —— 三维的线性移动
* 缩放 —— 相对膨胀或收缩
* 旋转 —— 三维的角度变换

你可以使用运动因子在你的应用场景来操作对象，而不必在多个帧中追踪单独的手和手指。

<!--
Types of Motions¶
The Leap Motion API provides three types of motions:

Translation – linear movement in 3 dimensions.
Scale – relative expansion or contraction.
Rotation – angular change in 3 dimensions.
You can use the motion factors to manipulate objects in your application’s scene without having to track individual hands and fingers over multiple frames.
-->

## 运动属性
你可以从[Frame](../api/Leap.Frame.md)和[Hand](../api/Leap.Hand.md)对象来获取运动因子。所描述的运动属性包括：

* 旋转轴 —— 表示旋转轴的方向向量
* 旋转角 —— 旋转轴顺时针方向的旋转角（使用右手定则）
* 旋转矩阵 —— 表示旋转的变换矩阵
* 缩放因子 —— 表示扩展或收缩的因子
* 平移 —— 表示线性移动的向量

<!--
Motion Properties
You can get motion factors from Frame objects and Hand objects. The attributes describing the synthesized motion include:

Rotation Axis — A direction vector expressing the axis of rotation.
Rotation Angle — The angle of rotation clockwise around the rotation axis (using the right-hand rule).
Rotation Matrix — A transform matrix expressing the rotation.
Scale Factor — A factor expressing expansion or contraction.
Translation — A vector expressing the linear movement.
-->