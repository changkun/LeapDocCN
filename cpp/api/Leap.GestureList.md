# GestureList

属性：

* [is_empty](#is_empty)

方法：

* [append()](#append)

## ***class*** **Leap. GestureList**
GestureList 类继承自 Python 数组来表示一系列 Gesture 对象。

通过 `Frame.gestures()` 来获取一个 GestureList 对象。

```python
# 获得两帧之间所有的手势
gesture_list = frame.gestures(last_frame_processed)

# 仅获取当前帧中的手势
gesture_list = frame.gestures()
```

*New in version 1.0*

----

### 构造函数
*classmethod* **GestureList**()
构造一个空列表。

*New in version 1.0*

----

### 属性
#### is_empty
类型：boolean

返回列表是否为空。

```python
if not frame.gestures(last_frame_processed).is_empty:
    for gesture in frame.gestures(last_frame_processed):
        print "Type: " + str(gesture.type)
```

*New in version 1.0*

----

### 方法

#### append(*other*)
将制定的 GestureList 成员添加到 GestureList 中。

参数：

**other**（*GestureList*）—— 一个 GestureList 对象包含的 Gesture 对象会添加到 GestureList 的末尾。
