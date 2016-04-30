# FingerList

属性：

* [is_empty](#is_empty)
* [frontmost](#frontmost)
* [leftmost](#leftmost)
* [rightmost](#rightmost)

方法：

* [append()](#append)
* [extended()](#extended)
* [finger_type()](#finger_type)

## ***class*** **Leap.FingerList**
FingerList 类继承自 Python 数组来表示一系列 Finger 对象。

通过 `Frame.Fingers()` 来获取一个 FingerList 对象。

```python
all_Fingers = frame.Fingers
```

*New in version 1.0*

----

### 构造函数
*classmethod* **FingerList**()
构造一个空列表。

从一个 Frame 对象中获得包含跟踪工具的 FingerList。

```python
all_the_Fingers = frame.Fingers
```
*New in version 1.0*

----

### 属性
#### is_empty
类型：boolean

表示一个列表是否为空。


```python
if not frame.Fingers.is_empty:
    #Use the fingers
```

*New in version 1.0*

--

#### frontmost
类型： Finger

z 轴坐标最小的列表项。

```python
most_forward_finger = frame.fingers.frontmost
```
*New in version 1.0*

--

#### leftmost
类型： Finger
x 轴坐标最小的列表项。


```python
finger_with_smallest_x = frame.fingers.leftmost
```
*New in version 1.0*

--

#### rightmost
类型： Finger
x 轴坐标最大的列表项。


```python
finger_with_largest_x = frame.fingers.rightmost
```
*New in version 1.0*

----

### 方法

#### append(*other*)
将制定的 FingerList 成员添加到 FingerList 中。

参数：**other**（*FingerList*）—— 一个 FingerList 对象包含的 Finger 对象会添加到 FingerList 的末尾。

*New in version 1.0*

--

#### extended()
从 FingerList 中移除不可扩展的手指。

```python
extended_finger_list = frame.fingers.extended()
```

返回：

修改后的 FingerList 对象，仅包含可扩展的手指。

*New in version 2.0*

--

#### finger_type(*type*)
返回指定类型的手指，只能指定一个。

参数：**type**（*integer*）—— 手指类型的代码。使用Finger 类的属性，例如`Finger.TYPE_THUMB`来指定一个特定的类型。

返回：一个 FingerList 对象包含了指定类型的手指。

*New in version 2.0*
