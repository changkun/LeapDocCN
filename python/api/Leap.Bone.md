# Bone

属性：

* basis
* center
* direction
* is_valid
* length
* next_joint
* prev_joint
* type
* width

## ***class*** **Leap.Bone**
Bone(骨头) 类表示手指的一根骨头。

所有的手指都能拆解包含 4 个骨头。可以从一个 Finger 对象中获得一个有效的 Bone 对象。

骨头可以从底部往指尖进行遍历，索引值从 0 到 3。另外，Bone 的类型枚举能够用于索引一个骨头。

拇指没有 Metacarpal 骨，但仍然是一个有效的对象，只不过他的长度为 0。

注意，Bone 对象也可以是无效的，这种情况发生在当它们没有包含有效的追踪数据以及没有匹配的物理意义的 Bone。无效的 Bone 对象可以作为访问一个无效的 Finger 对象的 Bone 对象的结果。从 Bone 对象的构造函数创建 Bone 依然可以是无效的。可以通过 `Bone.is_valid()` 属性来测试是否有效。

<!--The Bone class represents a bone of a finger.

All fingers contain 4 bones that make up the anatomy of the finger. Get valid Bone objects from a Finger object.

Bones are ordered from base to tip, indexed from 0 to 3. Additionally, the bone’s Type enum may be used to index a specific bone anatomically.

The thumb does not have a base metacarpal bone and therefore contains a valid, zero length bone at that location.

Note that Bone objects can be invalid, which means that they do not contain valid tracking data and do not correspond to a physical Bone. Invalid Bone objects can be the result of asking for a Bone object from an invalid Finger object. A Bone object created from the Bone constructor is also invalid. Test for validity with the Bone.is_valid() attribute.-->

*New in Version 2.0*

### 构造函数
*classmethod* **Bone([Bone])**

构造一个 Bone 对象。

从一个 Finger 对象中获得一个有效的 Bone 对象。

<!--Constructs a Bone object.

Get valid Bone objects from a Finger object.-->

```python
bone = Leap.Bone() # 无效的
```

参数：Bone(Bone): 一个表示 Bone 对象。如果没有给 Bone 提供参数或者对象并不表示 Bone，则会返回一个无效的 Bone 对象。

<!--Bone (Bone) – An object representing a Bone. If no Bone parameter is supplied, or the object does not represent a Bone, an invalid Bone object is returned.-->

返回类型：Bone

*New in Version 2.0*

----

### 实例属性

#### basis
类型：Matrix

一个 Bone 的正交基向量矩阵。

基向量指定了一根骨头的方向。

* x_basis： 垂直于骨头，沿骨头的侧向；
* y_basis 或 up vector：垂直于骨头，沿骨头的上下方向，正轴为向上的方向。
* z_basis：沿骨头方向，正方向指向手指的根部。

<!--The orthonormal basis vectors for this Bone as a Matrix.

Basis vectors specify the orientation of a bone.

x_basis. Perpendicular to the longitudinal axis of the bone; exits the sides of the finger.
y_basis or up vector. Perpendicular to the longitudinal axis of the bone; exits the top and bottom of the finger. More positive in the upward direction.
z_basis. Aligned with the longitudinal axis of the bone. More positive toward the base of the finger.-->

```python
basis = bone.basis
x_basis = basis.x_basis
y_basis = basis.y_basis
z_basis = basis.z_basis
origin = basis.origin
```

左手使用左手定则，右手使用右手定则。因此 x 轴正方向向右，而左手的正方向向左。你也可以通过吧基向量乘以 -1 将右手改为左手定则。

你可以使用基向量作为测量复杂手姿和骨骼动画的依据。

需要注意的是，将基向量直接转化成一个四元数并不是数学意义上有效的。如果你要使用四元数，不要直接创建他们，应该用旋转矩阵来推导创建。

<!--The bases provided for the right hand use the right-hand rule; those for the left hand use the left-hand rule. Thus, the positive direction of the x-basis is to the right for the right hand and to the left for the left hand. You can change from right-hand to left-hand rule by multiplying the basis vectors by -1.

You can use the basis vectors for such purposes as measuring complex finger poses and skeletal animation.

Note that converting the basis vectors directly into a quaternion representation is not mathematically valid. If you use quaternions, create them from the derived rotation matrix not directly from the bases.
-->

*New in Version 2.0*

--

#### center
类型：Vector

骨的中点位置。

<!--The midpoint of the bone.-->

```python
middle = bone.center
```

*New in Version 2.0*

--

#### direction
类型：Vector

从指根到指间的单位向量方向。

<!--The normalized direction of the bone from base to tip.-->

```python
direction = bone.direction
```

