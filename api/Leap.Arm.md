# Arm

属性：

* [basis](#basis)
* [direction](#direction)
* [elbow_position](#elbow_position)
* [is_valid](#is_valid)
* [width](#width)
* [wrist_position](#wrist_position)


## ***class*** **Leap.Arm**
Arm(手臂) 类表示一个追踪的手前臂。

<!--The Arm class represents a tracked arm.-->

注意，Arm 对象可以是无效的，这意味着它没有包含任何有效的的追踪数据且不符合一个物理手臂。无效的 Arm 对象能够作为从一个无效 Hand 对象访问一个 Arm 对象的结果。用 Arm 的构造函数创建一个 Arm 对象也可以是无效的。有效对象的检测办法是通过访问 [Arm.is_valid()](#is_valid) 属性。

<!--Note that Arm objects can be invalid, which means that they do not contain valid tracking data and do not correspond to a physical arm. Invalid Arm objects can be the result of asking for an Arm object from an invalid Hand object. An Arm object created with the Arm constructor is also invalid. Test for validity with the Arm.is_valid() attribute.-->

*New in Version 2.0.3*

### 构造函数
*classmethod* **Arm()**

构造一个有效的 Arm 对象。

<!--Constructs an invalid Arm object.-->

从 [Hand](Leap.Hand.md) 对象中获得一个有效的 Arm 对象。

<!--Get valid Arm objects from a Hand object.-->

```python
hand = frame.hands.frontmost
arm = hand.arm
```

返回类型：Arm

*New in Version 2.0.3*

----

### 实例属性

#### basis
类型：Matrix

一个 Arm 的正交基向量矩阵。

<!--The orthonormal basis vectors for this Arm as a Matrix.-->

基向量指定了一条手臂的方向。

<!--Basis vectors specify the orientation of a arm.-->

* x_basis: 垂直于手臂，沿手腕侧向；
* y_basis 或 up vector: 垂直于手臂，沿手臂的上下方向，正轴为向上的方向。
* z_basis：沿手臂方向，正轴指向肘部.

<!--
x_basis. Perpendicular to the longitudinal axis of the arm; exits leterally through the sides of the wrist.
y_basis or up vector. Perpendicular to the longitudinal axis of the arm; exits the top and bottom of the arm. More positive in the upward direction.
z_basis. Aligned with the longitudinal axis of the arm. More positive toward the elbow.
-->

```python
basis = arm.basis
x_basis = basis.x_basis
y_basis = basis.y_basis
z_basis = basis.z_basis
center = arm.elbow_position + (arm.wrist_position - arm.elbow_position) * .05

arm_transform = Leap.Matrix(x_basis, y_basis, z_basis, center)
```

右手臂使用了右手定则；而左手臂则使用左手定则。因此 右手臂的 x 轴正方向向右，而左手臂的 x 轴正方向向左。你可以通过将基向量乘以 -1 把右手的规则更改为左手定则。

<!--The bases provided for the right arm use the right-hand rule; those for the left arm use the left-hand rule. Thus, the positive direction of the x-basis is to the right for the right arm and to the left for the left arm. You can change from right-hand to left-hand rule by multiplying the basis vectors by -1.-->

你可以使用上述的基向量作为衡量复杂手势的姿势和骨骼动画的依据。

<!--You can use the basis vectors for such purposes as measuring complex finger poses and skeletal animation.-->

需要注意的是，将基向量直接转化成一个四元数表示并不是数学意义上有效的。
如果你要使用四元数，不要直接创建它们，而应从旋转矩阵推导创建。

<!--Note that converting the basis vectors directly into a quaternion representation is not mathematically valid. If you use quaternions, create them from the derived rotation matrix not directly from the bases.-->

*New in Version 2.0.3*

--

#### direction
类型：Vector

从手臂肘到手腕的单位向量方向。

<!--The normalized direction of the arm from elbow to wrist.-->

```python
direction = arm.direction
```

*New in Version 2.0.3*

--

#### elbow_position
类型：Vector

手臂肘的位置。

<!--The position of the elbow.-->

```python
elbow = arm.elbow_position
```

*New in Version 2.0.3*

--

#### is_valid
类型：boolean

返回一个 Arm 对象是否包含有效的数据。

<!--Reports whether this Arm object contains valid data.-->

```python
arm = frame.hand(20).arm
if(arm.is_valid):
    # ... 使用数据
```

*New in Version 2.0.3*

--

#### width
类型：float

手臂的平均宽度。

<!--The average width of the arm.-->

```python
width = arm.width

displacement = arm.wrist_position - arm.elbow_position;
length = displacement.magnitude
```

*New in Version 2.0.3*

--

#### wrist_position
类型：Vector

手腕的位置。

<!--The position of the wrist.-->

```python
wrist = arm.wrist_position
```

*New in Version 2.0.3*

----

### 类属性

####invalid
类型： Arm

一个无效的 Arm 对象。

<!--An invalid Arm object.-->

```python
arm = Leap.Arm.invalid
```

*New in Version 2.0.3*