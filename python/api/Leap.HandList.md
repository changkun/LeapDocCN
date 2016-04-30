# HandList

属性：

* [is_empty](#is_empty)
* [frontmost](#frontmost)
* [leftmost](#leftmost)
* [rightmost](#rightmost)

方法：

* [append()](#append)

## ***class*** **Leap.HandList**
HandList 类继承自 Python 数组来表示一系列 Hand 对象。

通过 `Frame.hands()` 来获取一个 HandList 对象。

```python
all_hands = frame.hands
```

*New in version 1.0*

----

### 构造函数
*classmethod* **HandList**()
构造一个空列表。

从一个 Frame 对象中获得包含跟踪工具的 HandList。

```python
all_the_Hands = frame.hands
```
*New in version 1.0*

----

### 属性
#### is_empty
类型：boolean

表示一个列表是否为空。


```python
if not frame.hands.is_empty:
    #Process hands...
    print str(hand)
```

*New in version 1.0*

--

#### frontmost
类型： Hand

z 轴坐标最小的列表项。

```python
front_hand = frame.hands.frontmost
```
*New in version 1.0*

--

#### leftmost
类型： Hand
x 轴坐标最小的列表项。


```python
farthest_left = frame.hands.leftmost
```
*New in version 1.0*

--

#### rightmost
类型： Hand
x 轴坐标最大的列表项。


```python
furthest_right = frame.hands.rightmost
```
*New in version 1.0*

----

### 方法

#### append(*other*)
将制定的 HandList 成员添加到 HandList 中。

参数：**other**（*HandList*）—— 一个 HandList 对象包含的 Hand 对象会添加到 HandList 的末尾。
