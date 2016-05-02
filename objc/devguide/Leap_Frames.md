# 帧

LeapMotion API 将发送给你应用程序的一系列动作追踪数据的快照称之为帧。追踪数据的每一帧所包含的测量位置和有关被检测的每个实体的信息。这篇文章讨论了从 LeapMotion 控制器中获取一个 [Frame](../api/Leap.Frame.md) 对象的细节。

<!--The Leap Motion API presents motion tracking data to your application as a series of snapshots called frames. Each frame of tracking data contains the measured positions and other information about each entity detected in that snapshot. This article discusses the details of getting Frame objects from the Leap Motion controller.-->

## 综述
每个 Frame 对象包含了一个由 LeapMotion 控制器记录的场景瞬间快照。手、手指以及工具都是基本的被 LeapMotion 系统所追踪的物理实体。

可以从连接的 Controller 对象中获取一个 Frame 对象所包含的数据。无论你的应用程序准备好使用 Controller 类中的 `frame()` 方法处理一帧时，你都能够获得一个 Frame。

```
if(controller.is_connected): # 控制器是一个 Leap.Controller 对象
    frame = controller.frame() # 当前帧
    previous = controller.frame(1) # 上一帧
```

`frame()`函数通过 `histore`参数可以进行帧的检索。最后的 60 帧是保存在缓存里的（不要精确以来此值，未来可能会发生变化）。

**注意**：通常情况下，连续的帧会有连续的 ID 值。但是某些情况下有些帧 ID 会被跳过。在资源首先的电脑上，LeapMotion 软件会丢弃一些帧。此外，当软件进入有红外补偿照明的鲁棒模式时，每个帧的两个帧都会被分析。连续的 Frame 对象 ID 每一次都会加二。还有，如果你使用 [Listener](../api/Leap.Listener.md) 回调获取帧，那么回调函数的在第一次调用返回前不会被调用。因此你的应用会丢失一些回调函数长时间处理的帧。这种情况下，丢失的真会被插入到历史缓存中。

## 从帧中获取数据

Frame 对象定义了一系列函数来提供访问帧内数据的方法。例如，下面的代码展示了如何从 LeapMotion 系统中获取一个基本的追踪对象：

```python
controller = Leap.Controller()
#Controller.isConnected() 状态为 True 前保持等待
#...

frame = controller.frame()
hands = frame.hands
pointables = frame.pointables
fingers = frame.fingers
tools = frame.tools
```

Frame 对象返回的所有对象都是只读的。你可以安全的存储并在以后他们。他们是线程安全的，对象使用了 [C++ Boost Library shared pointer class](http://www.boost.org/doc/libs/1_51_0/libs/smart_ptr/shared_ptr.htm#ThreadSafety).

## 通过查询获取帧

当你的应用程序是一个有着自然的消耗帧的速率的应用程序时，查询 Controller 对象中的真是最简单常用也是最安全的获取帧的策略。当你的应用准备处理一帧数据时候，你只需要调用 Controller.frame() 方法即可。

当你查询时，你有可能会在两次不同的查询中获得相同的真（如果你程序处理帧的速率超过了 Leap 的帧速率），也可能跳过其中某些帧（如果 Leap 的速率比你的程序处理的速率高）。大多数情况下，遗漏或者重复获得帧并不重要。比如，如果你在屏幕前使用手来移动一个物体，那么移动依然会是光滑流畅的（假设你的应用的整体速度足够高）。这些情况下，无论如何你都可以使用`history`参数来访问历史帧。

检测你是否已经处理过当前帧的最好办法就是保存你处理过的上一帧的 ID 值，然后与当前帧进行比较：

```
lastFrameID = 0;
def processFrame(self, frame):
    if(frame.id == self.lastFrameID):
        return
    #...
    self.lastFrameID = frame.id
```

如果你的应用已经跳过了一些帧，那么可以使用`frame()`函数的历史参数来访问这些被跳过的帧（只要这些帧还在缓存里）：

```
lastProcessedFrameID = 0
def nextFrame(self, controller):
    currentID = controller.frame().id;
    for history in range(0, currentID - self.lastProcessedFrameID):
        self.processFrame(controller.frame(history))
        self.lastProcessedFrameID = currentID;

def processNextFrame(self, frame ):
    if(frame.is_valid):
        #...process
```

## 通过回调获取帧

另外，你可以使用 Listener 对象从 LeapMotion 控制器获取帧。Controller 对象会在新的一帧可用时调用监听器的 `onFrame()` 方法。在 `onFrame` 处理程序中，你可以调用 `Controller.frame()` 方法来获得 Frame 对象本身。

使用监听器回调是非常复杂的，因为回调涉及到多线程。每次回调都是在一个独立的线程上被调用。你必须确保以线程安全的方式处理任何有多个线程访问的应用程序数据。即便从 API 获得的数据对象是线程安全的，但其他部分可能并不是这样。一个常见的问题就是只能通过只能有特定线程修改的GUI层来更新拥有的对象。在这种情况下，你必须为将你应用做特别的处理，将非线程安全的部分从适当的线程进行更新，而不是回调函数。

下面的例子定义了一个最小的获取新帧数据的 Listener 子类：

```python
class FrameListener(Leap.Listener):

    def onFrame(self, controller):
        frame = controller.frame() # 当前帧
        previous = controller.frame(1) # 上一帧
        #...
```

如你所见，从一个 Listener 对象获取追踪数据和查询的方法基本上是类似的。

值得注意的是，使用 Listener 回调依然有可能跳过一些帧。如果你的 onFrame 回调函数处理时间太长，那么下一阵就会被加到历史缓存中，而且它的 onFrame 回调会被跳过。极少数的情况下，LeapMotion 本身不能及时处理按成一帧时，帧会被丢弃且不会被添加到历史缓存中。这种问题会在计算机在处理任务过多时发生。

## 跨帧追踪实体

如果你有一个实体的 ID 处于不同的帧中，你可以当前帧中获取这个实体。将 ID 传递给 Frame 对象对应的函数即可：

```python
hand = frame.hand(handID)
pointable = frame.pointable(pointableID)
finger = frame.finger(fingerID)
tool = frame.tool(toolID)
```

如果具有相同 ID 的对象无法找到 - 很可能是因为手已经从视野中移出 - 取而代之的是，会返回一个无效的对象。所有的无效对象都是适当类的实例对象，但是他们的成员都会返回 0 值、零向量、或者无效对象。这种技术能够使得彼此之间的方法调用又方便的串在一起。例如，西面的代码段演示了在几个不同帧之间的平均指尖位置:

```python
#Average a finger position for the last 10 frames
count = 0
average = Leap.Vector()
finger_to_average = frame.fingers[0]
for i in range(0,9):
    finger_from_frame = controller.frame(i).finger(finger_to_average.id)
    if(finger_from_frame.is_valid):
        average = average + finger_from_frame.tip_position
        count += 1
average = average/count
```

如果没有无效对象，这个代码就必须在返回 Finger 对象之前检查每个 Frame 对象。无效对象的简化了当你需要访问 LeapMotion 数据你必须做的大量的 null 检查。

## 序列化

Frame 类提供了 `serialize` 和 `deserialize()` 方法让你对帧中数据进行持久化并且在以后重构为一个有效的 Frame 对象。具体请参考[序列化追踪数据](Leap_Serialization.md)。
