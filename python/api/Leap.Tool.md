# Tool

## ***class*** **Leap.Tool**
继承自 `Pointalbe`。

Tool(工具) 类表示一个被追踪的工具。

工具是一个 Pointable 对象，LeapMotion 软件可以将这种对象识别为一个工具。可以从一个帧中获得一个有效的 Tool 对象。

<!--The Tool class represents a tracked tool.

Tools are Pointable objects that the Leap Motion software has classified as a tool. Tools are longer, thinner, and straighter than a typical finger. Get valid Tool objects from a Frame object.-->

![](../images/Leap_Tool.png)

注意，Tool 对象可以是无效的，这意味着他们不包含有效的追踪数据以及不匹配一个实际的工具。
一个无效的 Tool 对象可以看做是使用当前帧的 ID 来访问无 Tool 对象的历史帧的结果。
利用构造函数创建的 Tool 对象仍然可以是无效的，可以用 `Pointable.is_valied`属性进行判断。

<!--Note that Tool objects can be invalid, which means that they do not contain valid tracking data and do not correspond to a physical tool. Invalid Tool objects can be the result of asking for a Tool object using an ID from an earlier frame when no Tool objects with that ID exist in the current frame. A Tool object created from the Tool constructor is also invalid. Test for validity with the inherited Pointable.is_valid property.-->

----

### 构造函数

#### Tool([tool]);
构造一个 Tool 对象。

从当前 Frame 或者 Hand 对象中获取一个有效的 Tool 对象。

<!--Constructs a Tool object.

Get valid Tool and Pointable objects from a Frame or a Hand object.-->

```python
tool = frame.tools.frontmost
if tool.is_valid:
    # 使用 tool 数据
```

参数：**tool**(`Pointable`) - 一个 Tool 对象，如果没有设置参数或者参数并不是一个 Tool，则会返回一个无效对象。

<!--Parameters:	tool (Pointable) – An object representing a tool. If no tool parameter is supplied, or the object does not represent a tool, an invalid Tool object is returned.-->

*New in version 1.0*

----

### 类属性
 
#### invalid
类型：Tool
一个无效的工具对象。

*New in version 1.0*