# PointableList

属性：

* [is_empty](#is_empty)
* [frontmost](#frontmost)
* [leftmost](#leftmost)
* [rightmost](#rightmost)

方法：

* [append()](#append)
* [extended()](#extended)

## ***class*** **Leap.PointableList**
PointableList 类继承自 Python 数组来表示一系列 Pointable 对象。

通过 `Frame.Pointables()` 或者 `Hand.pointables()` 来获取一个 PointableList 对象。

```python
#From frame:
pointables = frame.pointables

#From hand
pointables = hand.pointables
```

*New in version 1.0*

----

### 构造函数
*classmethod* **PointableList**()
构造一个空列表。

*New in version 1.0*

----

### 属性
#### is_empty
类型：boolean

表示一个列表是否为空。


```python
if frame.pointables.is_empty:
    print "Skipping empty frame"
```

*New in version 1.0*

--

#### frontmost
类型： Pointable

z 轴坐标最小的列表项。

```python
front_pointable = frame.pointables.frontmost
```
*New in version 1.0*

--

#### leftmost
类型： Pointable
x 轴坐标最小的列表项。


```python
leftmost_pointable = frame.pointables.leftmost
```
*New in version 1.0*

--

#### rightmost
类型： Pointable
x 轴坐标最大的列表项。


```python
rightmost_pointable = frame.pointables.rightmost
```
*New in version 1.0*

----

### 方法

#### append(*other*)
将制定的 PointableList 成员添加到 PointableList 中。

参数：**other**（*PointableList*）—— 一个 PointableList 对象包含的 Pointable 对象会添加到 PointableList 的末尾。

*New in version 1.0*

--

#### extended()
从 PointableList 中移除不可扩展的手指。

```python
extended_Pointable_list = frame.Pointables.extended()
```

返回：

修改后的 PointableList 对象，仅包含可扩展的手指。

*New in version 2.0*