这个方向是骨头 z 轴的的负方向。

<!--This is the negative of the bone’s z-basis.-->

*New in Version 2.0*

--

#### is_valid
类型：boolean

返回一个 Bone 对象的数据是否有效。

<!--Reports whether this Bone object contains valid data.-->

```python
bone = finger.bone(Bone.TYPE_PROXIMAL)
if(bone.is_valid):
    # ... 使用 Bone 数据
```

*New in Version 2.0*

--

#### length
类型：float

一个骨头的长度，单位是毫米。

<!--The length of the bone in millimeters.-->

```python
length = bone.length
```

*New in Version 2.0*

--

#### next_joint
类型：Vector

离指尖最近的骨头末端的位置。

<!--The position of the end of the bone closest to the finger tip.-->

```python
bone_end = bone.next_joint
```

*New in Version 2.0*

--

#### prev_joint
类型：Vector

离手腕最近的骨头末端的位置。

<!--The position of the end of the bone closest to the wrist.-->

```python
bone_start =  bone.prev_joint
```

*New in Version 2.0*

--

#### type
类型：integer

Bone 的名字。

<!--The name of this Bone.-->

```python
type = bone.type
```
Bone 的类型有：

* 0 = TYPE_METACARPRAL - 链接手腕的那根骨头
* 1 = TYPE_PROXIMAL - 手指暴露出来的第一根的骨头，离手掌最近的那个骨头。
* 2 = TYPE_INTERMEDIATE - 手指中间的那根骨头
* 3 = TYPE_DISTAL - 手指指尖所在的那根骨头

<!--The anatomical type of this Bone:

0 = TYPE_METACARPAL – the bone inside the hand connecting the wrist and finger
1 = TYPE_PROXIMAL – the first exposed bone of the finger, closest to the hand.
2 = TYPE_INTERMEDIATE – the middle bone of the finger
3 = TYPE_DISTAL – the bone at the tip of the finger-->

*New in Version 2.0*

--

####  width
类型：float

手指骨头的平均宽度（包括肉质）。

<!--The average width of the finger along the bone (including the fleshy sheathe).-->

```python
width = bone.width
```

*New in Version 2.0*

----

### 类属性

#### invalid
类型：Bone

一个无效的 Bone 对象。

<!--An invalid Bone object.-->

```python
bone = Bone.invalid
```
你可以使用这个无效的对象来测试一个 Bone 的实例是否是有效的。（当然你也可以用 `Bone.is_valid` 这个属性）

<!--You can use this invalid object in comparisons testing whether a given Bone instance is valid or invalid. (You can also use the Bone.is_valid attribute.)
-->

*New in Version 2.0*

--

#### TYPE_DISTAL
类型：integer

Phalanx 骨，手指的末端（离身体最远的地方）索引值为3。

<!--The phalanx bone at the end for the finger (most distant from the body). The distal phalanx has index 3.-->

```python
distal_bone = finger.bone(Bone.TYPE_DISTAL)
```

*New in Version 2.0*

--

#### TYPE_INTERMEDIATE
类型：integer

位于  Distal 和 Proximal Phanlanges 之间的骨头，索引值为 2。

<!--The bone in between the distal and proximal phanlanges. The intermediate phalanx has index 2.-->

```python
intermediate_bone = finger.bone(Bone.TYPE_INTERMEDIATE)
```

*New in Version 2.0*

--

#### TYPE_PROXIMAL
类型：integer

手指根部的第一根骨头（离身体最近的那根），索引值为1。

<!--The finger bone at the base of the finger (in closest proximity to the body). The proximal phalanx has index 1.-->

```python
proximal_bone = finger.bone(Bone.TYPE_PROXIMAL)
```

*New in Version 2.0*

--

#### TYPE_METACARPAL
类型：integer

连接手腕区域的第一根骨头，索引值为0。

<!--The bone connecting the wrist area to the base of the proximal finger bone. The metacarpal has index 0.-->

```python
metacarpal_bone = finger.bone(Bone.TYPE_METACARPAL)
```

**注意**：一个真正的拇指比其他的手指要少一根骨头，然而 LeapMotion 的拇指模型依然认为这根骨头是有效的，只不过Metacarpal 的长度为 0。虽然这与正常的解剖学命名系统有所不同，但是这使得对于每一根手指能使用相同的索引方法。

<!--Note: A real thumb has one less bone than the other fingers; therefore the Leap Motion assigns the thumb model a valid, zero-length bone at the metacarpal index. While this differs from the normal anatomical naming system, which dispenses with the intermediate phalanx instead, it does mean that each finger, including the thumb, has the same bone at the same index.-->

*New in Version 2.0*