# ToolList

属性：

* [is_empty](#is_empty)
* [frontmost](#frontmost)
* [leftmost](#leftmost)
* [rightmost](#rightmost)

方法：

* [append()](#append)

## ***class*** **Leap.ToolList**
ToolList 类继承自 Python 数组来表示一系列 Tool 对象。

通过 `Frame.tools` 来获取一个 ToolList 对象。

<!--The ToolList class extends the Python array to represent a list of Tool objects.

Get a ToolList object from Frame.tools.-->

```python
all_the_tools = frame.tools
for tool in all_the_tools:
    # ... 使用 tool
```

*New in version 1.0*

----

### 构造函数
*classmethod* **ToolList**()
构造一个空列表。

从一个 Frame 对象中获得包含跟踪工具的 ToolList。

<!--Constructs an empty list.

Get ToolLists containing tracked tools from a Frame object.-->

```python
all_the_tools = frame.tools
```
*New in version 1.0*

----

### 属性
#### is_empty
类型：boolean

表示一个列表是否为空。

<!--Reports whether the list is empty.-->

```python
if not frame.tools.is_empty:
    # 使用 tool
```

*New in version 1.0*

--

#### frontmost
类型： Tool

z 轴坐标最小的列表项。

<!--The item in this list with the smallest z coordinate.-->

```python
most_forward_tool = frame.tools.frontmost
```
*New in version 1.0*

--

#### leftmost
类型： Tool
x 轴坐标最小的列表项。

<!--The item in this list with the smallest x coordinate.-->

```python
tool_with_smallest_x = frame.tools.leftmost
```
*New in version 1.0*

--

#### rightmost
类型： Tool
x 轴坐标最大的列表项。

<!--The item in this list with the largest x coordinate.-->

```python
tool_with_ largest_x = frame.tools.rightmost
```
*New in version 1.0*

----

### 方法

#### append(*other*)
将制定的 ToolList 成员添加到 ToolList 中。

参数：**other**（*ToolList*）—— 一个 ToolList 对象包含的 Tool 对象会添加到 ToolList 的末尾。

<!--Appends the members of the specifed ToolList to this ToolList.

Parameters:	other (ToolList) – A ToolList object containing Tool objects to append to the end of this ToolList.-->