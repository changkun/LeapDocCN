# 序列化追踪数据

`Frame` 类提供了学历恶化一帧中的数据的方法。你可以反序列化这个字节序列来创建一个原始帧的新拷贝。

## 序列化一帧
创建一个 `Frame` 的序列化示例，可以使用 `Frame.serialize`。

下面的代码展示了如何将一帧保存到文件中：

```python
import ctypes

frame = controller.frame()

serialized_tuple = frame.serialize
serialized_data = serialized_tuple[0]
serialized_length = serialized_tuple[1]
data_address = serialized_data.cast().__long__()
buffer = (ctypes.c_ubyte * serialized_length).from_address(data_address)
with open(os.path.realpath('frame.data'), 'wb') as data_file:
    data_file.write(buffer)
```

## 反序列化一帧

在你反序列化一个 `Frame` 数据之前，你必须创建一个 `Controller`对象。如果你想要访问恢复帧中的任何 `Gesture` 数据，你也必须使用 `Controller.enable_gesture()` 函数。访问帧里存储的图像目前还不支持。反序列化来自不同 LeapMotion SDK 版本的数据并没有获得官方支持，如果两个版本中的数据模型没有差异，那么它可能有效。

反序列化帧数据需要以下几个步骤：

1. 创建一个 `Controller` 实例；
2. 获取数据，如果有必要的话将其转换成合适的数据类型；
3. 创建一个 Frame 对象；
4. 调用新帧的 `deserialize()` 方法。

注意，重建后的数据会替换帧中现有的数据。如果使用了已经存在且有效的 `Frame` 实例，那么已经存在的数据会被覆盖。然而任何子对象，例如手、手指等，只要你保持对它们的单独引用。

下面的例子展示了如何从一个文件中反序列化并创建一个 `Frame` 对象。

当你从磁盘加载这个数据，你会获得一个 Python 的字符串对象，然而 deserialize() 函数需要传入一个元组，其中包含一个 Leap.byte_array 对象（一个简单的有限的数组）。你可以使用数据的长度，构造这个 byte_array 对象，然后一个字节一个字节的复制数据或使用 ctypes.memmove() 函数。将字节数组放在元组的第一个位置，并把数据的长度放在第二个位置，再传递给 deserialize() 函数。

```
import ctypes, numpy

frame = Leap.Frame()
filename = "frame.data"
with open(os.path.realpath(filename), 'rb') as data_file:
    data = data_file.read()

leap_byte_array = Leap.byte_array(len(data))
address = leap_byte_array.cast().__long__()
ctypes.memmove(address, data, len(data))

frame.deserialize((leap_byte_array, len(data)))
```

## 保存和读取多个帧

如果你希望保存多个帧，那么你必须相处一个方法来表示一个帧的结束和下一个帧的开始。每一帧数据大小都可能不同。下面的代码展示了一个方法，使用的是存储一个4字节的证书来保存数据的大小：

```
with open("frames.data", "wb") as data_file:
    for f in range(0, 10):
        frame_to_save = controller.frame(9 - f)
        serialized_tuple = frame_to_save.serialize
        data = serialized_tuple[0]
        size = serialized_tuple[1]
        data_file.write(struct.pack("i", size))

        data_address = data.cast().__long__()
        buffer = (ctypes.c_ubyte * size).from_address(data_address)
        data_file.write(buffer)
```

从保存的文件中读取帧，你可以先读取四个字节来获得接下来要读取的帧数据的总长度。然后再重复这个过程直到完成整个文件的读取。

```
with open("frames.data", "rb") as data_file:
    next_block_size = data_file.read(4)
    while next_block_size:
        size = struct.unpack('i', next_block_size)[0]
        data = data_file.read(size)
        leap_byte_array = Leap.byte_array(size)
        address = leap_byte_array.cast().__long__()
        ctypes.memmove(address, data, size)

        frame = Leap.Frame()
        frame.deserialize((leap_byte_array, size))
        next_block_size = data_file.read(4)
```
